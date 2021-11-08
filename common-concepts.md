## Common Concepts in Rust


## **1. Guessing Game**

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

## **2. Variables and Mutability**

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

* Two data type subsets: **scalar** and **compound**.

* Rust is a *statically typed* language, which means that it must know the types of all variables at compile time

* In cases when many types are possible, such as when converting a `String` to a numeric type using `parse`, we must add a type annotation.

```rust
let guess: u32 = "42".parse().expect("Not a number!");

let guess = "42".parse().expect("Not a number!");
// Error: ^^^^^ consider giving `guess` a type
```

### **Scalar Types**

* A scalar type represents a single value.

* Rust has four primary scalar types: integers, floating-point numbers, Booleans, and characters.

| Length        | Signed           | Unsigned  |
| ------------- |:-------------:| -----:|
| 8-bit      | i8 | u8 |
| 16-bit     | i16      |   u16 |
| 32-bit     | i32     |    $32 |
| 64-bit      | i64 | u64 |
| 128-bit     | i128      |   u128 |
| arch     | isize     |    usize |

* Each variant can be either signed or unsigned and has an explicit size. 

* *Signed* and *unsigned* refer to whether it’s possible for the number to be negative—in other words, whether the number needs to have a sign with it (signed) or whether it will only ever be positive and can therefore be represented without a sign (unsigned). 

* Each signed variant can store numbers from -(2<sup>n</sup> - 1) to 2<sup>n</sup> - 1 - 1 inclusive, where *n* is the number of bits that variant uses.

* Additionally, the `isize` and `usize` types depend on the kind of computer your program is running on: 64 bits if you’re on a 64-bit architecture and 32 bits if you’re on a 32-bit architecture.

* You can write integer literals in any of the forms shown in the table below:

| Number literals        | Example           | 
| ------------- |:-------------:| 
| Decimal      | `98_222` | 
| Hex     | `0xff`      |   
| Octal     | `0o77`     |    
| Binary      | `0b1111_0000` |  
| Byte    | `b'A'`      |    

* How do you know which type of integer to use? If you’re unsure, Rust’s defaults are generally good places to start: integer types default to `i32`.

* The primary situation in which you’d use isize or usize is when indexing some sort of collection.