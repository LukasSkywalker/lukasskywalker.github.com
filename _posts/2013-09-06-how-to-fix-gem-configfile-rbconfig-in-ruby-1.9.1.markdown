---
layout: post
title:  "How to fix `Gem::ConfigFile::RbConfig (NameError)` in Ruby 1.9.1"
date:   2013-09-06 13:01:06
---

I recently had to use a very very old Ruby version for a legacy project. I installed version 1.9.1 via RVM on my Ubuntu 13.04 machine and everything seemed to work great. Until I tried to install the Rails 2.0.2 gem, which produced the following error:

    /home/me/.rvm/rubies/ruby-1.9.1-p431/lib/ruby/site_ruby/1.9.1/rubygems/config_file.rb:82:in `rescue in rescue in <class:ConfigFile>':
      uninitialized constant Gem::ConfigFile::RbConfig (NameError)
      from /home/me/.rvm/rubies/ruby-1.9.1-p431/lib/ruby/site_ruby/1.9.1/rubygems/config_file.rb:64:in `rescue in <class:ConfigFile>'
      from /home/me/.rvm/rubies/ruby-1.9.1-p431/lib/ruby/site_ruby/1.9.1/rubygems/config_file.rb:60:in `<class:ConfigFile>'
      from /home/me/.rvm/rubies/ruby-1.9.1-p431/lib/ruby/site_ruby/1.9.1/rubygems/config_file.rb:36:in `<top (required)>'
      from /home/me/.rvm/rubies/ruby-1.9.1-p431/lib/ruby/site_ruby/1.9.1/rubygems/gem_runner.rb:9:in `require'
      from /home/me/.rvm/rubies/ruby-1.9.1-p431/lib/ruby/site_ruby/1.9.1/rubygems/gem_runner.rb:9:in `<top (required)>'
      from /home/me/.rvm/rubies/ruby-1.9.1-p431/bin/gem:13:in `require'
      from /home/me/.rvm/rubies/ruby-1.9.1-p431/bin/gem:13:in `<main>'
	
I couldn't really get any info about this issue on the internet, but I discovered that the `gem`-command can be fixed by adding the line

    require 'rbconfig'

to the file on the last line of the stack trace. Just add it right after requiring `rubygems` and everything should work perfectly.

