# GOAL

This is a demo to show-case how to create models with tags in a rails app.

It was created from [this repo](https://github.com/andrerferrer/filter-by-tags-demo).

[You can also check my other demos](https://github.com/andrerferrer/dedemos/blob/master/README.md#ded%C3%A9mos).

## What needs to be done?

Follow the Mantra 🕉: Routes -> Controller -> View 

Nothing to change in the routes, because nothing is new here.

Let's go to the controller.

### 1. In the controller

Truth be told, we only need to allow some extra `strong params` here. So, we can add them:
```ruby
  def strong_params
    params.require(:restaurant).permit(:name, :address, tag_ids: [])
  end
```

### 2. The View

Add one the `association` to your `simple_form_for`

In the `app/views/restaurants/new.html.erb`:

```erb
  <%= f.association :tags, multiple: true, as: :check_boxes %>
```

### 3. Refactoring
We can also refactor this using a constant in the model:

In the controller
```ruby
  def strong_params
    params.require(:restaurant).permit(Restaurant::STRONG_PARAMS)
  end
```

In the model
```ruby
class Restaurant < ApplicationRecord
  STRONG_PARAMS = [
    :name,
    :address,
    tag_ids: []
  ]

  # rest of the code here
end
```

And we're good to go 🤓

Good Luck and Have Fun