source 'https://rubygems.org'

if ENV['RAILS_SOURCE']
  gemspec path: ENV['RAILS_SOURCE']
else
  # Need to get rails source beacause the gem doesn't include tests
  version = ENV['RAILS_VERSION'] || begin
    require 'net/http'
    require 'yaml'
    spec = eval(File.read('activerecord-fb-adapter.gemspec'))
    version = spec.dependencies.detect{ |d|d.name == 'activerecord' }.requirement.requirements.first.last.version
    major, minor, tiny = version.split('.')
    uri = URI.parse "http://rubygems.org/api/v1/versions/activerecord.yaml"
    YAML.load(Net::HTTP.get(uri)).select do |data|
      a, b, c = data['number'].split('.')
      !data['prerelease'] && major == a && (minor.nil? || minor == b)
    end.first['number']
  end
  gem 'rails', git: "git://github.com/rails/rails.git", tag: "v#{version}"
end

if ENV['AREL']
  gem 'arel', path: ENV['AREL']
end

group :development do
  gem 'bcrypt-ruby', '~> 3.0.0'
  gem 'bench_press'
  gem 'mocha'
  gem 'minitest-spec-rails'
  gem 'fb'
end
