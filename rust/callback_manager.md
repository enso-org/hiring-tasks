Please define a CallbackManager struct which will have two public methods – `add` and
`run_all`:
- The `add` method should accept any closure without arguments and should return some
kind of a handle to it.
- The `run_all` method should not consume any arguments and should run all registered
callbacks iff their handles still exist. If a handle was dropped, the registry should be cleaned
on the beginning of the `run_all` method logic.
- The `CallbackRegistry` should be a polymorphic structure parametrized with information about the
shape of the closures. For example, you should be able to create `CallbackManager` accepting
closures of type `FnMut(i32)` and then you should be able to fire them by a call to `run_all(7)`
(each closure will be fired with `7` as the argument).
