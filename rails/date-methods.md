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

Adds 30 seconds
```ruby
Time.now + 30.seconds
=> 2016-02-09 10:01:57 +0000
```

Adds 1 day
```ruby
date + 1.day
=> Wed, 10 Feb 2016
```

Adds 1 day from a parameterised date
```ruby
1.day.since(date = Date.today)
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

Subtracts 30 minutes
```ruby
Time.now - 30.minutes
=> 2016-02-09 09:31:13 +0000
```

Subtracts 1 day
```ruby
date - 1
=> Mon, 08 Feb 2016
```

Subtracts 1 month
```ruby
date - 1.month
=> Sat, 09 Jan 2016
```

Subtracts 1 month from a parameterised date
```ruby
1.month.ago(date = Date.today)
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


### Time in words

Using `ActionView::Helpers::DateHelper`:

```ruby
today_midday_time = Time.new(2016, 2, 9,  12,  0,  0)
today_tea_time    = Time.new(2016, 2, 9,  17,  0,  0)
```

Approximate distance in time between two times in words
```ruby
helper.distance_of_time_in_words(today_midday_time, today_tea_time)
=> "about 5 hours"
```

Approximate distance in time between `Time.now` and a parameterised time
```ruby
helper.time_ago_in_words(today_tea_time)
=> "about 7 hours"
```
