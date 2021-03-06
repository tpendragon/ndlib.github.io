---
author:   jeremyf
category: practices
filename: 2013-10-04-ruby-and-rails-developer-tools.md
layout:   post
tagline:  A Whirlwind Introduction
title:    Ruby and Rails Developer Tools
tags:     ruby
---

Below is a non-exhaustive list of tools to aid in ruby development.

## Rubygems.org

Given that your Gemfile has the following:

    gem 'active-fedora'

Goto [rubygems.org/gems/active-fedora](http://rubygems.org/gems/active-fedora) and review that page.
You will find links for Documentation, Source Code, Dependencies, etc.

## Ruby on Rails Guides and API

[Rails Guide](http://guides.rubyonrails.org) is an excellent resource on how to do things in Rails.
[Rails API](http://api.rubyonrails.org) is a resource documenting the code API.

## Rspec

> RSpec is testing tool for the Ruby programming language. Born under the banner
> of Behaviour-Driven Development, it is designed to make Test-Driven
> Development a productive and enjoyable experience

In your Gemfile add the following:

    group :development, :test do
      gem 'rspec-rails'
    end

Then run `rails generate rspec:install`.

With an Rspec test suite, run `rspec --format documentation` to see the more "human friendly" assertions.

A [detailed walkthrough via Git annotations](https://github.com/jeremyf/hydra-camp-testing).

## Simplecov

> Code coverage for Ruby 1.9+ with a powerful configuration library…

In your Gemfile add the following:

    gem 'simplecov', :require => false, :group => :test

Then in your `spec/spec_helper.rb`

    require 'simplecov'
    SimpleCov.start

## VCR

> Record your test suite's HTTP interactions and replay them during future test
> runs for fast, deterministic, accurate tests.

Odds are good that you will be incorporating web services in your application.
And testing those things is very slow. Use VCR to record your HTTP interactions
for tests then in future tests use the recorded tapes.

**More at [github.com/vcr/vcr](https://github.com/vcr/vcr)**

## Travis-CI

Free Continuous Integration for Open Source projects. Greatly improves project collaboration.

Let the cloud run your tests!

**More at [travis-ci.org](https://travis-ci.org/)**

## Bundler

> Bundler maintains a consistent environment for ruby applications. It tracks an
> application's code and the rubygems it needs to run, so that an application
> will always have the exact gems (and versions) that it needs to run.

* `bundle console` Opens an IRB session with the bundle pre-loaded
* `bundle show` Shows all gems that are part of the bundle, or the path to a given gem
* `bundle open` Opens the source directory of the given bundled gem
* `bundle viz` Generates a visual dependency graph

**More at [bundler.io](http://bundler.io/)**

## Better Errors (Rails specific)

> Better Errors replaces the standard Rails error page with a much better and
> more useful error page. It is also usable outside of Rails in any Rack app as
> Rack middleware.

In your Gemfile add the following:

    group :development do
      gem "better_errors"
      gem "binding_of_caller"
    end

Then in your browser start clicking around and trying to break things.

> * Full stack trace
> * Source code inspection for all stack frames (with highlighting)
> * Local and instance variable inspection
> * Live REPL on every stack frame

More info at [github.com/charliesome/better_errors](https://github.com/charliesome/better_errors)

## Debugger

In your Gemfile add the following:

* `gem 'debugger'`

Wherever you need a debugger, add `require 'debugger'; debugger`. This works
great with `bundle open` or the `better_errors` gem.

More info at [github.com/cldwalker/debugger](https://github.com/cldwalker/debugger)

Other [debuggers at Ruby Toolbox](https://www.ruby-toolbox.com/search?utf8=%E2%9C%93&q=debugger)

## Locating the method definition

> Returns the Ruby source filename and line number containing this method or
> nil if this method was not defined in Ruby (i.e. native)

From `rails console` or `bundle console`:

Location of an instance method:
```
ActiveRecord::Base.instance_method(:save).source_location
```

Location of a class method:
```
ActiveRecord::Base.method(:find).source_location
```
**More at [ruby-doc.org](http://www.ruby-doc.org/core-1.9.3/Method.html#method-i-source_location)**

## Advanced Method Location

> method_locator provides a way to traverse an object's method lookup path to
> find all places where a method may be defined.

Particularly helpful for determining where `super` is resolving to.

* `gem 'method_locator'`
* `$ bundle console`
* `ActiveRecord::Base.methods_for(:find)`
* `ActiveRecord::Base.method_lookup_path`

**More at [github.com/ryanlecompte/method_locator](https://github.com/ryanlecompte/method_locator)**

## Rake

In Rails you will be using a lot of rake;

* `rake -W` Describe the tasks (matching optional PATTERN) are defined, then exit.
* `rake -T` Display the tasks (matching optional PATTERN) with descriptions, then exit.
* `rake -A` Show all tasks, even uncommented ones
* `rake -P` Display the tasks and dependencies, then exit.

**More at [rake.rubyforge.org](http://rake.rubyforge.org/)**

## Git Bisect

From `man git-bisect`:

> Find by binary search the change that introduced a bug

A bug was introduced somewhere in the code. At commit "A" things were working. At commit "B" things are broken. Write a script (i.e. `test.sh`) that exits status 0 when things are working; and -1 when it is broken.

* `git bisect start`
* `git bisect bad <sha for commit B>`
* `git bisect good <sha for commit A>`
* `git bisect run ./path/to/test.sh`

**A more detailed run through at [blogs.nd.edu/jeremyfriesen](http://blogs.nd.edu/jeremyfriesen/2012/10/08/using-git-bisect-for-finding-when-a-bug-was-introduced/)**

## ND's Puppet Scripts for Building a VM for Curate

> Puppet is IT automation software that helps system administrators manage
> infrastructure throughout its lifecycle, from provisioning and configuration
> to orchestration and reporting.

Hydra is a complicated stack, there are steps to help ease the deployment.

**Notre Dame's Scripts at [github.com/ndlib/curate_nd/tree/master/puppet](https://github.com/ndlib/curate_nd/tree/master/puppet)**

## Ruby Toolbox

A resource for looking up gems by category and seeing usage and maintenance
statistics. More info at [ruby-toolbox.com](https://www.ruby-toolbox.com/)

## Further Hydra Developer Resources

* irc://freenode.net#projecthydra
* hydra-tech@googlegroups.com