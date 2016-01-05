# Wrap Parameters in Rails Controller

## Background

We have an API controller actiont that creates a record & returns the ID of it. It takes in an array of ids and a hash of attributes to update each item with. An example JSON request is:

```json
{
  "items": [
    {"recipe_id": 5},
    {"recipe_id": 10}
  ],
  "updated_attributes": {
    "dated_on": "2015-01-03",
    "calories": "1500"
  }
}
```

We end up with a controller action something like:

```ruby
class RecipeUpdatesController < ApiController
  def create
    recipe_ids = params.require(:items).map {|d| d["recipe_id"] }
    updated_attributes = params.require(:updated_attributes)

    @operation = UpdateRecipies.create!(ids: recipe_ids, attrs: updated_attributes)
  end
end
```

## Problem

This action has to support XML requests as well as JSON request. Translating the above into an XML request leads us to the following payload:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<items type="array">
  <items><recipe-id type="integer">5</transaction-id></items>
  <items><recipe-id type="integer">10</transaction-id></items>
</items>
<updated-attributes>
  <dated-on type="date">2015-01-03</dated-on>
  <calories>1500</calories>
</updated-attributes>
```

If we try and send this to rails however, we get an XML parse error on line 6 of the body. XML documents require a single root element, and we've got two: `<items>` and `<updated-attributes>`.

## Solution

The answer is easy, lets just wrap our payload in a single root element, `<recipe-update>`. This leads us to nesting our JSON payload under `"recipe_update"` root key as well.

This is all well and good, except that we've got API clients deployed which currently call this endpoint without the root element. Rather than break the endpoint for them, or have to coordinate deploys it would be nice to support both nested & non-nested request bodies for now. Doing that will complicate our controller code somewhat though, as we'll have to check for & strip or create the root element before trying to use our `params` object.

Except, this is rails! There's a handy helper in the framework for us! Booya! [ParamsWrapper](http://api.rubyonrails.org/classes/ActionController/ParamsWrapper.html) to the rescue. All we need to do is tell it that we expect json & xml requests to the controller to be wrapped in a root element it handles making our `params` consistent before it reaches the controller action.

Now our controller looks like

```ruby
class RecipeUpdatesController < ApiController

  wrap_parameters format: %i(json xml)

  def create
    recipe_update_params = params.require(:recipe_update)
    recipe_ids = recipe_update_params.require(:recipe_ids).map {|d| d["recipe_id"] }
    updated_attributes = recipe_update_params.require(:updated_attributes)

    @operation = UpdateRecipies.create!(ids: recipe_ids, attrs: updated_attributes)
  end
end
```

And hey presto, all three payloads we want to support Just Work™.

```json
{
  "items": […],
  "updated_attributes": {…}
}
```

```json
{
  "recipe_update": {
    "items": […],
    "updated_attributes": {…}
  }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<recipe-update>
  <items type="array"><!-- … --></items>
  <updated-attributes><!-- … --></updated-attributes>
</recipe-update>
````
