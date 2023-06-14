Consider the following code:

```rust
/// An empty generic representation of a struct. It represents a struct with no fields.
pub struct Empty;

/// A generic representation of a struct with many fields. For example, a struct can be
/// represented as `Field<usize, Field<String, Empty>>`.
pub struct Field<FirstField, RestOfFields>(pub FirstField, pub RestOfFields);

/// Trait for any structure that can be converted to generic representation.
/// For example, generic representation of `(usize, String)` is `Field<usize, Field<String, Empty>>`.
pub trait HasGenericRepr {
    type GenericRepr;
}

pub type GenericRepr<T> = <T as HasGenericRepr>::GenericRepr;

/// Trait allowing converting any struct to its generic representation.
pub trait IntoGenericRepr: HasGenericRepr {
    fn into_generic_repr(self) -> GenericRepr<Self>;
}
```

Implement the following things:

1. Ability to convert tuples of any types to their generic representation.
2. Method `first_field_ref` which will return the reference to the first field of any generic representation
   and any structure that implements `IntoGenericRepr`. For example, it should be possible to call `(1, "hello").first_field()`,
   and `Field(1, Field("hello", Empty)).first_field()`, which should return `&1`.
3. Method `map` which will allow mapping any function on all fields of a struct and return the struct itself. For example, it
   should be possible to call `(1, "hello").map(...)` with a function `format!("{t}!")` to get `("1!", "hello!")`. How the function
   is passed to the `map` method is up to you (it can be passed as a closure, as a structure representing that function, etc.).
