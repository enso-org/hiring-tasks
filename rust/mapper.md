# Mapper

Tasks:

1. Define a trait `Mapper` which will contain a `map` method.
2. Create implementation of `Mapper` for `Option<T>` in such a way, that
   `Some(5).map(|t|format!("{}!",t))` returns `Some("5!")`. Map on `None` should return `None`.
3. Create implementation of `Mapper` for `Result<T,E>` in such a way, that
   `Ok(5).map(|t|format!("{}!",t))` returns `Ok("5!")`. Map on `Err(..)` should return the same 
   value.
