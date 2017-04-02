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
       .:-::- .+/:-``.::-       Uptime: 32d 14h 35m
    .:/++++++/::::/++++++/:`    Packages: 109
  .:///////////////////////:`   Shell: rake
  ////////////////////////`     Resolution: 1440x900
 -+++++++++++++++++++++++`      DE: Aqua
 /++++++++++++++++++++++/       WM: Quartz Compositor
 /sssssssssssssssssssssss.      WM Theme: Graphite
 :ssssssssssssssssssssssss-     Font: Monaco 18
  osssssssssssssssssssssssso/`  CPU: Intel Core i5-2557M @ 1.70GHz
  `syyyyyyyyyyyyyyyyyyyyyyyy+`  GPU: Intel HD Graphics 3000
   `ossssssssssssssssssssss/    RAM: 2298MiB / 4096MiB
     :ooooooooooooooooooo+.
      `:+oo+/:-..-:/+o+/-


RUBY VERSION
ruby --version
ruby 2.3.0p0 (2015-12-25 revision 53290) [x86_64-darwin15]

MRUBY VERSION
./mruby/bin/mruby --version
mruby 1.2.0 (2015-11-17)

./mruby/bin/mrbc -Bbm_ao_render -o bm_ao_render.mrbc bm_ao_render.rb

gcc -std=c99 -Imruby/include bm_ao_render.c -o bm_ao_render.mrbx mruby/build/host/lib/libmruby.a -lm

./mruby/bin/mrbc -Bbm_app_lc_fizzbuzz -o bm_app_lc_fizzbuzz.mrbc bm_app_lc_fizzbuzz.rb

gcc -std=c99 -Imruby/include bm_app_lc_fizzbuzz.c -o bm_app_lc_fizzbuzz.mrbx mruby/build/host/lib/libmruby.a -lm

./mruby/bin/mrbc -Bbm_fib -o bm_fib.mrbc bm_fib.rb

gcc -std=c99 -Imruby/include bm_fib.c -o bm_fib.mrbx mruby/build/host/lib/libmruby.a -lm

./mruby/bin/mrbc -Bbm_so_lists -o bm_so_lists.mrbc bm_so_lists.rb

gcc -std=c99 -Imruby/include bm_so_lists.c -o bm_so_lists.mrbx mruby/build/host/lib/libmruby.a -lm

./mruby/bin/mrbc -Bexpensive -o expensive.mrbc expensive.rb

gcc -std=c99 -Imruby/include expensive.c -o expensive.mrbx mruby/build/host/lib/libmruby.a -lm

./mruby/bin/mrbc -Bstring_concat -o string_concat.mrbc string_concat.rb

gcc -std=c99 -Imruby/include string_concat.c -o string_concat.mrbx mruby/build/host/lib/libmruby.a -lm

BENCHMARK: bm_ao_render
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   7.950000 (  7.961114)
mruby   0.000000   0.000000  36.720000 ( 36.759344)
------------------------------- total: 44.670000sec

            user     system      total        real
ruby    0.000000   0.000000   7.670000 (  7.685080)
mruby   0.000000   0.000000  36.430000 ( 36.823992)

BENCHMARK: bm_app_lc_fizzbuzz
Rehearsal -----------------------------------------
ruby    0.000000   0.010000 105.860000 (109.624123)
mruby   0.000000   0.000000  63.000000 ( 63.143049)
------------------------------ total: 168.860000sec

            user     system      total        real
ruby    0.000000   0.000000 100.460000 (102.298439)
mruby   0.000000   0.000000  65.330000 ( 65.743660)

BENCHMARK: bm_fib
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   5.480000 (  5.941543)
mruby   0.000000   0.000000  28.300000 ( 31.349370)
------------------------------- total: 33.780000sec

            user     system      total        real
ruby    0.000000   0.000000   6.050000 (  6.195110)
mruby   0.000000   0.000000  24.580000 ( 25.075655)

BENCHMARK: bm_so_lists
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   0.940000 (  1.009265)
mruby   0.000000   0.000000  10.410000 ( 10.445364)
------------------------------- total: 11.350000sec

            user     system      total        real
ruby    0.000000   0.000000   0.920000 (  0.926414)
mruby   0.000000   0.000000  11.060000 ( 11.127232)

BENCHMARK: expensive
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   0.850000 (  0.927835)
mruby   0.000000   0.000000   3.660000 (  3.686869)
-------------------------------- total: 4.510000sec

            user     system      total        real
ruby    0.000000   0.000000   0.860000 (  0.873429)
mruby   0.000000   0.000000   3.710000 (  3.769398)

BENCHMARK: string_concat
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   1.460000 (  2.199239)
mruby   0.000000   0.000000   0.960000 (  1.329229)
-------------------------------- total: 2.420000sec

            user     system      total        real
ruby    0.000000   0.000000   1.090000 (  1.320321)
mruby   0.000000   0.000000   1.210000 (  1.936563)
```
