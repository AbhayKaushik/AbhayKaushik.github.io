---
layout: post
title:  "Making your first blog"
date:   2019-07-07 10:08:57 +0530
categories: jekyll update
---

So here’s my first blog. It’s more of my experience than it is a step by step guide so **do read before pasting the commands in your terminal**

Reading and writing are very important and have been a integral part of gaining understanding for a long time. 
The best way to conform and absorb what you have read is to write about it.In these times, writing a blog can be just that.

The task of writing your first blog is indeed a difficult thing. Then again, taking the first step for anything worthwhile has always been tough.

I am hosting this blog on [Github Pages][github-pages]. You can should read this blog if you are new to blogging, may it help you

### **Always go step wise**

So I was already behind the deadline I had set and was rushing to quickly set up a blog. I decided to use Jekyll for my github page as it is great for generating minimal stactic pages quickly.
Also, the [Jekyll themes][jekyll-themes] are really cool , you should check them out. 

So, without further ado, I just opened my terminal and entered the first lines that were written on the jekyll homepage, telling I could set up Jekyll in few lines (very tempting indeed)

```bash
~ $ gem install bundler jekyll
~ $ jekyll new my-awesome-site
~ $ cd my-awesome-site
~/my-awesome-site $ bundle exec jekyll serve
```
I manipulated some commands, adding a sudo here and there (those were the dark times; used to sudo anytime the terminal said access denied)

As you may expect,it didn’t work(I didn’t expect that though :P)
And then started the not-very-likable task of finding what I did wrong started.

### **Not so Likeable After All**

I explore and see the homepage a bit more, and lo, there was an Installation link. 
I opened it, looked setting up in Linux distros, and realized that I didn’t have any Ruby environment to begin with. 
Jekyll was written in Ruby, know more about it and some other terms [here][101-link]

The steps are as follows:

```bash
sudo apt-get install ruby-full build-essential zlib1g-dev
```
```bash
echo ' Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```
```bash
somedirectory $ gem install jekyll bundler
somedirectory $ jekyll new my-blog-name
somedirectory $ cd my-blog-name
somedirectory/myblog $ bundle exec jekyll serve
```
Where somedirectory can be any directory

You can know more from the [Jekyll-docs][jekyll-docs]

Keep in mind that the gem install command above works on the local directory.
_I totally forgot that, as I had previously globally installed gem, which in NOT a good practice._

And viola, took me more time due to my haste though.

Following are some things that may confuse you, make sure you follow them through, especially if you are a Linux user 

### **Things to Watch out For**

If you are working on Linux, you will probably see this text when executing jekyll new command :

>```The dependency tzinfo-data (>= 0) will be unused by any of the platforms Bundler is installing for. Bundler is installing for ruby but the dependency is only for x86-mingw32, x86-mswin32, x64-mingw32, java. To add those platforms to the bundle, run bundle lock --add-platform mingw, mswin, x64_mingw, jruby.```

Basically, the command is not required for Unix-based systems
The reason for this has been explained [here][github-issue-link]

To correct it , just open the Gemfile and edit it.
Your Gemfile may look somewhat like this:
```ruby
source "https://rubygems.org"

# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
#gem "jekyll", "~> 3.8.5"

# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "minima", "~> 2.0"

# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
#gem "github-pages", group: :jekyll_plugins

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.6"
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]

# Performance-booster for watching directories on Windows
gem "wdm", "~> 0.1.0" if Gem.win_platform?
```

Remove or comment out the lines (ingnore if using Windows) like this:
```ruby
#gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]
#gem "wdm", "~> 0.1.0" if Gem.win_platform?
```

Also, if you are using Jekyll for Github Pages (which we are), uncomment this line in the Gemfile
```ruby
gem "github-pages", group: :jekyll_plugins
```
After these changes, your file will look something like this.
```ruby
source "https://rubygems.org"

# Hello! This is where you manage which Jekyll version is used to run.
# When you want to use a different version, change it below, save the
# file and run `bundle install`. Run Jekyll with `bundle exec`, like so:
#
#     bundle exec jekyll serve
#
# This will help ensure the proper Jekyll version is running.
# Happy Jekylling!
#gem "jekyll", "~> 3.8.5"

# This is the default theme for new Jekyll sites. You may change this to anything you like.
gem "minima", "~> 2.0"

# If you want to use GitHub Pages, remove the "gem "jekyll"" above and
# uncomment the line below. To upgrade, run `bundle update github-pages`.
gem "github-pages", group: :jekyll_plugins

# If you have any plugins, put them here!
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.6"
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
#gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]

# Performance-booster for watching directories on Windows
#gem "wdm", "~> 0.1.0" if Gem.win_platform?
```

Save the changes and execute the following command:
```bash
bundle update
```
All the required things have now been taken care of. Just execute this command and see the magic at [http:/localhost:4000/][localhost]
```bash
bundle exec jekyll serve
```
### **What's Next**

Well now you have set up Jekyll.You can customize it, and add your content.Check out the jekyll themes for you github page. 
And keep blogging! 

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-themes]: https://jekyllthemes.io
[github-issue-link]: https://github.com/tzinfo/tzinfo-data/issues/12#issuecomment-279554001
[localhost]: http://localhost:4000/
[101-link]: https://jekyllrb.com/docs/ruby-101/
[github-pages]: https://pages.github.com/
