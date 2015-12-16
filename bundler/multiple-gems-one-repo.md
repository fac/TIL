#Background
## Bundler with multiple gems in a single git repository
[Bundler](http://bundler.io), as you might know, is a way of managing your ruby dependencies in a project. You can pull the dependencies ("gems") from a number of different sources, including any git repositiories that Bundler can contact when it is resolving depencies.

Typically, these git repositories contain a single `.gemspec` file that defines a dependency.

```ruby
gem "nokogiri", :git => "https://github.com/tenderlove/nokogiri.git"
```

However, Bundler also allows you to pull in [multiple different gems from a single repository](bundler.io/v1.11/git.html), in a pleasingly simple fashion:

```ruby
git "https://github.com/rails/rails.git" do
  gem "railties"
  gem "action_pack"
  gem "active_model"
end
```

##Learning
If you have access to those dependencies, you probably want to do some integration testing with a the neat `action_pack` branch you've been working on. You might be tempted to do what you would do if you only had one gem per repository. That is to say:

```ruby
git "https://github.com/rails/rails.git" do
  gem "railties"
  gem "action_pack", :branch => "packing-more-action"
  gem "active_model"
end
```

This actually works as you'd expect, but is confusing for a number of reasons:
* Although you might feel like you're only working on one of the gems, you're not. All the other gems will still come from the version on the `packing-more-action` branch.
* This syntax might encourage you to try to use multiple branches, which won't work.

```ruby
#Bundler will not resolve these dependencies
git "https://github.com/rails/rails.git" do
  gem "railties", :branch => "my-development-branch"
  gem "action_pack", :branch => "spike-out-this-one-change"
  gem "active_model"
end
```

Far better is to use all the Gemfile options on the repository itself:
```ruby
git "https://github.com/rails/rails.git", :branch => "my-development-branch" do
  gem "railties"
  gem "action_pack"
  gem "active_model"
end
```

Now you won't be tempted to play with different versions at the same time! I also think that the intent is more clear this way. This is actually listed in the Bundler documentation, but wasn't clear to me!

Note: some examples above lifted in their entirety from the excellent [Bundler documentation](http://bundler.io).
