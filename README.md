# str_enum

Don’t like storing enums as integers in your database? Introducing...

String enums for Rails!! :tada:

- scopes
- validations
- accessor methods
- state change methods

## Getting Started

Add this line to your application’s Gemfile:

```ruby
gem 'str_enum'
```

Add a string column to your model.

```ruby
add_column :users, :status, :string
```

And use:

```ruby
class User < ActiveRecord::Base
  str_enum :status, [:active, :archived]
end
```

The first value will be the initial value. This gives you:

#### Scopes

```ruby
User.active
User.archived
```

#### Validations

```ruby
user = User.new(status: "unknown")
user.valid? # false
```

#### Accessor Methods

```ruby
user.active?
user.archived?
```

### State Change Methods

```ruby
user.active!
user.archived!
```

#### Forms

```erb
<%= f.select :status, User.statuses.map { |s| [s.titleize, s] } %>
```

## Options

Choose which features you want with:

```ruby
class User < ActiveRecord::Base
  str_enum :status, [:active, :archived],
    scopes: false,
    validate: false,
    accessor_methods: false,
    default: nil
end
```

Prevent method name collisions with the `prefix` and `suffix` options.

```ruby
class User < ActiveRecord::Base
  str_enum :address_status, [:active, :archived], suffix: :address
end

# scopes
User.active_address
User.archived_address

# accessor methods
user.active_address?
user.archived_address?

# state change methods
user.active_address!
user.archived_address!
```

## History

View the [changelog](https://github.com/ankane/str_enum/blob/master/CHANGELOG.md)

## Contributing

Everyone is encouraged to help improve this project. Here are a few ways you can help:

- [Report bugs](https://github.com/ankane/str_enum/issues)
- Fix bugs and [submit pull requests](https://github.com/ankane/str_enum/pulls)
- Write, clarify, or fix documentation
- Suggest or add new features
