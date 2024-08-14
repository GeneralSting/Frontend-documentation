# Binding

- `binding` is an association of and indentifier with a value.
  - not all bindings are variables - function parameters and the binding created by the catch (e) block are not "variables" in the strict sense
  - some bindings are implicitly created by the language - `this` and `new.target` in JS
- binding is `mutable` if it can be re-assigned, and `immutable` otherwise; this does not mean that the value it holds is immutable
- binding is often associated with a scope
