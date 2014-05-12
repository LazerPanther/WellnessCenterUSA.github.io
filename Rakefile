require "rubygems"
require "tmpdir"

require "bundler/setup"
require "jekyll"



# Change your GitHub reponame eg. "kippt/jekyll-incorporated"
GITHUB_REPONAME = "WellnessCenterUSA/WellnessCenterUSA.github.io"


namespace :site do
  desc "Generate blog files"
  task :generate do
    Jekyll::Site.new(Jekyll.configuration({
      "source"      => ".",
      "destination" => "_site"
    })).process
  end


  desc "Generate and publish blog to gh-pages"
  task :publish => [:generate] do
    Dir.mktmpdir nil, './tmp' do |tmp|
      cp_r "_site/.", tmp
      
      pwd = Dir.pwd
      Dir.chdir tmp
      system "git init"
      system "git add ."
      message = "Site updated at #{Time.now.utc}"
      system "git commit -m #{message.inspect}"
      system "git remote set-url origin git@github.com:WellnessCenterUSA/WellnessCenterUSA.github.io.git"
      system "git push origin master:refs/heads/gh-pages --force"

      Dir.chdir pwd
    end
  end
end
