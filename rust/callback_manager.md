# Callback Manager

Please define a `CallbackManager` struct which has two public methods – `add` and `run_all`:

- The `CallbackManager` should be a polymorphic structure parametrized with information about the
  shape of the closures. For example, you should be able to create a `CallbackManager` accepting
  closures of type `FnMut(i32)` and then you should be able to fire them by a call to `run_all(7)`
  (each closure will be fired with `7` as the argument).
- The `add` method should accept any unapplied closure of a type matching the shape of the closure
  which `CallbackManager` is parametrized with and should return some kind of a handle to it.
- The `run_all` method should run all registered callbacks and pass provided arguments iff their 
  handles still exist. If a handle was dropped, the callback should be removed from the registry 
  at the beginning of the `run_all` method.
