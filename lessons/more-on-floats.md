## More Float methods

Ruby on Rails enhances certain Ruby classes with additional convenience methods that aren't included in plain ol' Ruby. Many of these are included in the `activesupport` gem that comes with Rails; you could include in a pure Ruby program if you wanted to.

 - To use the following methods within Ruby on Rails, you don't have to do anything.
 - To use the following methods in a plain Ruby script, include the line:

    ```ruby
    require 'activesupport'
    ```

### Formatting Floats as Strings

As we know, you can call the `.to_s` method on a Float to convert the number into a String:

```ruby
10.25.to_s # => "10.25"
```

Within a Rails application[^Rails], you can provide a `Symbol`[^Symbol] as an argument to `Float`'s `to_s` method. This allows you to convert the `Float` to a `String` _and_ add additional formatting at the same time.

[^Rails]:  Or anywhere using `activesupport`.

[^Symbol]: A `Symbol` is a Ruby Class that is similar to a `String`. Symbols start with a colon (`:`) at the beginning. See the chapter section [here][A brief interlude: Symbols]. 

#### Phone

```ruby
5551234.to_s(:phone) # => "555-1234"
```

In addition to providing a `Symbol` to the `to_s` method, you can provide an _additional_ `Hash`[^Hash] argument to tweak the some finer details about how we want to format the Float.

```ruby
1235551234.to_s(:phone, { :area_code => true }                     # => "(123) 555-1234"
1235551234.to_s(:phone, { :country_code => 1 } )                   # => "+1-123-555-1234"
1235551234.to_s(:phone, { :area_code => true, :extension => 555 }) # => (123) 555-1234 x 555
```

[^Hash]: A `Hash` is another Class is Ruby that. See the [Hash chapter](#hash-chapter). In this case, just be aware that this kind of formatting is possible and easy to do in a Rails application.

#### Currency

```ruby
1234567890.50.to_s(:currency)                  # => "$1,234,567,890.50"
67890.506.to_s(:currency, { :precision => 3 }) # => "$67,890.506"
```

#### Percentage

```ruby
100.to_s(:percentage)                                            # => "100.000%"
100.to_s(:percentage, { :precision => 0 } )                      # => "100%"
1000.to_s(:percentage, { :delimiter => ".", :separator => "," }) # => "1.000,000%"
```
