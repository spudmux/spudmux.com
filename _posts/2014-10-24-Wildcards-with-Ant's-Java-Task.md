---
layout: post
categories: ant wildcard java
---


Recently I was writing an Ant task to pass files to a jar for processing, and ran into an issue using wildcards with the Java task.

	<target name="run">
		<java jar="Echo.jar" fork="true">
			<arg value="src/*.java"/>
		</java>
	</target>

Echo.jar contains a singel class which prints any arguments received to the console.

	public class EchoArguments {
		public static void main(String[] args) {
			System.out.println("Echoing Arguments:");
			for (String arg : args) {
				System.out.println(arg);
			}
		}
	}

Running the task under Windows works as expected:

	run:
		[java] Echoing Arguments:
		[java] src\EchoArguments.java

The one java file in the src folder is passed to the jar. Whereas on Mac it fails to pass the file:

	run-passing-wildcard:
		[java] Echoing Arguments:
		[java] src/*.java

Passing instead the actual value in the Ant file.

## Wildcard Expansion 
The difference in behaviour is down to how Windows and Unix/Mac treat wildcard expansion. For *nix based systems the shell performs the wildcard expansion, whereas on Windows its preformed by the application recieving the arguments.

In Windows when Ant passes the argumennts to the JVM it preforms the whildcard expansion. Whereas on Mac the JVM doesn't preform the expansion and as Ant is starting the JVM and passing the arguments itself there's no shell involved to do the expansion.

## Pathconvert & Fileset
The pathconvert task along with fileset can be used to construct the list of files which can be passed as an argument.

	<pathconvert property="src.files">
		<fileset dir="src" includes="**/*.java"/>
	</pathconvert>
	
Modifying the run target to use the new property and the arg path element.

    <target name="run">
        <java jar="Echo.jar" fork="true">
            <arg path="${src.files}"/>
        </java>
    </target>

Now re-running the test on Windows and Mac produces the same result

	run:
		[java] Echoing Arguments:
		[java] src\EchoArguments.java
