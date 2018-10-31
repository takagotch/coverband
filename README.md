### coverband
---
https://github.com/danmayer/coverband

```
gem 'coverband'
bundle
gem install coverband

rake -T coverband
rake coverband:clear
rake coverband:coverage


rails new coverage_example
cd coverage_example
atom .

gem 'redis'
gem 'coverband'. '>= 2.0.0.alpha1', require: false
bundle install

rails g scaffold blogs
rake db:migrate

require 'coverband'
Coverband.configure
require 'coverband/tasks'

rake -T coverband

rake coverband:coverage

rails s
open http://localhost:3000/blogs

rake coverband:coverage

rake coverband:clear

rake coverband::coverage_no_filters

require 'coverage'
Coverage.start
require './test/unit/dog.rb'
5.times { Dog.new.bark }
Coverage.peek_result

```

```ruby
# config/coverband.rb
Coverband.configure do |config|
  config.root = Dir.pwd
  config.collector = 'coverage'
  config.redis = Redis.new(url: ENV['REDIS_URL']) if defined? Redis
  config.store = Redis.new(url: ENV['REDIS_URL']) if defined? Redis
  config.ignore = %w[vendor .erb$ .slim$]
  config.root_paths = []
  config.percentage = Rails.env.production? ? 1.0 : 100.0
  config.logger = Rails.logger
  # config.verbose = 'debug'
end


require 'coverband'
Coverband.configure
require 'coverband/tasks'

# config/application.rb
module MyApplication
  class Application < Rails::Application
    require 'coverband'
    Coverband.configure
    config.middleware.use Coverband::Middleware
    
    config.before_initialize do
      require 'coverage'
      Coverband::Collectors::Base.instance.start
    end
  end
end

require File.dirname(__FILE__) + '/config/environment'
require 'coverband'
Coverband.configure
use Coverband::Middleware
run ACtionController::Dispatcher.new


Coverband::Reporter.clear_coverage
Coverband::Reporter.clear_coverage(Redis.new(:host => 'target.com', :port => 6789))

require 'coverband'
Coverband.configure
def before_perform(*args)
  if (rand * 100.0) <= Coverband.configuration.percentage
    @recording_sample = true
    Coverband::Base.instance.start
  else
    @recording_samples = false
  end
end
def after_perform(*args)
  if @recording_samples
    Coverband::Base.instance.stop
    Coverband::Base.instance.save
  end
end

require "coverband"
Coverband.configure
coverband = Coverband::Base.instance
coverband.start
coverband.stop
coverband.save
coverband.sample {
}

require 'coverband'
Coverband.configure
require 'coverband/tasks'
current_tasks = Rake.application.top_level_tasks
if current_tasks.any? && current_tasks.none? { |t| t.to_s.match?(/^coverband:/) }
  current_tasks.unshift 'coverband:start'
  current_tasks.push 'coverband:stop_and_save'
end
namespace :coverband do
  task :start do
    Coverband::Base.instance.start
  end
  task :stop_and_save do
    Coverband::Base.instance.stop
    Coverband::Base.instance.save
  end
end

require 'rails'
class CoverageRunner < ::Rails::Railtie
  runner do
    Coverband::Collectors::Base.instance.start
    at_exit do
      Coverband::Collectors::Base.instance.report_coverage
    end
  end
end

Coverband.configure do |config|
  config.safe_reload_files = ['config/coverband.rb']
end

config.verbose = 'debug'
coverband file usage:
  [],
  [],
  ...
  [],
  []
file:
  // => [], [],
  ...
  []
  
data = JSON.generate Coverband::Reporter.get_current_scov_data
File.write("blah.json", data)
data = JSON.parse(File.read("blah.json"))
Coverband::Reporter.report :additional_scov_data => [data]

# config/coverband.rb
config.s3_bucket = 'coverband-demo'
config.s3_region = 'us-east-1'
config.s3_access_key_id = ENV['AWS_ACCESS_KEY_ID']
config.s3_secret_access_key = ENV['AWS_SECRET_ACCESS_KEY']

# config/routes.rb
Rails.application.routes.draw do
  mount Coverband::Reporters::Web.new, at: '/coverage'
end

devise_constraint = lambda do |request|
  request.env['warden'] && request.env['warden'].authenticate? && request.env['warden'].use.admin?
end
basic_constraint = lambda do |request|
  return true if Rails.env.development?
  if ActionController::HttpAuthentication::Basic.has_basic_credentials?(request)
    credentials = ActionController::HttpAuthentication::Basic.decode_credentials(request)
    email, password = credentials.split(';')
    email == 'foo' && password = 'bar'
  end
end
Rails.application.routes.draw do
  constraints basic_constraint do
    mount Coverband::Reporters::Web.new, at: '/coverage'
  end
end

require 'simpleconv'
SimpleCov.start do
  add_filter 'app/admin'
  add_filter '/spec/'
  add_filter '/config/'
  add_filter '/vendor/'
  add_filter 'userevents'
end

```

```
```


