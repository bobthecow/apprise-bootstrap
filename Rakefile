require 'rake/clean'
require 'rake/packagetask'
require 'less'
require 'rainpress'
require 'uglifier'

APPRISE_BOOTSTRAP_VERSION = '1.0.0'

LESS_FILE    = 'apprise-bootstrap.less'
CSS_FILE     = 'apprise-bootstrap.css'
CSS_MIN_FILE = 'apprise-bootstrap.min.css'
JS_FILE      = 'apprise.js'
JS_MIN_FILE  = 'apprise.min.js'

ALL_FILES    = [ CSS_FILE, CSS_MIN_FILE, JS_FILE, JS_MIN_FILE ]

class String
  def unindent
    gsub(/^#{self[/\A\s*/]}/, '')
  end
end

HEADER = <<-doc.unindent
  /*!
   * Apprise Bootstrap v#{APPRISE_BOOTSTRAP_VERSION}
   *
   * Stylish alerts for a Bootstrapped web.
   *
   * https://github.com/bobthecow/apprise-bootstrap
   *
   * @author Justin Hileman <justin@justinhileman.info>
   */
doc

DIST_STYLESHEET = <<-doc.unindent
  @import 'variables';
  @import 'mixins';
  @import 'modals';
  @import 'buttons';
  /** SNIP! **/
  @import 'apprise-bootstrap';
doc

file CSS_FILE => FileList[ LESS_FILE, 'vendor/bootstrap/less/*.less' ] do
  File.open(CSS_FILE, 'w') do |file|
    parser = Less::Parser.new(:paths => ['.', 'vendor/bootstrap/less'], :filename => 'apprise-bootstrap-dist.less')

    file << HEADER
    file << parser.parse(DIST_STYLESHEET).to_css.split('/** SNIP! **/')[1].strip
  end
end

file CSS_MIN_FILE => FileList[ CSS_FILE ] do
  File.open(CSS_MIN_FILE, 'w') do |file|
    file << HEADER
    file << Rainpress.compress(File.read(CSS_FILE))
  end
end

file JS_FILE => FileList[ 'vendor/apprise/apprise-1.5.full.js' ] do
  cp 'vendor/apprise/apprise-1.5.full.js', JS_FILE
end

file JS_MIN_FILE => FileList[ JS_FILE ] do
  ugly = Uglifier.new
  File.open(JS_MIN_FILE, 'w') do |file|
    file << ugly.compile(File.read(JS_FILE))
  end
end

desc "Generate Apprise Bootstrap"
task :build => ALL_FILES

Rake::PackageTask.new('apprise-bootstrap', APPRISE_BOOTSTRAP_VERSION) do |p|
  p.need_tar = true
  p.package_files.include('README.md', *ALL_FILES)
end

CLOBBER.include(*ALL_FILES)

task :default => :build
