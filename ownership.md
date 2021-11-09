# Ownership

## **What Is Ownership?**

* All programs have to manage the way they use a computer’s memory while running.

* Rust's approach -> memory is managed through a system of ownership with a set of rules that the compiler checks at compile time. None of the ownership features slow down your program while it’s running.

--- 

## **The stack, the heap, and pointers**

The stack and the heap are two places to keep memory in computers. The important differences are:

* The stack is very fast, but the heap is not so fast. It's not super slow either, but the stack is always faster. But you can't just use the stack all the time, because:

* Rust needs to know the size of a variable at compile time. So simple variables like `i32` go on the stack, because we know their exact size. You always know that an `i32` is going to be 4 bytes, because 32 bits = 4 bytes. So `i32` can always go on the stack.

* But some types don't know the size at compile time. But the stack needs to know the exact size. So what do you do? First you put the data in the heap, because the heap can have any size of data. And then to find it a pointer goes on the stack. This is fine because we always know the size of a pointer. So then the computer first goes to the stack, reads the pointer, and follows it to the heap where the data is.

Pointers are like a table of contents in a book. 

The pointer you usually see in Rust is called a **reference**.

This is the important part to know: **a reference points to the memory of another value.**

A reference means you *borrow* the value, but you don't own it.

In Rust, references have a `&` in front of them.

```rust
// makes a regular variable
let my_variable = 8

// makes a reference.
let my_reference = &my_variable
```

This means that `my_reference` is only looking at the data of `my_variable`. `my_variable` still owns its data.

You can also have a reference to a reference, or any number of references.

```rust
fn main() {
    let my_number = 15; // This is an i32
    let single_reference = &my_number; //  This is a &i32
    let double_reference = &single_reference; // This is a &&i32
    let five_references = &&&&&my_number; // This is a &&&&&i32
}
```