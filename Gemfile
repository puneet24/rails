source 'https://rubygems.org'

gemspec

# We need a newish Rake since Active Job sets its test tasks' descriptions.
gem 'rake', '>= 10.3'

# Active Support depends on a prerelease concurrent-ruby 1.0.0, so track
# latest master as it approaches release.
gem 'concurrent-ruby', '~> 1.0.0.pre3', github: 'ruby-concurrency/concurrent-ruby'

# Active Job depends on the URI::GID::MissingModelIDError, which isn't released yet.
gem 'globalid', github: 'rails/globalid', branch: 'master'
gem 'rack', github: 'rack/rack', branch: 'master'

# This needs to be with require false as it is
# loaded after loading the test library to
# ensure correct loading order
gem 'mocha', '~> 0.14', require: false

gem 'rack-cache', '~> 1.2'
gem 'jquery-rails', github: 'rails/jquery-rails', branch: 'master'
gem 'coffee-rails', '~> 4.1.0'
gem 'turbolinks', github: 'rails/turbolinks', branch: 'master'
gem 'arel', github: 'rails/arel', branch: 'master'
gem 'mail', github: 'mikel/mail', branch: 'master'

gem 'sprockets', '~> 4.0', github: 'rails/sprockets', branch: 'master'
gem 'sprockets-rails', '~> 3.0.0.beta3', github: 'rails/sprockets-rails', branch: 'master'
gem 'sass-rails', github: 'rails/sass-rails', branch: 'master'

# require: false so bcrypt is loaded only when has_secure_password is used.
# This is to avoid ActiveModel (and by extension the entire framework)
# being dependent on a binary library.
gem 'bcrypt', '~> 3.1.10', require: false

# This needs to be with require false to avoid
# it being automatically loaded by sprockets
gem 'uglifier', '>= 1.3.0', require: false
gem 'sass', '>= 3.3', require: false

group :doc do
  gem 'sdoc', '~> 0.4.0'
  gem 'redcarpet', '~> 3.2.3', platforms: :ruby
  gem 'w3c_validators'
  gem 'kindlerb', '0.1.1'
end

# ActiveSupport
gem 'dalli', '>= 2.2.1'
gem 'listen', '~>3.0.2'

# ActiveJob
group :job do
  gem 'resque', require: false
  gem 'resque-scheduler', require: false
  gem 'sidekiq', require: false
  gem 'sucker_punch', require: false
  gem 'delayed_job', require: false
  gem 'queue_classic', github: "QueueClassic/queue_classic", branch: 'master', require: false, platforms: :ruby
  gem 'sneakers', require: false
  gem 'que', require: false
  gem 'backburner', require: false
  gem 'qu-rails', github: "bkeepers/qu", branch: "master", require: false
  gem 'qu-redis', require: false
  gem 'delayed_job_active_record', require: false
  gem 'sequel', require: false
end

# Add your own local bundler stuff
local_gemfile = File.dirname(__FILE__) + "/.Gemfile"
instance_eval File.read local_gemfile if File.exist? local_gemfile

group :test do
  # FIX: Our test suite isn't ready to run in random order yet
  gem 'minitest', '< 5.3.4'

  platforms :mri do
    gem 'stackprof'
    gem 'byebug'
  end

  gem 'benchmark-ips'
end

platforms :ruby do
  gem 'nokogiri', '>= 1.6.7.rc3'

  # Needed for compiling the ActionDispatch::Journey parser
  gem 'racc', '>=1.4.6', require: false

  # ActiveRecord
  gem 'sqlite3', '~> 1.3.6'

  group :db do
    gem 'pg', '>= 0.18.0'
    gem 'mysql', '>= 2.9.0'
    gem 'mysql2', '>= 0.4.0'
  end
end

platforms :jruby do
  gem 'json'
  if ENV['AR_JDBC']
    gem 'activerecord-jdbcsqlite3-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
    group :db do
      gem 'activerecord-jdbcmysql-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
      gem 'activerecord-jdbcpostgresql-adapter', github: 'jruby/activerecord-jdbc-adapter', branch: 'master'
    end
  else
    gem 'activerecord-jdbcsqlite3-adapter', '>= 1.3.0'
    group :db do
      gem 'activerecord-jdbcmysql-adapter', '>= 1.3.0'
      gem 'activerecord-jdbcpostgresql-adapter', '>= 1.3.0'
    end
  end
end

platforms :rbx do
  # The rubysl-yaml gem doesn't ship with Psych by default
  # as it needs libyaml that isn't always available.
  gem 'psych', '~> 2.0'
end

# gems that are necessary for ActiveRecord tests with Oracle database
if ENV['ORACLE_ENHANCED']
  platforms :ruby do
    gem 'ruby-oci8', '~> 2.1'
  end
  gem 'activerecord-oracle_enhanced-adapter', github: 'rsim/oracle-enhanced', branch: 'master'
end

# A gem necessary for ActiveRecord tests with IBM DB
gem 'ibm_db' if ENV['IBM_DB']
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
