# Borrow Error

Consider the following code:

```rust
use std::collections::HashMap;

pub struct ShapeSystemRegistryEntry {
    instance_count : usize,
}

pub struct ShapeSystemRegistryEntryRef<'t> {
    instance_count : &'t mut usize,
}

pub struct ShapeSystemRegistry {
    shape_system_map : HashMap<usize,ShapeSystemRegistryEntry>,
}

impl ShapeSystemRegistry {
    fn get_mut(&mut self, id:usize) -> Option<ShapeSystemRegistryEntryRef> {
        self.shape_system_map.get_mut(&id).and_then(|t| {
            let instance_count = &mut t.instance_count;
            Some(ShapeSystemRegistryEntryRef {instance_count})
        })
    }

    fn register(&mut self, id:usize) -> ShapeSystemRegistryEntryRef {
        let entry = ShapeSystemRegistryEntry {instance_count:0};
        self.shape_system_map.insert(id,entry);
        self.get_mut(id).unwrap()
    }

    fn get_or_register_mut<T>(&mut self, id:usize) -> ShapeSystemRegistryEntryRef {
        match self.get_mut(id) {
            Some(entry) => entry,
            None        => self.register(id)
        }
    }
}

fn main(){}
```

It does not compile, with `rustc` reporting the following error:

```
error[E0499]: cannot borrow `*self` as mutable more than once at a time
  --> src/main.rs:32:28
   |
29 |     fn get_or_register_mut<T>(&mut self, id:usize) -> ShapeSystemRegistryEntryRef {
   |                               - let's call the lifetime of this reference `'1`
30 |         match self.get_mut(id) {
   |               ---- first mutable borrow occurs here
31 |             Some(entry) => entry,
   |                            ----- returning this value requires that `*self` is borrowed for `'1`
32 |             None        => self.register(id)
   |                            ^^^^ second mutable borrow occurs here
```

Please answer the following questions:

1. Why does this code fail to compile? Please elaborate, taking into consideration the way that the
   Rust type checker works.
2. Is this code theoretically safe? What would be the possible problems if the Rust compiler allowed
   this code?
3. How would you fix the code to make it compile?

