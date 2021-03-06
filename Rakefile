require 'spec/rake/spectask'
require 'rake/rdoctask'

task :default => :spec

spec_opts = 'spec/spec.opts'
spec_glob = FileList['spec/**/*_spec.rb']

desc 'Run all specs in spec directory'
Spec::Rake::SpecTask.new(:spec) do |t|
  t.libs = %w(lib spec)
  t.spec_opts = ['--options', spec_opts]
  t.spec_files = spec_glob
end

namespace :spec do
  desc 'Run all specs in spec directory with RCov'
  Spec::Rake::SpecTask.new(:rcov) do |t|
    t.spec_opts = ['--options', spec_opts]
    t.spec_files = spec_glob
    t.rcov = true
    # t.rcov_opts = lambda do
    #   IO.readlines('spec/rcov.opts').map {|l| l.chomp.split " "}.flatten
    # end
  end
  
  desc 'Print Specdoc for all specs'
  Spec::Rake::SpecTask.new(:doc) do |t|
    t.spec_opts = ['--format', 'specdoc', '--dry-run']
    t.spec_files = spec_glob
  end
  
  desc 'Generate HTML report'
  Spec::Rake::SpecTask.new(:html) do |t|
    t.spec_opts = ['--format', 'html:doc/spec_results.html', '--diff']
    t.spec_files = spec_glob
    t.fail_on_error = false
  end
end

desc 'Generate RDoc documentation'
Rake::RDocTask.new(:rdoc) do |rdoc|
  rdoc.rdoc_files.add ['README.markdown', 'LICENSE', 'lib/**/*.rb']
  rdoc.main = 'README.markdown'
  rdoc.title = 'Markdown Ruby parser documentation'
  
  rdoc.rdoc_dir = 'doc'
  rdoc.options << '--inline-source'
  rdoc.options << '--charset=UTF-8'
end

begin
  require 'jeweler'
rescue LoadError
  $stderr.puts "Jeweler not available (gem install technicalpickles-jeweler)"
else
  Jeweler::Tasks.new do |gem|
    gem.name = "bluecloth"
    gem.summary = "A Ruby implementation of Markdown"
    gem.email = "mislav.marohnic@gmail.com"
    gem.homepage = "http://github.com/mislav/bluecloth"
    gem.description = "Markdown allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid XHTML (or HTML)."
    gem.authors = ["Michael Granger", "Mislav Marohnić"]
  end
end
