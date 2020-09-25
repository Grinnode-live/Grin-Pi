# Pi-Grin
Pi-Grin is a standalone [Grin](https://github.com/mimblewimble/grin) node which can be built by anyone on the Raspberry Pi.

![RPI-4-Grin-Node-PoC](https://aws1.discourse-cdn.com/standard10/uploads/grin/optimized/2X/9/9b6b4826f21743d676d6f0803ea8c64c15466d66_2_499x375.jpeg)

## Parts List

  * Raspberry Pi 4 Model B 8GB RAM (RPI4)
  * 3.5" Screen for RPI4
  * Case for RPI4 + fan
  * Active fan with heatsink for the RPI4 (*Important!*)

## Installation

*Disclaimer: Basic setup for the RPI4, display, SSH, etc. are not shown here.*

  * Install RUST using https://rustup.rs/
  * Dependencies:

    git ● tor ● clang ● ncurses and libs (ncurses, ncursesw5) ● zlib libs (zlib1g-dev or zlib-devel) ● pkg-config ● libssl-dev ● llvm ● linux-headers (needed on Alpine linux)

For Debian-based distributions (Ubuntu, Mint, etc.):

    apt install build-essential git tor cmake git libgit2-dev clang libncurses5-dev libncursesw5-dev zlib1g-dev pkg-config libssl-dev llvm

  * Clone the official Grin repository: `git clone https://github.com/mimblewimble/grin`
    
  * Compile the latest tag using the following script within the directory of the grin repo.

`compile-grin-node.sh`

```sh
#!/bin/bash
/usr/bin/git checkout master
/usr/bin/git fetch --tags
latestTag=$(git describe --tags `git rev-list --tags --max-count=1`)
/usr/bin/git checkout $latestTag
echo $latestTag
~/.cargo/bin/cargo clean
~/.cargo/bin/cargo build --release
```
  * setup `grin-server.toml` to use TUI

```toml
# whether to run the ncurses TUI (Ncurses must be installed)
run_tui = true
```

To see the TUI on your 3.5" screen, add the following to your `.bashrc` file:

```bash
[[ $(/usr/bin/tty) == "/dev/tty1" ]] && exec /usr/bin/screen -S display
```

Now, SSH into your RPI4, connect to your screen session, and run the `grin` binary in `target/release/`. You should see the TUI on your 3.5" display.

## Pictures of the Build Process

![RPI4-Grinnodelive-Poc](https://aws1.discourse-cdn.com/standard10/uploads/grin/optimized/2X/2/21c1f5a17b0decde0adfef128542d7329a00ed83_2_333x250.jpeg)

![RPI-4-Grin-Node-PoC2](https://aws1.discourse-cdn.com/standard10/uploads/grin/optimized/2X/b/bc32d7aa53f07a8bda76d1974b8bfcccb18473c0_2_333x250.jpeg)

## Thanks
Johndavies24 for his help on ARM compilation.

Paouky for his [build documentation](https://paouky.github.io/docs/getting-started/build/).

## License
*WIP*
