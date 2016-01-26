# How to skip/run a specific test or block in RSpec

##Skip

Adding `x` at the beginning of an iteration `it` or a block: `describe`, `context`.
```ruby
# it
xit ".." do
...
end

# context
xcontext ".." do
...
end

# describe
xdescribe ".." do
...
end
```
And finally executing:
```sh
$ rspec user_spec.rb
```

##Run

Option 1 - Passing a line to run. Useful to run a specific test or block.
```sh
$ rspec user_spec.rb:23
```
Option 2 - Adding `f` at the beginning of a `it` or a block: `describe`, `context`. Useful to run more than one test or block.
```ruby
# Example. Executes only the first and the last test:
fit "returns true" do
...
end

it "returns false" do
...
end

fit "respond with default values" do
...
end
```
And finally executing:
```sh
$ rspec -t focus user_spec.rb
```
