# Sinatra + ActiveRecord Application

## Installing Gems

```ruby
source 'https://rubygems.org'

ruby '3.1.2' # Only this version supported by Heroku

group :test do 
  gem 'rspec'
  gem 'simplecov', require: false # Code coverage analysis
  gem 'simplecov-console', require: false
  gem 'rubocop', '1.20' # Ruby styling
  gem "rack-test", "~> 2.0" # To test responses
  gem "capybara", "~> 3.37" # To test user interaction with the app
end

group :development do # So they won't get installed on the server when deploying app
  gem "tux", "~> 0.3.0" # Interactive console that pre-loads database and ActiveRecord relationships
  gem "dotenv", "~> 2.8" # For storing database variables
  gem "pry", "~> 0.14.1" # For REPL to run ActiveRecord methods
end


gem "bcrypt", "~> 3.1" # Password encryption for security

gem "require_all", "~> 3.0" # Can require all files in the dir instead of require each file separately

gem "sinatra", "~> 3.0" # To create web app
gem "sinatra-contrib", "~> 3.0", require: false # Collection of common Sinatra extensions

gem "activerecord", "~> 7.0" # Object Relation Mapper 
gem "sinatra-activerecord", "~> 2.0" # ActiveRecord extension for Sinatra

gem "webrick", "~> 1.7" # Ruby server

gem "rake", "~> 13.0" # Automates database creation
gem "pg", "~> 1.4" # PostgreSQL
```

## Setting up Sinatra and Connecting to the Database

```
Files structure as following:

in root dir:
- Rakefile
- config.ru

in spec dir:
- spec_helper.rb

in config dir:
- database.yml
- environment.rb

in app dir:
- controllers dir:
  - application_controller.rb
- models dir:
  - peep.rb 
  - user.rb
- views dir: 
  - includes all of HTML pages
```

```ruby
# in Rakefile

ENV["SINATRA_ENV"] ||= "development"

require_relative './config/environment'
require 'sinatra/activerecord/rake'

task :console do
  Pry.start
end

# CL `rake -T` to see the available rake tasks.

# CL `rake console` to initiate Pry (REPL)
```




## Rakefile - Creating Migrations (tables)

```ruby
# in Rakefile (yes, no extension)
require './config/environment'
require 'sinatra/activerecord/rake'
```

```
rake -T # If everything set up correctly - should see the ouput of rake commands

rake db:create_migration NAME=create_users # Last word specifies the name of the table
# After that it should create the file db/migrate/20221006111933_create_users.rb
```

```ruby
# in db/migrate/20221006111933_create_users.rb

class CreateUsers < ActiveRecord::Migration[7.0]
  def change
    create_table :users do |t| # specifying name of the table
      t.string :login
      t.string :username
      t.string :password_hash # Passwords will be converted and stored in a hash
      t.string :email
    end
  end

end
```

```
rake db:create_migration NAME=create_peeps
```

```ruby
# in db/migrate/20221007142644_create_peeps.rb

class CreatePeeps < ActiveRecord::Migration[7.0]
  def change
    create_table :peeps do |t|
      t.text :content
      t.string :tagged_users
      t.timestamps # Automatically creates created_at and updated_at columns
      t.integer :user_id
    end
  end

end
```

```
rake db:migrate SINATRA_ENV="development" # To add tables in the development database
rake db:migrate SINATRA_ENV="test" # To add tables in the test database
```

