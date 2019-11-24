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


# Rspec

rspec


bundle exec rake db:drop RAILS_ENV=test
bundle exec rake db:create RAILS_ENV=test
bundle exec rake db:schema:load RAILS_ENV=test


running specs

rpsec —fail-fast

equivalence matchers:
eq, eql, equal
==, type srtict, object id

truthiness matchers
to be(true) or truthy 

numeric matchers:
to be </>/>=
to be_between(1,2).inclusive/exclusive
to be_within(5).of(105)
expect(1..10).to cover(3)

collection matchers(string/array/hash):

to include(3), 
to start_with, end_with
to eq([1,2]) order matters
to match_array([1,2]) order does not matter
to contain_excatly(1,2,3)

other matchers:

regex matchers
to match(/regex/) only with strings it works

object type matchers
(obj)to be_instance_of(class)
to be_an_instance_of(class)
to be_kind_of(class) (inheritance case, animal -> mama -> dog)
to be_a_kind_of(class)
to be_a(class)
to be_an()

respond to matcher:

to respond_to(:method_name)

atrribute mathcer:
to have_attributes(:attr_name => ‘eg')

satisfy matcher:
(use it as last resort)
to satisfy {|| } or
to satisfy do |v|
# 
end


predicate(true/false) matchers:
nil? odd? in ruby

dynamic methods
expect(product).to be_visible or expect(product.visible).to be true

to be_nil
to be_odd
to be_even
to be_zero
to be_non_zero
to be_integer
to be_empty

hash

expect(hash).to have_key(:city)
expect(hash).to have_value(‘dallas’)

observation matchers:

syntax:
do end also

 expect{}.to()

array = []
expect{ array << 1}.to change(array, :empty?).from(true).to(false)

expect { x+=1 }.to change{x}.from(10).to(11)

expect{x+=1}.to change{x}.by(1)
expect{x+=1}.to change{x}.by_at_least(1)
expect{x+=1}.to change{x}.by_at_most(1)

observer errors:

expect {customer.delete}.to raise_error
expect {customer.delete}.to raise_exception

expect{1/0}.to raise_error.with_message(“msg”)
expect{1/0}.to raise_error(ZeroDivisionError)
expect{1/0}.to raise_error.with_message(/regex/)

observer output:

stdout

expect{print ‘hello’}.to output.to_stdout

expect{print ‘hello’}.to output(‘hello’).to_stdout

expect{print ‘hello’}.to output(/regex/).to_stdout

expect{warn ‘hello’}.to output(/hello/).to_stderr


complex observation:

compound expectations:

and/or &/|

to start_with(‘L’).and end_with(‘a’)
to be_even.or be < 6

to start_with(‘L’) & end_with(‘a’)
to be_even | be < 6


composing matchers:

 some matchers expect other matchers as arguments (mixing and matching)

all

expect(arr).to all(be < 5)

expect(arr).to all(be_visible & be_in_stock) 
(predicate matchers)

  all(matcher)
  include(matcher, matcher)
  start_with(matcher)
  end_with(matcher)
  contain_excatly(matcher, matcher, matcher)
  match(matcher) 

  change {}.from(matcher).to(matcher)
  change {}.by(matcher)
  output(matcher).to_stdout
  rase_error.with_message(matcher)


ch 5:

 tester efficency

File.expand_path(‘../..’, __FILE__)

 hooks:
  before, after, around

 Let method:

 used for setting variables
 
  @car =|| Car.new

  Setting a Subject:

  let(:subject) { Car.new }
   subject { Car.new }

implicit defined subject:
 
describe Car
  it “describes” do
    expect(subject.method).to eq(4)
  end
end

Shared Examples:
DRYing code using modules

ch6:

 Test Doubles:
  doubles, mocks, stubs, fakes, spies, dummies

 using mock and stub 
 
 in rspec 3
  mock => double #fake object
  stub => allow #fake method

  it “allows stubbing methods” do
    dbl = double(“chant”) #create a fake/mock object
    allow(dbl).to recieve(:hey!)
    expect(dbl).to respond_to(:hey!)
  end

  #to return a value from method
  # syntax 1
  it “allows stubbing methods” do
    dbl = double(“chant”) #create a fake/mock object
    allow(dbl).to recieve(:hey!) { “Ho!” }
    expect(dbl.hey!).to eq(“Ho!”)
  end

  #syntax 2
  it “allows stubbing methods” do
    dbl = double(“chant”) #create a fake/mock object
    allow(dbl).to recieve(:hey!).and_return(“Ho!”)
    expect(dbl.hey!).to eq(“Ho!”)
  end

  # used to stub multiple methods but not avisible
  allow(dbl).to recieve_messages(:met1 => ‘a’, :met2 => ‘b’)
  expect(dbl.met1).to eq(“a”)
  expect(dbl.met2).to eq(“b”)

  #simpler syntax
  
   dbl = double(“Person”, :met1 => ‘a’, :met2 => ‘b’)
   expect(dbl.met1).to eq(“a”)
   expect(dbl.met2).to eq(“b”)
  
  #multiple response from method / random return values
 
   dbl = double(“Die”)
   allow(dbl).to recieve(:roll).and_return(1,2,3)
   expect(dbl.roll).to eq(1)
   expect(dbl.roll).to eq(2)
   expect(dbl.roll).to eq(3)


 partial test doubles:
  real objects with test double(stub)

  time = Time.new(2010,1,1,12,0,0)

  allow(time).to recieve(:year).to recieve(:year).and_return(1975)
  expect(time.to_s).to eq(‘2010-01-01 12:00:00 -0500’) #call to actual method
  expect(time.year).to eq(1975) # call to stubbed method

  #mocking db

  dbl = double(‘Mock Customer’) #fake object
  allow(dbl).to recieve(:name).and_return(‘Bob’) #fake object to receive a method
  allow(Customer).to recieve(:find).and_return(dbl) #partial double
  c = Customer.find
  expect(c.name).to eq(‘Bob’)
  
 # same with multiple objects

 c1 = double(‘F1’, :name => ‘bob’)
 c2 = double(‘F2’, :name => ‘Mary’)
 
  allow(Customer).to recieve(:all).and_return([c1,c2])
  expect(c[1].name).to eq(‘Mary’)

message expectations: (objects that send messages to trigger methods)

 # see diff
 dbl = double(“chant”)
 allow(dbl).to recieve(:hey!).and_return(“Ho!”)
 expect(dl.hey!).to eq(“Ho!”)

  #actual testing of messages
  dbl = double(“chant”)
  expect(dbl).to recieve(:hey!).and_return(“Ho!”)
  dl.hey!

 #using multiple calls but in order to be called if not remove ordered
 dbl = double(“Multi”)
 expect(dbl).to recieve(:step_1).ordered 
 expect(dbl).to recieve(:step_2).ordered 

 dbl.step_1
 dbl.step_2 # if order interchanged error will be thrown

Message argument constraints:

#passing args for methods

 dbl = double(“Customer List”)
 expect(dbl).to recieve(:sort).with(‘name’) #specific argument
 db.sort(‘name’)

 #for any argument
 expect(dbl).to recieve(:sort).with(any_args)
 db.sort(‘name’)

 #matchers

 with(any_args)
 with(no_args)
 with(‘Rspec’)
 with(‘Rspec’, 1234, true, [:a, :b, :c])
 with(‘Rspec’, anything)  # method(‘Rspec’, 1, s f) 
 with(boolean)
 with(hash_including(:verbose => true))
 with(array_including(‘blue’))
 with(a_multipleof(3))
 with(<< any matcher >>) # see complex matchers for example

message count constraint:

 # to check how many times a method gets called

  post = double(‘blog post’)
  expect(post).to recieve(:like).excatly(3).times # recieve().once / twice/ excatly(n) / at_least(:once) / at_least(:twice) / at_least(n).times / at_most(:once) / at_most(:twice) / at_most(n).times
  post.like(:user => ‘bob’)
  post.like(:user => ‘mary’)
  post.like(:user => ‘ted’)

 # see diff carefully
  cart = Cart.new
  cart.add_item(3)
  cart.add_item(2)
  
  expect(cart).to recieve(:restock_item).twice
  cart.empty

 ## class Cart
     def add_item()
     end
     
      def restock_item
      end
     
      def empty
        restock_item
        restock_item
      end
    end


spies:

  dbl = spy(“chant”)
  allow(dbl).to recieve(:hey!).and_return(“ho!”)
  dbl.hey!
  expect(dbl).to have_recieved(:hey!)

  even count constraints can be used 
  dbl = spy(“chant”)
  allow(dbl).to recieve(:hey!).and_return(“ho!”)
  dbl.hey!
  dbl.hey!
  expect(dbl).to have_recieved(:hey!).twice

  # spies are little looser in working, we need not stub methods
  cust = spy(“Customer”)
  #allow(just).to recieve(:send_invoice) #stubbing
  cust.send_invoice
  expect(cust).to have_recieved(:send_invoice) 

  # spies with partial doubles
  c = Customer.new
  allow(c).to recieve(:send_invoice) # necessary if used with partial doubles
  c.send_invoice
  expect(c).to have_recieved(:send_invoice) 

 # using spies with let and before
  let(:order) do
    spy(‘Order’, meth1 => nil, meth2 => nil)
  end 
 
  before(:example) do
    order.meth1
    order.meth2 
  end

 it “” do
  expect(order).to have_recieved(:meth1)
 end

 it “” do
  expect(order).to have_recieved(:meth2)
 end

ch 7 :

 challenges:

 TODO

ch - 8
ROR 

generators

 rails generate rspec:model Customer

Test Databases

rake db:test:prepare

or

rake db:drop RAILS_ENV=test
rake db:create RAILS_ENV=test
rake db:schema:load RAILS_ENV=test


Transactional examples:
spec runs as transactions in order to the db clean

in rails helper this can be set
config.use_transactional_fixtures = true or
config.use_transactional_examples = true

diff between before(:exampe) and before(:context)

data modified by example is rolled back automatically

data used by context will not be rolled back and has to handled like shown below

 before(:context) do
    @cust = Customer.create(name: ‘jane’)
 end

 after(:context) {@customer.destroy}

gem database_cleaner can be used instead of transactions



Model Specs:

 use reload
 let => does  trigger immediately until a call to it is made
 let! => get called immediately

for validations and associations use should-matchers

active record test doubles:

 rspec-activemodel-mocks gem

Helper Specs

there is helper object

module ApplicationHelper
  def abc(a)
  end
end

 describe ApplicationHelper do
    describe “blah” do
       it “blah” do
         expect (helper.abc(2)).to eq(2)
       end
   end
end

controller specs Requests:

simulate requests with the following

get(action, options)
post(action, options)
patch(action, options)
put(action, options)
delete(action, options)

action => index, show, method_1…n
options =>  url params, form data

ex:

 get(:index) or get(“/:controller/:method”)

get(:index, :page => 2, :search => ‘smith’) # url params or {:page => 2, :search => ‘smith’}
post(:create, :customer => {:first_name => ‘test’, :country => ‘US’}) 

controller spec attributes: #controller objects

controller 
request
response

assigns
session
flash
cookies


example

@c = Customer.all

spec:

let(customer) {  Customer.all }
# notes assigns is diff then assign(to assign an instance variable in specs)
# assigns(‘c’) or assigns(:c) will work see diff [] and ()
 it “” do
    get :index
    expect(assigns[‘c’]).to eq(customer) # assigns[:c] does not work
 end

cookies[‘logged_in’]

 use request.cookies[‘logged_in’]

controller responses:

expect(response).to render_template(template)

     redirect_to(path)
    have_http_status(status)

  status code

  either one can be used symbol or num
  200, :ok
  403, :forbidden
  404, :not_found 
  301, :moved_permanently
  302, :found
  500, :internal_server_error
  502, :bad_gateway
 
for more search rails status codes


render_views

 by default rspec stubs rendering of the body content, so expect(response.body).to eq(‘’) will work

 if we need to actual views to render then

 describe ‘Get index’ do
  render_views
  
   it “” do
     get :index
     expect(response).to render_template(‘customer/index’)
     expect(response.body).to match(/Customer List/)
   end
 end

gotcha

#it slow down
#renders vies for all that group
# better alternatives are there using view specs

View Specs:

# less important

describe ‘controller/method’ do
end

three parts

1) instances variables set
2) render template
3) set expectations

helper methodsL

 view
assign
render
rendered

ex


describe ‘customer/index’ do
  it “displays all customers” do
    assign(:customers, [Customer.new(:name => ‘Alice’)])
    
    render # render(:template => ‘customer/index,html.erb’)
    
   expect(rendered).to match(/Alice/)
  end
end


testing partials

  expect(view).to render_template(:partial => ‘_customer’, :count => 3)
  expect(view).to render_template(:partial => ‘_customer’, :locals => {:page => 1})

to set template explicitly

  render(:template => ‘customer/index,html.erb’)

 by default it does not render the layout file if required then 

   render(:template => ‘customer/index,html.erb’, :layout => ‘layouts/application’)

  stub template:

  stub rendering of partials

 stub_template(template_file_name => new_template)

 ex:

  assigns(:c => [C.new(:name => ‘A’)])
 
  stub_template(“customers/_customer.html.erb” => “<%= c.name.reverse %>”)

 expect(rendered).to match(/A/)

other specs

routing
mailer
request
feature 

ch9 :
 TDD

ch 10 :

fixtures and Factories
