---
title: "Rust"
date: 2020-02-21T10:08:27+08:00
draft: true
---

### Traits

* 

### Modules
* `mod`类似`clojure`的`require ns`
* `use utils::{say_hello, say_goodbye};`类似`clojure`的`use ns`

### Crates
* Rust2018中可以省略`extern crate xxxx`
* `regex` 正则包
* `lazy_static` 惰性静态，可定义静态`HashMap`等不方便直接定义的变量


### Macros


* `#[macro_export]` can be used when be imported
* macro types
    * `macro_rules!` like a match (`declarative macros`)
    * `procedural macros` like a function
        * `custom derive`, process ast, only for `struct` `enum`
            * `#[proc_macro_derive(HelloMacro)]`
        * `attribute-like`,more param, can be used in `fn`etc. 
            * `#[proc_macro_attribute]`
        * `function-like`,not like a match, process ast
            * `#[proc_macro]`
* `!`代表宏调用
* `foo()?`代表`try!`宏

```rust
// custom derive
fn impl_hello_macro(ast: &syn::DeriveInput) -> TokenStream {
    let name = &ast.ident;
    let gen = quote! {
        impl HelloMacro for #name {
            fn hello_macro() {
                println!("Hello, Macro! My name is {}", stringify!(#name));
            }
        }
    };
    gen.into()
}
```
    
### 编程之道的知识树

![toc](/rust/toc.png)
