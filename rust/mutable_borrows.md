Consider the following code:

```rust
#[derive(Debug)]
pub struct MyRefCell<T> {
    data:T
}

impl<T> MyRefCell<T> {
    pub fn new(data:T) -> Self {
        Self {data}
    }
    
    pub fn borrow_mut(&self) -> &mut T {
        unsafe {&mut *(&self.data as *const T as *mut T)}
    }
}

fn main() {
    let rc = MyRefCell::new(0);
    println!("{:?}", rc);
    let b1 = rc.borrow_mut();
    let b2 = rc.borrow_mut();
    *b1 += 1;
    *b2 += 1;
    println!("{:?}", rc);
    *b1 += 1;
    *b2 += 1;
    println!("{:?}", rc);
}
```

It compiles and the output is:

```rust
MyRefCell { data: 0 }
MyRefCell { data: 2 }
MyRefCell { data: 4 }
```

Questions:
1. Is this particular code safe? Is there any possibility (options, compiler flags, compiler versions, etc) that this program would produce other result that provided above?
2. Is it safe to use `MyRefCell::borrow_mut` when compiling to a native platform? If not, what bad could happen? Please elaborate.
3. Is it safe to use `MyRefCell::borrow_mut` when compiling to a WASM and running in a browser? If not, what bad could happen? Please elaborate.