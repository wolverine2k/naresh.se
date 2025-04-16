---
title: "Reverse a string in Rust"
date: 2024-05-28
categories: 
  - "technical"
tags: 
  - "code"
  - "reverse"
  - "rust"
  - "string"
---

Rust has been gaining a lot of positive attention in the developer community due to very many positive things. You can read more on Stackoverflow ([https://stackoverflow.blog/2020/01/20/what-is-rust-and-why-is-it-so-popular/](https://stackoverflow.blog/2020/01/20/what-is-rust-and-why-is-it-so-popular/)) so I will avoid repetition on this blog.

Rust has fantastic support for basic str primitive ([https://doc.rust-lang.org/std/primitive.str.html](https://doc.rust-lang.org/std/primitive.str.html)) but there are typical things that are very hard to get a grip on when one jumps to Rust as a C/C++ developer. I was doing some [exercisim.io](http://exercisim.io) for Rust and came across a nice exercise where a primitive str is passed to a function which is expected to return a Rust String with the contents reversed i.e. drawer as an input is reversed into reward as an out.

Exercism has quite a few test cases with widechar strings as well. I went through quite some resources but couldn't find a simple way to use str with widechar. So I used the following solution:

```
pub fn reverse(input: &str) -> String {
    let mut input_vec: Vec<u16> = input.encode_utf16().collect();
    let mut output_vec: Vec<u16> = Vec::new();

    while input_vec.len() != 0 {
        output_vec.push(input_vec.pop().unwrap());
    }
    
    return String::from_utf16(&output_vec).expect("Found invalid UTF-16");
}
```

I converted the str into a u16 vector and a while loop poping from one vector and pushing to another (Playground link: https://gist.github.com/rust-play/49a036d0f96c6795756e58b809fa6a8b). I guess another option would be to use a reverse iterator. I am unsure if this is the most optimum way of doing things. I am looking forward to your comments.
