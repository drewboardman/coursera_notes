Monads have 2 operations defined on them, `flatMap` and `unit`

- `flatMap` is more commonly called `bind` in the literature.
- There is also a `unit` functions that takes a value and create a monad from it

```Scala
def unit[T](x: T): M[T]
```

Some examples of monads and their `unit` operations

```Scala
List(x)
Set(x)
Some(x)
```

`map` can be defined on every monad as a combination of `flatMap` and `unit`

```Scala
m.map(f) == m.flatMap (x => unit(f(x)))
         == m.flatMap (f.andThen(unit))
```

To qualify as a monad, a type has to satisfy 3 laws that connect `flatMap` and `unit`:

I. Associativity
- this is really a law about placing parentheses

```Scala
m flatMap f flatMap g == m flatMap (x => f(x) flatMap g)
```

II. Left Unit
- if I inject into the monad using `unit` and then `flatMap`, then the result is the same as just using `f(x)`

```Scala
unit(x).flatMap(f) == f(x)
```

III. Right Unit
- if you `flatMap` a monad with the `unit` constructor, then you end up with the original monad

```Scala
m.flatMap unit == m
```

