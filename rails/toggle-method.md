# Toggle booleans

In Rails (ActiveRecord) you can use `record.toggle!(:field_name)` if you need to quickly toggle boolean fields from `false -> true -> false -> true...`

See: [ActiveRecord/Persistence.html#method-i-toggle](https://api.rubyonrails.org/classes/ActiveRecord/Persistence.html#method-i-toggle)

Great for when you need to switch something on/off in a PPT via the Rails console.

e.g.

```ruby
accountancy_practice_profile.toggle!(:hidden)

# Also without the bang, if you want validations errors rather than exceptions:
acoountancy_practice_profile.toggle(:hidden)
```
