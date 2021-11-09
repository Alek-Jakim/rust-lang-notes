# Ownership

## **What Is Ownership?**

* All programs have to manage the way they use a computer’s memory while running.

* Rust's approach -> memory is managed through a system of ownership with a set of rules that the compiler checks at compile time. None of the ownership features slow down your program while it’s running.

--- 

## **The stack, the heap, and pointers**

* Both the *stack* and the *heap* are parts of memory that are available to your code to use at runtime, but they are structured in different ways.

### The Stack

* The stack stores values in the order it gets them and removes the values in the opposite order(last in, first out).

* Adding data is called pushing onto the stack, and removing data is called popping off the stack.

* All data stored on the stack must have a known, fixed size.

### The Heap

* Data with an unknown size at compile time or a size that might change must be stored on the heap instead.

* The heap is less organized: when you put data on the heap, you request a certain amount of space.

* The memory allocator finds an empty spot in the heap that is big enough, marks it as being in use, and returns a pointer, which is the address of that location. 

* This process is called allocating on the heap and is sometimes abbreviated as just allocating (pushing values onto the stack is not considered allocating). 

* Because the pointer is a known, fixed size, you can store the pointer on the stack, but when you want the actual data, you must follow the pointer.


### Summary

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

These are all different types, just in the same way that "a friend of a friend" is different from "a friend".

