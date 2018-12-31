# Blur Network 

Copyright (c) 2018, Blur Network</br>

*See [LICENSE](LICENSE).*<br>


<h1 id="compile-linux">Compiling from Source on Linux</h1>

**Blur uses the CMake build system and a top-level [Makefile](Makefile) that invokes cmake commands as needed.**

**Step 1:** Clone this repository recursively, to pull in needed submodules:

>`git clone https://github.com/blur-network/blur.git`

**Step 2:** Install dependencies:

Ubuntu 18.04.1 One-Liner:

>`sudo apt-get install -y build-essential cmake pkg-config libboost-all-dev libssl-dev libzmq3-dev libunbound-dev libnorm-dev libpgm-dev libsodium-dev libminiupnpc-dev libunwind8-dev liblzma-dev libreadline6-dev libldns-dev libexpat1-dev libgtest-dev doxygen graphviz`

Debian 9/Ubuntu 16.04 One-Liner:

>`sudo apt-get install -y build-essential cmake pkg-config libboost-all-dev libssl-dev libzmq3-dev libunbound-dev libpgm-dev libsodium-dev libminiupnpc-dev libunwind8-dev liblzma-dev libreadline6-dev libldns-dev libexpat1-dev libgtest-dev doxygen graphviz`

Arch Linux One-Liner:

>`sudo pacman -S base-devel cmake boost openssl zeromq libpgm unbound libsodium libunwind xz readline ldns expat gtest doxygen graphviz`

**Step 3:** `cd` into the the directory where the source code was cloned,  and issue a `make` command. 

>`cd ~/blur && make release-all`

    *Optional*: If your machine has several cores and enough memory, enable
    parallel build by running `make -j<number of threads>` instead of `make`. For
    this to be worthwhile, the machine should have one core and about 2GB of RAM
    available per thread.

*There are multiple platforms and configurations for which you can compile.  A non-exhaustive list can be found below:*

For statically linked binaries (defaults to the platform configuration of the host compiler):
>`make release-static`

For Windows portable binaries (Cross-Compiled on Linux <a href="https://github.com/blur-network/blur/tree/v0.1.7.6/contrib/depends">using contrib/depends system from Bitcoin</a>):

Follow the link above to setup build environment, then issue the command below

>`make release-static-win64`

*It is probably much easier to <a href="https://github.com/blur-network/blur/tree/v0.1.7.6/contrib/depends">use the depends system</a> for a cross-compile on Windows Susbsytem Linux than getting MSYS2 to actually work properly*

For MacOS portable binaries:
>`make release-static-mac-x86_64`

For Linux portable binaries:
>`make release-static-linux-x86_64`

*Note that we do not officially support builds for 32-bit architecture, arm architecture, or the freebsd linux distribution currently. However, there are options within the [Makefile](Makefile) for these configurations.  These configurations (and source files) will need modified (considerably), in order for the resulting binaries to work.  Even if they build, it is unlikely that the network will not identify your node as malicious, upon running a daemon with incorrect code.*

<h1 id="mining-linux">Mining on Linux</h1>

Compile from source, or download the <a href="https://github.com/blur-network/blur/releases"> latest binary release from the Releases page</a>.  

We also now offer a Snap package on the Ubuntu Snap Store: <a href="https://snapcraft.io/blur"><img alt="Get it from the Snap Store" src="https://snapcraft.io/static/images/badges/en/snap-store-black.svg" /></a>

Open a terminal in the directory within which the binaries were downloaded.  Assuming that is your Downloads folder, enter the following command:

>`cd ~/Downloads && tar xvzf blur-v0.1.7.6-linux-x86_64.tar.xz`

Navigate into the directory you just unzipped from the archive, and start the daemon.

>`cd blur-v0.1.7.6-linux_x86_64 && ./blurd`

Wait for sync to complete, open a new tab or terminal window, and then start the wallet:

>`./blur-wallet-cli`

Follow the prompts to setup a new wallet.  When prompted for the password, the CLI will not show a password as you type.  It is recording your keystrokes, however.

Record the information for your wallet.

Once the wallet is open, type into the wallet CLI: `start_mining [# of threads]` where [# of threads] is the amount of cpu threads you wish to dedicate to mining BLUR. 

You should see the message: `Mining started in daemon`

Switch back to the terminal or tab in which your daemon is running, and type `show_hr` for real-time  hashrate monitoring.  For further commands in either the wallet or the daemon, type `help` into either CLI.  Note that the commands for the daemon and wallet are different.

Whenever you find a block, your daemon will show a bold message with the block # found.  There is a slight delay between that message and the balance reflecting in your wallet. 

<h1 id="mining-windows"> Mining on Windows </h1>

Download the <a href="https://github.com/blur-network/blur/releases">latest release from our Releases page</a>.

Open your Downloads Library in your File Explorer.  Extract the executables from the compressed archive, and navigate to the folder that you just extracted. 

Start the daemon by double-clicking the `blurd.exe` file. 

You will see a pop-up from your firewall.  Be sure to check the box next to "Private Networks" if you are on a private network, or your daemon will not be able to sync with the network. If you daemon stalls while syncing, close and restart the program.  You will not lose any blocks you have already synced with. Once your daemon is synced with the network...

Start the wallet by double-clicking the `blur-wallet-cli` file.

Follow the prompts to setup a new wallet.  When prompted for the password, the CLI will not show a password as you type.  It is recording your keystrokes, however.

Once the wallet is open, type into the wallet CLI: `start_mining [# of threads]` where [# of threads] is the amount of cpu threads you wish to dedicate to mining BLUR. . 

You should see the message: `Mining started in daemon`

Switch back to the terminal or tab in which your daemon is running, and type `show_hr` for real-time  hashrate monitoring.  For further commands in either the wallet or the daemon, type `help` into either CLI.  Note that the commands for the daemon and wallet are different.

Whenever you find a block, your daemon will show a bold message with the block # found.  There is a slight delay between that message and the balance reflecting in your wallet. 

<h1 id="sync-issues">How to Fix Synchronizing Issues</h1>

If you cannot synchronize with the network, kill your daemon & restart with the following options:

Linux: `cd` to the directory you downloaded the files into, and type:
`./blurd --add-priority-node 178.128.191.245:13894 --add-priority-node 178.128.186.101:13894 --seed-node 178.128.180.136:13894`

Windows:  Open cmd.exe, `cd` to the directory you downloaded the files into, and type:
`blurd.exe --add-priority-node 178.128.191.245:13894 --add-priority-node 178.128.186.101:13894 --seed-node 178.128.180.136:13894`

This should fix the synchronizing issue if the daemon does not connect to the seed nodes automatically. 

You can also see additional command-line options by running the daemon with the option `--help`.  The program will return a list of startup flags and their descriptions. 

