---
author:
  - Samuel Dalton Walker
tags:
  - 2025-03-05
---
``
# Heading 1 
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat *metus*, a fermentum mauris. Vivamus pharetra sollicitudin elit non mattis. Donec metus libero, sollicitudin vel eros id, porttitor dignissim neque. Vivamus euismod nisl ac pellentesque elementum. Quisque gravida accumsan ante sed tristique. Proin in neque eu odio feugiat malesuada. Mauris a rhoncus velit, sit amet tempor est. Nam in volutpat lorem, vel lacinia sapien. Vivamus iaculis libero risus. Pellentesque habitant *morbi* tristique senectus et netus et malesuada fames ac turpis egestas. Vestibulum et risus rutrum, aliquet tellus vel, posuere risus.
## Heading 2
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris.
### Heading 3
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris.
#### Heading 4
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris.
##### Heading 5
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris.
###### Heading 6
Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris.

## Mathematics

$$f(x) \approx \frac{a_0}{2} + \sum_{n=1}^{\infty} \left( a_n \cos(nx) + b_n \sin(nx) \right)$$
$$a_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \cos(nx) \,dx$$
$$b_n = \frac{1}{\pi} \int_{-\pi}^{\pi} f(x) \sin(nx) \,dx$$

## Code

```rust
// main.rs - A comprehensive Rust syntax highlighting test

/*
 * This is a block comment that can span
 * multiple lines. It's often used for longer explanations.
 */

// Import necessary items from the standard library
use std::collections::HashMap;
use std::fmt::{Debug, Display};

// A constant value, known at compile time
const PI: f64 = 3.14159265359;

// A static variable, which has a fixed memory location
static mut COUNTER: u32 = 0;

/// A struct with named fields and a lifetime parameter.
#[derive(Debug, Clone)]
pub struct User<'a> {
    username: &'a str,
    id: u64,
    is_active: bool,
}

// An enumeration with different variants
enum Message {
    Quit,
    Write(String),
    Move { x: i32, y: i32 },
}

// A trait defining a shared behavior
trait Summarizable {
    fn summary(&self) -> String;
}

// Implement the trait for our User struct
impl<'a> Summarizable for User<'a> {
    fn summary(&self) -> String {
        // Using a macro to format a string
        format!("User {} (ID: {})", self.username, self.id)
    }
}

// A generic function that works with any type that implements Display
fn print_item<T: Display>(item: T) {
    println!("Item: {}", item);
}

/// The main entry point of the program.
/// This is an asynchronous function.
#[tokio::main]
async fn main() {
    let name = "Rustacean";
    let mut user = User {
        username: name,
        id: 101,
        is_active: true,
    };

    println!("Welcome, {}!", user.username);

    // Using a match statement on an enum
    let msg = Message::Move { x: 10, y: -5 };
    match msg {
        Message::Quit => println!("Quitting..."),
        Message::Write(text) => println!("Text: {}", text),
        Message::Move { x, y } => {
            println!("Moving to ({}, {})", x, y);
        }
    }

    // A simple loop
    for i in 0..=3 {
        print_item(i);
    }

    // Working with a HashMap
    let mut scores = HashMap::new();
    scores.insert(String::from("Blue"), 10);

    // Raw string literal
    let raw_string = r#"This is a raw string. \n escapes are not processed."#;
    println!("{}", raw_string);

    // A character literal
    let heart: char = '❤️';

    // Call an async function
    another_task().await;
}

// Another asynchronous function
async fn another_task() {
    println!("This is running in another task.");
}
```

## Miscellaneous
---
> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris. Vivamus pharetra sollicitudin elit non mattis. Donec metus libero, sollicitudin vel eros id, porttitor dignissim neque.

%% Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris. Vivamus pharetra sollicitudin elit non mattis. Donec metus libero, sollicitudin vel eros id, porttitor dignissim neque. %%


> [!NOTE] Callout
> Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris. Vivamus pharetra sollicitudin elit non mattis. Donec metus libero, sollicitudin vel eros id, porttitor dignissim neque.

> [!CAUTION] CAUTION
> Contents

> [!IMPORTANT] IMPORTANT
> asdasdasd

> [!WARNING] WARNING TEST
> TEST TEST TEST

> [!TIP] TIP
> asdas

==Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla.== 

~~Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla.~~

**Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus.** 
*Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla.* 
- Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris. Vivamus pharetra sollicitudin elit non mattis. Donec metus libero, sollicitudin vel eros id, porttitor dignissim neque.
1. Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut eget auctor felis, id tempus risus. Pellentesque pellentesque, risus vitae egestas consequat, nibh nisi interdum dolor, ac blandit nulla purus ut nulla. Praesent ut leo lobortis, consectetur felis vitae, venenatis metus. Ut vitae feugiat metus, a fermentum mauris. Vivamus pharetra sollicitudin elit non mattis. Donec metus libero, sollicitudin vel eros id, porttitor dignissim neque.
[[Obsidian Test File]]
