## Dates in Rails

Rails provides a lot of methods to play with dates. These are some of them:

Today
```ruby
Date.today
=> Tue, 09 Feb 2016
```

Yesterday
```ruby
Date.yesterday
=> Mon, 08 Feb 2016
```

Tomorrow
```ruby
Date.tomorrow
=> Wed, 10 Feb 2016
```

Create a date
```ruby
date = Date.new(2016, 2, 9)
=> Tue, 09 Feb 2016
```

Beginning of the month
```ruby
date.beginning_of_month
=> Mon, 01 Feb 2016
```

End of the month
```ruby
date.end_of_month
=> Mon, 29 Feb 2016
```

Beginning of the year
```ruby
date.beginning_of_year
=> Fri, 01 Jan 2016
```

End of the year
```ruby
date.end_of_year
=> Sat, 31 Dec 2016
```

Next month
```ruby
date.next_month
=> Wed, 09 Mar 2016
```

Last month
```ruby
date.last_month
=> Sat, 09 Jan 2016
```

Next year
```ruby
date.next_year
=> Thu, 09 Feb 2017
```

Last year
```ruby
date.last_year
=> Mon, 09 Feb 2015
```

### combinations

Beginning of the next month
```ruby
date.next_month.beginning_of_month
=> Tue, 01 Mar 2016
```


### Date manipulation

Adds 1 day
```ruby
date + 1
=> Wed, 10 Feb 2016
```

Adds 1 month
```ruby
date + 1.month
=> Wed, 09 Mar 2016
```

Adds 1 year
```ruby
date + 1.year
=> Thu, 09 Feb 2017
```

Subtracts 1 day
```ruby
date - 1
=> Mon, 08 Feb 2016
```

Subtracts 1 monht
```ruby
date - 1.month
=> Sat, 09 Jan 2016
```

Subtracts 1 year
```ruby
date - 1.year
=> Mon, 09 Feb 2015
```


### Accessors

Day
```ruby
date.day
=> 9
```

Month
```ruby
date.month
=> 2
```

Year
```ruby
date.year
=> 2016
```


### Boolean methods

Today?
```ruby
Date.new(2016, 2, 9).today?
=> true
```

Past?
```ruby
Date.new(2016, 2, 9).past?
=> false
```

Future?
```ruby
Date.new(2016, 2, 10).future?
=> true
```
