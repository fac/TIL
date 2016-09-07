## Removing duplicates from an array of hashes

Let's say you have an array of hashes, like this one:

```ruby
data = [
  {
    :id => 1,
    :email => 'elliot.alderson@allsafe.com'
  },
  {
    :id => 2,
    :email => 'elliot.alderson@allsafe.com'
  },
  {
    :id => 3,
    :email_address => 'elliot.alderson@allsafe.com'
  }
]
```

If you want to extract the unique email addresses you can't call `data.uniq` because the hashes are not themselves unique. However, `uniq` takes a block which allows you to specify on which field to determine uniqueness:

```ruby
data.uniq {|hash| hash[:email] }
=> [{:id=>1, :email=>"elliot.alderson@allsafe.com"}, {:id=>3, :email_address=>"elliot.alderson@allsafe.com"}]
```

If you want to determine uniqueness across multiple fields, you can specify conditions in the block:

```ruby
data.uniq {|hash| hash[:email] || hash[:email_address]}
=> [{:id=>1, :email=>"elliot.alderson@allsafe.com"}]
```
