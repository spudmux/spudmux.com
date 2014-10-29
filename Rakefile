
def jekyll(opts="", path="")
  sh "rm -rf _site"
  sh path + "jekyll " + opts
end

desc "Build site using Jekyll"
task :build do
  jekyll 'build'
end

desc "Clean Build and Start Server"
task :serve do 
  jekyll 'serve'
end

desc "Deploy to Dev"
task :deploy => :build do
  rsync 'spudmux.com'
end   
  
def rsync(domain)
  sh "rsync -rtz --delete _site/ neahun@spudmux.com:~/#{domain}/"
end
