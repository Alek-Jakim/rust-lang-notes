# Rust Basics

### Importing a function

```rust
//print.rs -> new file that we created inside the src folder

//The "pub" keyword is used at the starting of the declaration so that the function becomes accessible to the outside functions.
pub fn run() {
    println!("Hello from the print.rs file!");
}

//Note: Semicolons ; are required in Rust
```

```rust
//main.rs

//Importing the print file
mod print;

fn main() {
    //Calling the run function from the print file
    print::run();
}
```

---

### Formating

```rust
    // Basic Formating
    println!("{}", 1);

    println!("{} is from {}", "Aleksandar", "Skopje");

    // Positional Arguments
    println!("{0} is from {1} and {0} likes to {2}", "Aleksandar", "Skopje", "play video games");

    // Named Arguments
    println!("{name} likes to play {activity}", name = "John", activity = "football");

    //Placeholder traits
    println!("Binary: {:b} Hex: {:x} Octal: {:o}", 10, 10, 10);

```