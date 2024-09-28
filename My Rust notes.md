- Resources 
  - https://dieterplex.github.io/rust-ebookshelf/
  - https://www.rust-lang.org/fr/learn
  - https://jimskapt.github.io/rust-book-fr/
  - https://github.com/rust-lang/rustlings/
  - https://practice.course.rs/ownership/ownership.html


- Basic DataType 
  - boolean
  - u32
  - i32
  - string slice "&str"
  - string "String"
  - array 
  - tupple ( A empty tupple () is a special unittype )

- Type alias 
  
- Variable, Const, Static 
  - let or let mut
  - const are inlined 
  - static use memory   

- Function 
```
  fn FUNCTION_NAME(PARAMS) -> RESULT
    BODY
```
  - by default RESULT is a empty tupple    
  - use return keyword to direct exit 


- Control Flow
  - if/else 
  - loop
  - while
  - for

- Comments
  - Line comment //
  - Bloc comment /* */

- Memory Management Strategies
  - Rust use OBRM (Ownership Based Resource Management)
  - ownership ! 
    - onlyone
    - auto move ownership
    - Box, Rc, .... 

- Ownership (No mem leak, no dble free, no use after free)
  - Each value belong to a variable called its owner
  - Only one owner at a time
  - When the owner goes out of scope, value is dropped 

- Borrowing (&xxx)
  - just take a ref to a var w/o taking ownership  
    ex: a fct can borrow a var !
  - Two Rules:
    1. Only one mutable ref **OR** Many unmutable ref
    2. Ref must always be valid (no dangling ref)

- Slices ( slices are ref to a contiguous sequence of elements in a collection)  
  ex. part of a string ...
