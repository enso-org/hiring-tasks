# Macros (writing a code)

Write a macro `to_angles` by using `macro_rules!`, which will replace every occurence of `[<[ ... ]>]` with `< ... >`.
For example, for the given input:

```rust
to_angles! {
    struct Token [<[T]>] {
        prefix: Option [<[T]>],
        data: String,
        suffix: Option [<[T]>],
    }
}
```

It should produce:

```rust
struct Token<T> {
    prefix: Option<T>,
    data: String,
    suffix: Option<T>,
}
```
