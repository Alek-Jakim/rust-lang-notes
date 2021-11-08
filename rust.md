# Rust

## Installation

- On macOS and Linux:

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```


## Initialize cargo projects

```bash
cargo init
```

## Hello World

 The main function is special: it is always the first code that runs in every executable Rust program. The first line declares a function named main that has no parameters and returns nothing.

```rust
fn main() {
    println!("Hello, world!");
}
```

## Cargo

Cargo is Rust’s build system and package manager. 

```bash
# Check cargo version
cargo --version

# Creating a project with cargo
cargo new hello_cargo
```

The Cargo.toml file is in the TOML (Tom’s Obvious, Minimal Language) format, which is Cargo’s configuration format.


### Building and Running a Cargo Project

From your main directory, build your project by entering the following command:

```bash
cargo build
```

This command creates an executable file in target/debug/hello_cargo (or target\debug\hello_cargo.exe on Windows) rather than in your current directory. You can run the executable with this command:

```bash
./target/debug/hello_cargo # or .\target\debug\hello_cargo.exe on Windows

# If all goes well, Hello, world! should print to the terminal. 
```

We just built a project with cargo build and ran it with ./target/debug/hello_cargo, but we can also use cargo run to compile the code and then run the resulting executable all in one command:

```bash
cargo run
```

Cargo also provides a command called cargo check. This command quickly checks your code to make sure it compiles but doesn’t produce an executable:


```bash
cargo check
```

### Building for release


When your project is finally ready for release, you can use `cargo build --release` to compile it with optimizations. This command will create an executable in target/release instead of target/debug.

---
## Topics

## [Printing](./print.md)

## [Common Concepts](./common-concepts.md)
