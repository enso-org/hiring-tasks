# Callback Manager (writing a code)

Please define a `CallbackManager` struct which will allow you to register functions (callbacks) and
fire all of them at the same time. In particular:

- The `CallbackManager` should be a polymorphic structure parametrized with information about the
  shape of the closures. It should support closures of types `Fn(...)` and `FnMut(...)` with 
  arbitrary number of arguments.

- The `CallbackManager::add` method should accept any unapplied closure of a type matching 
  the shape of the closure which `CallbackManager` is parametrized with and should return some kind 
  of a handle to it.

- The `CallbackManager::run_all` method should run all registered callbacks and pass provided arguments 
  iff their handles still exist. If a handle was dropped, the callback should be removed from the registry 
  at the beginning of the `run_all` method call.

Take an extra care about performance and how easy it is to use the API of `CallbackManager`, please.
You can use unstable Rust if you want to.
