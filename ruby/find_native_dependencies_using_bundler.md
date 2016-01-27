# Find native dependencies using Bundler

Given a `Gemfile` and a bunch of required rubygems, what's the easiest way of finding out which of the gems have native extensions?

Turns out, it's quite simple. Just interrogate `Bundler` about the dependencies to get the `Gem::Spec` instances representing the gems, which know if a given gem has extensions or not. Then all we need to do is output that information somewhere!

     $ bundle exec ruby -e 'puts Bundler.definition.dependencies.map(&:to_spec).reject {|spec| spec.extensions.empty? }.map {|s| [s.name, s.version] * " = " }'
    mysql2 = 0.3.16
    libv8 = 3.16.14.13
    therubyracer = 0.12.1
    nokogiri = 1.6.3.1
    unicorn = 4.6.3
    json = 1.8.0
    capybara-webkit = 0.14.2
    byebug = 4.0.5
