### Resources 
  - https://dieterplex.github.io/rust-ebookshelf/
  - https://www.rust-lang.org/fr/learn
  - https://jimskapt.github.io/rust-book-fr/
  - https://github.com/rust-lang/rustlings/
  - https://practice.course.rs/ownership/ownership.html


### Rust Basics

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

- String and str
  - string are coded in UTF-8
  - string literals are string slice stored in the code seq. (app binary exe)
  - operators and macro: + , concat
  - use crate unicode_segmentation 

- Struct {}  
  - method self, &self, & mut self
  - static method w/o self  Struct::StaticFctName
  - Tuples Struct == Struct w/o field names
  - unit-like Struct == Struct w/o field (can be use to impl. trait )

- Enums
  - ....

- Matching (swith case)  match XXXX { value1 => code, } 
  - fffff

- Option<T>  and Result<T,E> 
  - Rust convert auto. Result.Ok() into  Option

- Verctor 
  - into_iter(), iter() , iter_mut() ,   


### Rust Projects
- convention main.rs, lib.rs, ...
- cargo run --bin bin_packages_name
- modules, sub-modules  ( do not follow file struct !)
- cargo modules structure ; cargo modules structure
- use std::time::SystemTime;  
- mod and use 
  - the mod statement define sub-modules  
  - the use statement add shortcut to fully qualifiednames and 
  - the pub use re-export ....

- Crates.io 
  - no delete 
  - yanking 

- Conditionnal Code and Optional Features
  - Cargo.toml [dependencies] and [features]
  - #[cfg(feature="test")] 


- Cargo.toml [workspace]
  - aka monorepo ? 

- Test : Unit Test, Integration Test
  - Doc code block are executed by cargo run !!!! cargo doc --open


### Generics (Monomorphization)
  - In Struct,Enum definition and impl.
  - In free function 
  - Associated Types

### Traits (aka Interfaces in Delphi, Allow Polymorphisme)
  - define trait Xxx {} 
  - impl. Xxx . 
  - default trait implementation
  - Trait Bounds 
    - using fnName<T:TraitName>(x:T)
    - using fnName<T>(x: &impl TraitName)
    - using fnName<T>(x:T) where T: TraitName ....
  - Super Traits
  - Static and Dynamic Dispatch 
    If compiler can NOT known the concrete type, ....
  - Deriving traits ex: #[derive(Debug)]
  - orphan rule == trait coherence
    - work around using WrapperType(InnerType)   

### LifeTime
  - Concrete LifeTimes 
    - Scope LifeTimes 
    - Lexical LifeTimes 
  - Generic LifeTimes  == LifeTime annotation 
    - fn fnName<'a>  
    - struct structName<'a>
    - LifeTime Elison 3 rules
      1. Each parameter that is a reference gets its own lifetime parameter.
      2. If there is exactly one input lifetime parameter, that lifetime
         is assigned to all output lifetime parameters.
      3. If there are multiple input lifetime parameters, but one of them is
         &self or &mut self, the lifetime of self is assigned to all output lifetime parameters.       
  - Static LifeTime
   
### Box Smart Pointer, Rc Smart Pointer, RefCell Smart Pointer 
  - Kind of shared ownership 
  - Box Smart Pointer
  - Rc Smart Pointer ONLY INMUTABLE ! Try to avoid :)
  - RefCell Smart Pointer  inside Rc to remove INMUTABLILITY
  - Deref/DerefMut Coercion trait

### Errors
  - panic! macro
  - enum Result
  - question mark operator == unwrap or panic

### Combinators
  - map
  - and_then
  
### Errors Handling, Logging
  - use crate log, env_logger
  - use crate thiserror, anyhow
  - use crate error-stack

### Closures, Function Pointer (Anonymous Fctions)
  - Fn - Immutably borrow variables in environment.
  - FnMut - Mutably borrow variables in environment. Can change environment.  
    using the **move** keyword 
  - FnOnce - Take ownership of variables in environment. Can only be called once.
  - Function Pointer **(Fn)** == concrete type == fn(x)->y

### Iterator, Combinators
  - Trait next
  - Trait into_iter
  - Method **.iter()**, .iter_mut(), .into_iter() 
    - in &scores >>>> .iter() 
    - in &mut scores >>>> .iter_mut() 
    - in scores >>>> .into_iter() 

  - **Combinators** are pure function that execute specific task 
    - map, filtermap, ... 
    - flatten
    - collect 
    - ....
    
### Turbo Fish synctax ???
  - ????

### Threads
  - use std::thread;
    - sleep 
  - use std::sync::mpsc::{self, Sender}; 
    - Multi-producer, single-consumer 
    - FIFO queue communication primitives
  - use Mutex
  - use Arc to share (Atomic Ref Cnted) ...
  - Send and Sync Traits 
  - async and await  
    - async function simple function returning a Future<> similar to js promise
  - tokio, tokio task 
    - cooperative scheduler
  - async fn should **NOT** be CPU intensive
    or use spawn_blocking !!!!
  - stream ~= async serie of values ~= async iterator 

### Macro
  - What is  macros
    - aka Syntax extensions
    - aka way if writing code that writes code
    - ake metaprogramming
    - aka compile time process 
  - Lexical Analysis -> convert code into 

