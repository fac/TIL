## Transient Arguments in FactoryBot

When defining a factory, you can specify extra "transient" arguments to be used as options when creating.

For example, when creating a recipe, you could add a `salty` option:

```ruby
FactoryBot.define do
  factory :recipe, class: Recipe do
    title "Onion Soup"
    description "an old French classic"
    total_time "4 hours"

    transient do
      salty { true }

      after(:create) do |recipe, evaluator|
        recipe.update_attribute(:title, "Salty " + recipe.title)
      end
    end
  end
end

create(:recipe, salty: true)
=> #<Recipe id: 1, title: "Salty Onion Soup", description: "an old French classic", total_time: "4 hours", created_at: "2019-03-19 04:13:20", updated_at: "2019-03-19 04:13:20">
```

You can also use transient arguments in the same way with Traits:
[https://www.rubydoc.info/gems/factory_bot/file/GETTING_STARTED.md#Traits](https://www.rubydoc.info/gems/factory_bot/file/GETTING_STARTED.md#Traits)
