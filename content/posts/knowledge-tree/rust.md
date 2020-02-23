---
title: "Rust"
date: 2020-02-21T10:08:27+08:00
draft: true
---


### Modules
* `mod`类似`clojure`的`require ns`
* `use utils::{say_hello, say_goodbye};`类似`clojure`的`use ns`

### Crates
* 


### Macros


* `#[macro_export]` can be used when be imported
* macro types
    * `macro_rules!` like a match (`declarative macros`)
    * `procedural macros` like a function
        * custom derive
        * attribute-like
        * function-like
    * 
* `!`代表宏调用
* `foo()?`代表`try!`宏
    
### 编程之道的知识树

![toc](/rust/toc.png)
