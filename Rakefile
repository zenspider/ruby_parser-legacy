# -*- ruby -*-

require "rubygems"
require "hoe"

Hoe.add_include_dirs File.expand_path "../lib" # HACK: to work with drop_legacy

Hoe.plugin :isolate
Hoe.plugin :seattlerb
Hoe.plugin :rdoc
Hoe.plugin :racc

V1 = %w[18 19]

Hoe.spec "legacy" do
  developer "Ryan Davis", "ryand-ruby@zenspider.com"

  # HACK: until I merge in drop_legacy branch to master and release it:
  # dependency "ruby_parser", "~> 3.12"
  # TODO: remove when above is uncommented:
  dependency "sexp_processor", "~> 4.9"
  dependency "rake", "< 11", :developer
  dependency "oedipus_lex", "~> 2.5", :developer

  license "MIT"

  if plugin?(:racc)
    self.racc_flags << " -t" if ENV["DEBUG"]
    self.racc_flags << " --superclass RubyParser::Legacy::RubyParser"
    # self.racc_flags << " --runtime ruby_parser" # TODO: broken in racc
  end
end

base = "lib/ruby_parser/legacy"
V1.each do |n|
  file "#{base}/ruby#{n}_parser.rb" => "#{base}/ruby#{n}_parser.y"
end

# vim: syntax=ruby
