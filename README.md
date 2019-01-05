

Copyright (c) 2018, Blurrycash</br>

*See [LICENSE](LICENSE).*<br>


<h1 id="compile-linux">Compiling from Source on Linux</h1>

**Step 1:** Clone this repository recursively, to pull in needed submodules:

>`git clone https://github.com/bizshady/blurrycash.git`

**Step 2:** Install dependencies:

Ubuntu 18.04.1 One-Liner:

>`sudo apt-get install -y build-essential cmake pkg-config libboost-all-dev libssl-dev libzmq3-dev libunbound-dev libnorm-dev libpgm-dev libsodium-dev libminiupnpc-dev libunwind8-dev liblzma-dev libreadline6-dev libldns-dev libexpat1-dev libgtest-dev doxygen graphviz`

Debian 9/Ubuntu 16.04 One-Liner:

>`sudo apt-get install -y build-essential cmake pkg-config libboost-all-dev libssl-dev libzmq3-dev libunbound-dev libpgm-dev libsodium-dev libminiupnpc-dev libunwind8-dev liblzma-dev libreadline6-dev libldns-dev libexpat1-dev libgtest-dev doxygen graphviz`

Arch Linux One-Liner:

>`sudo pacman -S base-devel cmake boost openssl zeromq libpgm unbound libsodium libunwind xz readline ldns expat gtest doxygen graphviz`

**Step 3:** `cd` into the the directory where the source code was cloned. 

>`cd ~/blurrycash`

**Step 4:** Create a new build directory and change into it by running the following:

>`mkdir build && cd $_`

**Step 5:** Run `cmake` with the following flags:

>`cmake -D BUILD_SHARED_LIBS=OFF ..`

**Step 6:** Run `make`

>`make`

    *Optional*: If your machine has several cores and enough memory, enable
    parallel build by running `make -j<number of threads>` instead of `make`. For
    this to be worthwhile, the machine should have one core and about 2GB of RAM
    available per thread.
