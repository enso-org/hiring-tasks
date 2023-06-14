# Zeroable Memory (writing a code)

When is it safe to initialize structs with zeroed memory? For example, are the following code snippets safe/sound? Please elaborate.

```rust
fn main() {
    let a: Option<bool> = unsafe { std::mem::zeroed() };
}
```

```rust
fn main() {
    let a: Vec<usize> = unsafe { std::mem::zeroed() };
}
```

```rust
fn main() {
    let a: std::cell::RefCell<bool> = unsafe { std::mem::zeroed() };
}
```

If the answer is "no", how can we implement a structure `ZOption` that will be safe to be initialized with zeroed memory?
