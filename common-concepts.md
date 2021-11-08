## Common Concepts in Rust


## 1. Guessing Game

```rust
use std::io;
use rand::Rng;
use std::cmp::Ordering;

fn main() {
    println!("Guess the number!");

    println!("Please input your guess");



    //To summarize, the let mut guess = String::new(); line has created a mutable variable that is currently bound to a new, empty instance of a String. Whew!
    let mut guess = String::new();

    let secret_num = rand::thread_rng().gen_range(1..10);

    //If we hadn’t put the use std::io line at the beginning of the program, we could have written this function call as std::io::stdin. The stdin function returns an instance of std::io::Stdin, which is a type that represents a handle to the standard input for your terminal.
    io::stdin()
        .read_line(&mut guess)
        .expect("Failed to read line");

    let guess: u32 = guess.trim().parse().expect("Please type a number!");

    println!("You guessed {}", guess);

    
    match guess.cmp(&secret_num) {
        Ordering::Less => println!("Too small! The secret number was {}", secret_num),
        Ordering::Greater => println!("Too big! The secret number was {}", secret_num),
        Ordering::Equal => println!("You win! The secret number was {}", secret_num),
    }
}
```

---

## 2. Variables and Mutability

* By default variables are immutable.

* When a variable is immutable, once a value is bound to a name, you can’t change that value.

* You can make variables mutable by adding `mut` in front of the variable name.

* In cases where you’re using large data structures, mutating an instance in place may be faster than copying and returning newly allocated instances. With smaller data structures, creating new instances and writing in a more functional programming style may be easier to think through.


### **Differences Between Variables and Constants**

* First, you aren’t allowed to use `mut` with constants. Constants aren’t just immutable by default—they’re always immutable.

* You declare constants using the `const` keyword instead of the `let` keyword, and the type of the value **must** be annotated. 

* Constants can be declared in any scope, including the global scope - useful for values that many parts of code need to know about.

* The last difference is that constants may be set only to a constant expression, not the result of a value that could only be computed at runtime.

```rust
// Rust’s naming convention for constants is to use all uppercase with underscores between words.

const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

* Constants are valid for the entire time a program runs, within the scope they were declared in - useful for values in your application domain that multiple parts of the program might need to know about (maximum number of points any player of a game is allowed to earn or the speed of light).


### **Shadowing**

Shadowing --> you can declare a new variable with the same name as a previous variable.

Rustaceans say that the first variable is shadowed by the second, which means that the second variable’s value is what the program sees when the variable is used.

```rust
fn main() {
    let x = 5;

    let x = x + 1;

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {}", x);
        // x is 12
    }

    println!("The value of x is: {}", x);
    // x is 6
}
```

* Shadowing is different from marking a variable as `mut`, because we’ll get a compile-time error if we accidentally try to reassign to this variable without using the `let` keyword.

The other difference between mut and shadowing is that because we’re effectively creating a new variable when we use the let keyword again, we can change the type of the value but reuse the same name:

```rust
//Shadowing thus spares us from having to come up with different names, such as spaces_str and spaces_num; instead, we can reuse the simpler spaces name. 

let spaces = "   ";
let spaces = spaces.len();
```

---

## **3. Data Types**