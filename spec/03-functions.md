# 03. Functions

Functions are the only mechanism for operations and value construction.

### Syntax
```
key: funcname(
    arg1
    arg2
    ...
)
```

Arguments are one-per-line, no commas.

### Built-in Functions (v0.1)

**concat** — string concatenation
```
url: concat(
    base
    "/v1"
)
```

**append** — array append
```
allowed: append(
    base_list
    [
        "10.0.0.1"
        "10.0.0.2"
    ]
)
```

**merge** — deep object merge (right wins)
```
config: merge(
    defaults
    {
        port: 8443
        ssl: true
    }
)
```

No infix operators (`+`, `.`, `<<`, etc.) are supported.

Additional functions (`default`, `required`, `env`, `if`, ...) are planned for future versions.