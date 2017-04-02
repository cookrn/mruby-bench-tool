BENCHMARKS = Rake::FileList["*.rb"]
EXECUTABLES = BENCHMARKS.ext(".mrbx")
CLEANABLES = Rake::FileList["*.mrbc", "*.c", "*.mrbx"]
PREFIX = ->(t) { (t.name rescue t).split(".").first }

task default: :run

desc "Run the full benchmark suite: install, clean, sysinfo, compile, and bench"
task run: %i(install clean sysinfo compile bench)

desc "Compile all the scripts into mruby executables"
task compile: EXECUTABLES

rule ".mrbc" => ".rb" do |t|
  prefix = PREFIX.(t)
  puts
  sh "./mruby/bin/mrbc -B#{prefix} -o #{t.name} #{t.source}"
end

rule ".c" => ".mrbc" do |t|
  require 'erb'

  prefix = PREFIX.(t)

  template = <<TMPL
#include <mruby.h>
#include <mruby/irep.h>
#include "<%= prefix %>.mrbc"

int
main(void)
{
  mrb_state *mrb = mrb_open();
  if (!mrb) { return 42; }
  mrb_load_irep(mrb, <%= prefix %>);
  mrb_close(mrb);
  return 0;
}
TMPL
  
  File.write("#{prefix}.c", ERB.new(template).result(binding))
end

rule ".mrbx" => ".c" do |t|
  prefix = PREFIX.(t)
  puts
  sh "gcc -std=c99 -Imruby/include #{t.source} -o #{t.name} mruby/build/host/lib/libmruby.a -lm"
end

desc "Remove compiled and templated files ending in .c, .mrbc, and .mrbx"
task :clean do
  require "fileutils"

  CLEANABLES.each do |f|
    FileUtils.rm(f) rescue nil
  end
end

desc "Run the cruby versus mruby benchmarks"
task :bench do
  require 'benchmark'
  
  BENCHMARKS.each do |b|
    prefix = PREFIX.(b)

    puts
    puts "BENCHMARK: #{prefix}"

    Benchmark.bmbm do |experiment|
      experiment.report("ruby") { system "ruby #{b}" }
      experiment.report("mruby") { system "./#{prefix}.mrbx" }
    end
  end
end

desc "Check if mruby is symlinked in the current directory"
task :install do
  unless Dir.exist?("mruby/bin") && File.exist?("mruby/bin/mruby") && File.exist?("mruby/bin/mrbc")
    raise "Please symlink your mruby source directory here as 'mruby' once you have compiled it!"
  end
end

desc "Print system and ruby version infos"
task :sysinfo do
  sh "sh sysinfo.sh"
  puts
  puts "RUBY VERSION"
  sh "ruby --version"
  puts
  puts "MRUBY VERSION"
  sh "./mruby/bin/mruby --version"
end
