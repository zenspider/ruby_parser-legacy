# -*- ruby -*-

require "rubygems"
require "hoe"

Hoe.plugin :isolate
Hoe.plugin :seattlerb
Hoe.plugin :rdoc
Hoe.plugin :racc

Hoe.spec "ruby_parser-legacy" do
  developer "Ryan Davis", "ryand-ruby@zenspider.com"

  dependency "ruby_parser", "~> 3.13"
  dependency "oedipus_lex", "~> 2.5", :developer # doesn't come in from RP

  license "MIT"

  if plugin?(:racc)
    self.racc_flags << " -t" if ENV["DEBUG"]
    self.racc_flags << " --superclass RubyParser::Legacy::RubyParser"
    # self.racc_flags << " --runtime ruby_parser" # TODO: broken in racc
  end
end

base = "lib/ruby_parser/legacy"
V1 = %w[18 19]

V1.each do |n|
  file "#{base}/ruby#{n}_parser.rb" => "#{base}/ruby#{n}_parser.y"
end

base = "lib/ruby_parser/legacy/ruby_lexer.rex"
file "#{base}.rb" => "#{base}"
file "#{base}.rb" => :isolate

task :clean do
  rm_rf Dir["lib/**/*.output"]
end

# vim: syntax=ruby
