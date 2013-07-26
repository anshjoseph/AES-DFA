
#### C++ implementation of [Differential Fault Analysis][1] (DFA) of AES-128 using a single fault injection. Software features multi-core support via [OpenMP][2].
---

#### LICENSE
This program is free software; see [LICENSE][3] for more details.

#### REQUIREMENTS
* gcc-4.8.1 or newer.
* [OpenMP][2].
* Python 2.7.5 or newer. (optionally)
* Workstation with at least 32 cores. (recommended)

#### USAGE
##### Example 1
Differential fault analysis of a single ciphertext pair (see input-1.csv) on 32
cores. A fault was injected in byte 11 during the 8-th round of the AES
encryption process.

    cd analysis
    make
    cd ../examples
    ./dfa 32 11 input-1.csv

After the computation is finished all remaining masterkeys are written to
keys-0.csv including the correct key:

    10000005200000063000000740000008

The ciphertext pair in input-1.csv was generated by

    cd simulator
    ./inject 7 11 >> ../examples/input-1.csv

##### Example 2
DFA of multiple ciphertext pairs with distinct keys (see input-2.csv) on 40
cores. Faults were injected at unknown locations (input -1) during the 8-th
round of the AES encryption process.

    cd analysis
    make
    cd ../examples
    ./dfa 40 -1 input-2.csv

After the computation is finished the remaining masterkeys of pair {0,1,2}
are written to keys-{0,1,2}.csv. The correct keys are:

    keys-0.csv: 1234567890abcdef1234567890abcdef
    keys-1.csv: deadc0dedeadc0dedeadc0dedeadc0de
    keys-2.csv: 10000005200000063000000740000008

The data in input-2.csv was generated by

    cd simulator
    ./inject 2 5 >> ../examples/input-2.csv
    ./inject 6 8 >> ../examples/input-2.csv
    ./inject 7 12 >> ../examples/input-2.csv

#### Contact
Philipp Jovanovic <jovanovic@fim.uni-passau.de>

[1]: http://eprint.iacr.org/2009/575
[2]: http://openmp.org/
[3]: https://github.com/Daeinar/dfa-aes/blob/master/LICENSE
