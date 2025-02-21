# Error Handling in Rust: A Practical Guide

Rust provides a robust and safe way to handle errors, making it a powerful language for building reliable applications. Unlike many other languages that rely heavily on exceptions, Rust uses the Result and Option types to handle errors in a more predictable and explicit manner.

The Result Type

The Result<T, E> type is used for functions that can return an error. It has two variants:

Ok(T): Represents a successful computation returning a value of type T.

Err(E): Represents an error, returning an error type E.

Example:

fn divide(a: f64, b: f64) -> Result<f64, String> {
    if b == 0.0 {
        Err("Division by zero".to_string())
    } else {
        Ok(a / b)
    }
}

fn main() {
    match divide(10.0, 2.0) {
        Ok(result) => println!("Result: {}", result),
        Err(e) => println!("Error: {}", e),
    }
}

Return Value:

divide(10.0, 2.0) → Ok(5.0)

Output: Result: 5.0

If b == 0.0, it would return Err("Division by zero") instead.

The Option Type

The Option<T> type is used when a value may or may not be present.

Some(T): Contains a value of type T.

None: Represents an absence of a value.

Example:

fn find_value(arr: &[i32], target: i32) -> Option<usize> {
    arr.iter().position(|&x| x == target)
}

fn main() {
    let numbers = [1, 2, 3, 4, 5];
    match find_value(&numbers, 3) {
        Some(index) => println!("Found at index: {}", index),
        None => println!("Not found"),
    }
}

Return Value:

find_value(&[1, 2, 3, 4, 5], 3) → Some(2)

Output: Found at index: 2

If the target number does not exist in the array, it would return None.

Error Propagation with ?

The ? operator allows propagating errors in functions that return Result or Option.

Example:

use std::fs::File;
use std::io::{self, Read};

fn read_file(path: &str) -> io::Result<String> {
    let mut file = File::open(path)?;
    let mut contents = String::new();
    file.read_to_string(&mut contents)?;
    Ok(contents)
}

fn main() {
    match read_file("example.txt") {
        Ok(data) => println!("File content: {}", data),
        Err(e) => println!("Failed to read file: {}", e),
    }
}

Return Value:

If example.txt exists and contains "Hello, Rust!", the function returns Ok("Hello, Rust!").

If the file does not exist, it returns an Err with an io::Error.

Possible error message: Failed to read file: No such file or directory (os error 2)

Custom Error Types

For complex applications, defining custom error types using thiserror or anyhow can improve error handling.

Example:

use thiserror::Error;

#[derive(Debug, Error)]
enum MyError {
    #[error("Invalid input: {0}")]
    InvalidInput(String),
    #[error("IO error: {0}")]
    IoError(#[from] std::io::Error),
}

fn example_function() -> Result<(), MyError> {
    Err(MyError::InvalidInput("Bad data".to_string()))
}

fn main() {
    if let Err(e) = example_function() {
        println!("Error occurred: {}", e);
    }
}

Return Value:

example_function() → Err(MyError::InvalidInput("Bad data".to_string()))

Output: Error occurred: Invalid input: Bad data

Conclusion

Rust’s approach to error handling ensures safety and clarity. By using Result, Option, the ? operator, and custom error types, developers can write robust and maintainable code. Understanding these patterns is essential for building reliable Rust applications.
