# Rpi starter template

Contains the correct linker setup and a Cargo Makefile that builds and transfers the
cross compiled program to the Raspberry pi. Follow the instructions to cross compile.

### Important

You'll need to point the path in ./.cargo/config.toml:

```toml
[target.armv7-unknown-linux-gnueabihf]
linker = "path/to/the/linker/you/downloaded
```

## Usage

Develop the files in WSL. Change the environment variables in `Makefile.toml` they're
correct for the project and the raspberry pi.

Build the program using one of the commands:
```
cargo make debug
cargo make release
```

Log on to the Rpi and run the program.

## On the Rpi

1. Start the pi and set a password
2. Enable SSH:

```
sudo raspi-config
> Interfacing Options
  > SSH
    > Enable
```

3. Find the IP:

```
ifconfig | grep -Eo 'inet (addr:)?([0-9]*\.){3}[0-9]*' | grep -Eo '([0-9]*\.){3}[0-9]*' | grep -v '127.0.0.1'
```

4. Confirm additional information

```
whoami > returns "pi"
hostname > returns "raspberrypi"
```


## From scratch in WSL
Install rustup and Rust.

1. Install the correct target `rustup target add armv7-unknown-linux-gnueabihf`
2. Install the [linker](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-a/downloads)
3. Add path to extracted toolchain to ".bashrc": `export PATH="$HOME/PATH_TO_YOUR_DOWNLOAD/PATH_TO_TOOLCHAIN_FOLDER/bin:$PATH"`
4. Install sshpass `sudo apt install sshpass`
5. Install cargo make `cargo install cargo-make`
