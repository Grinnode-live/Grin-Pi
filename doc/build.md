# Building Grin

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
  * Setup `grin-server.toml` to use TUI.

```toml
# whether to run the ncurses TUI (Ncurses must be installed)
run_tui = true
```

 * To see the TUI on your 3.5" screen, add the following to your `.bashrc` file:

```bash
[[ $(/usr/bin/tty) == "/dev/tty1" ]] && exec /usr/bin/screen -S display
```

 * Now, SSH into your RPI4, connect to your screen session, and run the `grin` binary in `target/release/`. You should see the TUI on your 3.5" display.
