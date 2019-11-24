# Blorgh
Short description and motivation.

## Usage
How to use my plugin.

## Installation
Add this line to your application's Gemfile:

```ruby
gem 'blorgh'
```

And then execute:
```bash
$ bundle
```

Or install it yourself as:
```bash
$ gem install blorgh
```

## Contributing
Contribution directions go here.

## License
The gem is available as open source under the terms of the [MIT License](http://opensource.org/licenses/MIT).


# Important
  Rails:

Model:

 ActiveModel::Serializer
  to_json, from_json => from json to class using 
  need to define 
      def attributes=(hash)
        hash.each do |key, value|
           send("#{key}=", value)
        end
      end

  def attributes
    instance_values
  end

 ActiveModel::Validator 
 
class MyValidator < ActiveModel::Validator
  def validate(record)
    unless record.name.starts_with? 'X'
      record.errors[:name] << 'Need a name starting with X please!'
    end
  end
end
 
class Person
  include ActiveModel::Validations
  validates_with MyValidator
end

  
Controller:

* ActionDispatch::Session::CookieStore - Stores everything on the client.
* ActionDispatch::Session::CacheStore - Stores the data in the Rails cache.
* ActionDispatch::Session::ActiveRecordStore - Stores the data in a database using Active Record. (require activerecord-session_store gem).
* ActionDispatch::Session::MemCacheStore


ActionDispatch::Request
ActionDispatch::Response
ActionDispatch::SSL

Routes:

 INCSEUD
 resources
 resource
 namespace => if modules used
 concern => like common code to reuse
 member => single record return with custom name
 collection => multiple records returned with custom name
 shallow => INC, limit nesting. 
constraints => conditions on routes like subdomains, specific IDS



mattr, 
cattr => @@name, static variable
attr_internal => to avoid name collision with same name, @_name_var


Start-up:
  
1)  Rails::AppLoader.exec_app executes -> bin/rails
     bin/rails -> calls config/boot.rb -> bundler/setup(set up gems from Gemfile)
2.  then calls rails/commands(rails/commands.rb) in config/boot.rb -> 
3.  When require APP_PATH is executed, config/application.rb is loaded   

Action Dispatch is the routing component of the Rails framework

# Rack
  * https://www.engineyard.com/blog/understanding-rack-apps-and-middleware
  * https://auth0.com/blog/ruby-authentication-secure-rack-apps-with-jwt/
  * https://stackoverflow.com/questions/16577139/trigger-basic-http-auth-from-within-middleware
  * https://dzone.com/articles/ruby-authentication-secure-your-rack-application-w
  * https://www.justinweiss.com/articles/a-web-server-vs-an-app-server/

