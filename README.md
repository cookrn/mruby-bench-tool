# mruby Bench Tool

A simple tool to use for benchmarking a Ruby script against (c)ruby and mruby on
your local machine. Two example scripts are included with their results from my
laptop pasted below: `expensive.rb` and `string_concat.rb`.

## Install

* Install `ruby`: https://www.ruby-lang.org/en/
* Clone and compile `mruby`: https://github.com/mruby/mruby
* Optionally install `screenfetch`: https://github.com/KittyKatt/screenFetch
* Clone this repository: https://github.com/cookrn/mruby-bench-tool

## Usage

* Optionally add additional *.rb scripts to benchmark
* Run `rake`

```
$ rake
sh sysinfo.sh

                 -/+:.          cookrn@cookrn-macbook-air
                :++++.          OS: 64bit Mac OS X 10.12.3 16D32
               /+++/.           Kernel: x86_64 Darwin 16.4.0
       .:-::- .+/:-``.::-       Uptime: 32d 13h 27m
    .:/++++++/::::/++++++/:`    Packages: 109
  .:///////////////////////:`   Shell: rake
  ////////////////////////`     Resolution: 1440x900
 -+++++++++++++++++++++++`      DE: Aqua
 /++++++++++++++++++++++/       WM: Quartz Compositor
 /sssssssssssssssssssssss.      WM Theme: Graphite
 :ssssssssssssssssssssssss-     Font: Monaco 18
  osssssssssssssssssssssssso/`  CPU: Intel Core i5-2557M @ 1.70GHz
  `syyyyyyyyyyyyyyyyyyyyyyyy+`  GPU: Intel HD Graphics 3000
   `ossssssssssssssssssssss/    RAM: 1879MiB / 4096MiB
     :ooooooooooooooooooo+.
      `:+oo+/:-..-:/+o+/-


RUBY VERSION
ruby --version
ruby 2.3.0p0 (2015-12-25 revision 53290) [x86_64-darwin15]

MRUBY VERSION
./mruby/bin/mruby --version
mruby 1.2.0 (2015-11-17)

./mruby/bin/mrbc -Bexpensive -o expensive.mrbc expensive.rb

gcc -std=c99 -Imruby/include expensive.c -o expensive.mrbx mruby/build/host/lib/libmruby.a -lm

./mruby/bin/mrbc -Bstring_concat -o string_concat.mrbc string_concat.rb

gcc -std=c99 -Imruby/include string_concat.c -o string_concat.mrbx mruby/build/host/lib/libmruby.a -lm

BENCHMARK: expensive
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   0.880000 (  0.887372)
mruby   0.000000   0.000000   1.200000 (  1.197895)
-------------------------------- total: 2.080000sec

            user     system      total        real
ruby    0.000000   0.000000   0.920000 (  0.944652)
mruby   0.000000   0.000000   1.160000 (  1.153831)

BENCHMARK: string_concat
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   1.210000 (  1.388873)
mruby   0.000000   0.000000   0.940000 (  1.133357)
-------------------------------- total: 2.150000sec

            user     system      total        real
ruby    0.010000   0.000000   0.970000 (  1.050362)
mruby   0.000000   0.010000   0.870000 (  0.921770)
```
