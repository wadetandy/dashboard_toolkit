require 'rubygems'
require 'bundler'
require 'appraisal'

$:.unshift(File.dirname(__FILE__) + "/lib")
require 'dashboard_toolkit/version'


PKG_NAME    = ENV['PKG_NAME']    || "dashboard_toolkit"
PKG_VERSION = ENV['PKG_VERSION'] || DashboardToolkit::VERSION


# Run test by default.
task :default => :spec

spec = Gem::Specification.new do |s|
  s.name              = PKG_NAME
  s.version           = PKG_VERSION
  s.authors = ["Wade Tandy"]
  s.date = "2016-05-12"
  s.description = "Collection of useful classes for building dashboard-style interfaces"
  s.email = "wade.tandy@gmail.com"
  s.summary = "Collection of useful classes for building dashboard-style interfaces"

  s.files             = `git ls-files`.split("\n")
  s.test_files        = `git ls-files -- {test,spec,features}/*`.split("\n")
  s.require_paths     = %w( lib )

  s.add_development_dependency "rails", ">= 4.0"
  s.add_development_dependency "appraisal"
  s.add_development_dependency "mocha", ">= 1.0"
  s.add_development_dependency "yard"
  s.add_development_dependency 'rspec'
  s.add_development_dependency 'rspec-rails'
end


require 'rubygems/package_task'

Gem::PackageTask.new(spec) do |pkg|
  pkg.gem_spec = spec
end

desc "Build the gemspec file #{spec.name}.gemspec"
task :gemspec do
  file = File.dirname(__FILE__) + "/#{spec.name}.gemspec"
  File.open(file, "w") {|f| f << spec.to_ruby }
end

desc "Remove any temporary products, including gemspec."
task :clean => [:clobber] do
  rm "#{spec.name}.gemspec"
end

desc "Remove any generated file"
task :clobber => [:clobber_package]

desc "Package the library and generates the gemspec"
task :package => [:gemspec]

# Bundler.setup
# Bundler::GemHelper.install_tasks
begin
  require 'rspec/core/rake_task'
  RSpec::Core::RakeTask.new(:spec)
rescue LoadError
end
