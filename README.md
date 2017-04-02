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
       .:-::- .+/:-``.::-       Uptime: 32d 16h 5m
    .:/++++++/::::/++++++/:`    Packages: 109
  .:///////////////////////:`   Shell: rake
  ////////////////////////`     Resolution: 1440x900
 -+++++++++++++++++++++++`      DE: Aqua
 /++++++++++++++++++++++/       WM: Quartz Compositor
 /sssssssssssssssssssssss.      WM Theme: Graphite
 :ssssssssssssssssssssssss-     Font: Monaco 18
  osssssssssssssssssssssssso/`  CPU: Intel Core i5-2557M @ 1.70GHz
  `syyyyyyyyyyyyyyyyyyyyyyyy+`  GPU: Intel HD Graphics 3000
   `ossssssssssssssssssssss/    RAM: 2180MiB / 4096MiB
     :ooooooooooooooooooo+.
      `:+oo+/:-..-:/+o+/-


RUBY VERSION
ruby --version
ruby 2.4.1p111 (2017-03-22 revision 58053) [x86_64-darwin16]

MRUBY VERSION
./mruby/bin/mruby --version
mruby 1.2.0 (2015-11-17)
git log -1
commit a49c9f86e73d76cbeba30e1affda874fcab0a504
Author: Yukihiro "Matz" Matsumoto <matz@ruby-lang.org>
Date:   Mon Apr 3 00:05:16 2017 +0900

    Update callinfo->target_class in mrb_exec_irep(); fix #3543

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
ruby    0.000000   0.000000   8.010000 (  8.032256)
mruby   0.000000   0.000000  41.350000 ( 46.825119)
------------------------------- total: 49.360000sec

            user     system      total        real
ruby    0.000000   0.000000   9.100000 (  9.399123)
mruby   0.000000   0.000000  35.970000 ( 36.391348)

BENCHMARK: bm_app_lc_fizzbuzz
Rehearsal -----------------------------------------
ruby    0.000000   0.000000 104.550000 (109.046081)
mruby   0.000000   0.000000  80.230000 ( 83.029188)
------------------------------ total: 184.780000sec

            user     system      total        real
ruby    0.000000   0.000000 112.820000 (117.137334)
mruby   0.000000   0.000000  67.490000 ( 67.952091)

BENCHMARK: bm_fib
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   4.720000 (  4.774076)
mruby   0.000000   0.000000  23.750000 ( 24.465618)
------------------------------- total: 28.470000sec

            user     system      total        real
ruby    0.000000   0.000000   4.850000 (  4.903897)
mruby   0.000000   0.000000  27.540000 ( 28.468836)

BENCHMARK: bm_so_lists
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   1.010000 (  1.066049)
mruby   0.000000   0.000000  87.250000 ( 88.961688)
------------------------------- total: 88.260000sec

            user     system      total        real
ruby    0.000000   0.000000   0.910000 (  0.932768)
mruby   0.000000   0.000000  83.030000 ( 83.518203)

BENCHMARK: expensive
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   0.880000 (  0.985178)
mruby   0.000000   0.000000   3.110000 (  3.137985)
-------------------------------- total: 3.990000sec

            user     system      total        real
ruby    0.000000   0.010000   0.880000 (  0.879990)
mruby   0.000000   0.000000   3.500000 (  3.501646)

BENCHMARK: string_concat
Rehearsal -----------------------------------------
ruby    0.000000   0.000000   1.400000 (  2.008662)
mruby   0.000000   0.000000   0.880000 (  1.058646)
-------------------------------- total: 2.280000sec

            user     system      total        real
ruby    0.000000   0.000000   0.870000 (  0.939528)
mruby   0.000000   0.000000   0.800000 (  0.857720)
```
