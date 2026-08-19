# 03. Functions

Functions are the only mechanism used to derive new values in SEN.

All operations such as string concatenation, array manipulation, and object merging are expressed through function calls.

SEN intentionally avoids operators and special expression syntax in order to keep the language simple, predictable, and easy to parse.

## 3.1 Function Call Syntax

A function call appears as a value assigned to a key.

Example:

```
url: concat(
    base
    "/v1"
)
```

General form:

```
key: function_name(
    argument_1
    argument_2
    ...
)
```

Rules:

- Function names follow the identifier pattern:

```
[a-zA-Z_][a-zA-Z0-9_]*
```

- Function names are case-insensitive.
- Arguments are written one per line.
- Commas are not used between arguments.
- The closing parenthesis must appear on its own line.

Example:

```
path: concat(
    base
    "/api"
)
```

## 3.2 Argument Types

Function arguments may be any valid SEN value.

Allowed argument types:

- literal values (string, number, boolean, null)
- key references
- arrays
- objects
- other function calls

Example:

```
url: concat(
    base
    "/v1"
)

ports: append(
    base_ports
    [
        8080
        8443
    ]
)

config: merge(
    defaults
    {
        port: 8443
    }
)
```

## 3.3 Key References

A bare identifier used as a value refers to another key.

Example:

```
base: "https://api.example.com"

url: concat(
    base
    "/v1"
)
```

In this example, `base` refers to the value of the key named `base`.

The evaluation rules for resolving references are defined in the evaluation model.

## 3.4 Built-in Functions (v0.1)

SEN v0.1 defines the following built-in functions.

### 3.4.1 concat

Concatenates multiple string values into a single string.

Type signature:

```
concat(string...) -> string
```

Example:

```
url: concat(
    base
    "/v1"
)
```

### 3.4.2 append

Appends elements to an array.

Type signature:

```
append(array<T>, array<T>) -> array<T>
```

Example:

```
allowed_ips: append(
    base_ips
    [
        "10.0.0.1"
        "10.0.0.2"
    ]
)
```

### 3.4.3 merge

Performs a deep merge of two objects.

When keys conflict, values from the second object override values from the first object.

Type signature:

```
merge(object, object) -> object
```

Example:

```
config: merge(
    defaults
    {
        port: 8443
        ssl: true
    }
)
```

## 3.5 Operators

SEN does not support infix operators such as:

```
+
.
&&
||
```

All operations must be expressed using function calls.

For example, string concatenation must be written using `concat`.

Valid:

```
name: concat(
    first
    " "
    last
)
```

Invalid:

```
name: first + last
name: first . last
name: "{first} {last}"
```

## 3.6 Future Functions

Additional built-in functions may be introduced in future versions of SEN.

Examples include:

- default
- required
- env