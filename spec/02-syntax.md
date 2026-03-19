# 02. Syntax

> **Source Encoding:**  
> SEN source files **MUST** be encoded in UTF‑8 without BOM.

## 2.1 Lexical Rules

- File extension: `.sen`
- The source text is a sequence of Unicode code points
- Statements are terminated by a newline (`LF` or `CRLF`)
- Whitespace characters (space or tab) are used to separate tokens
- Whitespace has no semantic meaning except for newline termination
- Indentation is ignored (cosmetic only)
- No commas (`,`) or semicolons (`;`) are used anywhere

## 2.2 Comments

SEN supports both single-line and block comments.

### 2.2.1 Single-line Comments

Two single-line comment styles are allowed:

```
# comment
// comment
```

A single-line comment continues until the end of the current line.

Examples:

```
# full line comment
// full line comment

key: value  # inline comment
key: value  // inline comment
```

### 2.2.2 Block Comments

Block comments allow commenting multiple lines.

Syntax:

```
/*
    comment
    multiple
    lines
*/
```

Rules:

- Block comments may span multiple lines.
- Block comments may appear anywhere whitespace is allowed.
- Block comments do not nest.

Example:

```
/*
    Example configuration
    for development
*/
port: 8080
```

## 2.3 Keys

- Key pattern: `[a-zA-Z_][a-zA-Z0-9_]*`
- Keys are case-insensitive
- During parsing, all keys are normalized to lowercase
- It is recommended to always write keys in lowercase

### 2.3.1 Nested Keys (Dot Notation)

Keys may use dot notation to define nested objects.

Dot notation expansion occurs before duplicate key resolution.

Example:

```
db.connection.timeout: 5
```

Is equivalent to:

```
db: {
    connection: {
        timeout: 5
    }
}
```

### 2.3.2 Duplicate Keys

If a key appears multiple times within the same object, the last occurrence
overrides the previous value.

Implementations SHOULD emit a warning when this occurs.

Example:

```
port: 8080
port: 9090
```

Result:

```
port = 9090
```

## 2.4 Data Types

### 2.4.1 Primitive Types
| Type    | Syntax                     | Notes |
|-------- |----------------------------|-------|
| String  | `"..."`                    | Must be quoted, JSON escape sequences supported |
| Integer | `42`, `-17`, `0`           | No leading zeros except for zero |
| Float   | `3.14`, `-0.01`, `0.5`     | Must match `[0-9]+ "." [0-9]+` |
| Boolean | `true`, `false`            | Case-insensitive |
| Null    | `null`                     | Case-insensitive |

### 2.4.2 Notes

- Bare strings are not allowed  
  (except for the keywords `true`, `false`, and `null`)
- Floating-point numbers:
  - `.5` is **invalid**
  - `5.` is **invalid**
- Boolean and null values are parsed case-insensitively, but the canonical
  form is lowercase. Implementations MAY emit warnings for non-canonical forms
  (e.g. `TRUE`, `False`, `NULL`).

### 2.4.3 Type Stability

If a key is overridden, the value type MUST remain the same.

Example (invalid):

```
port: 8080
port: "8080"
```

This MUST produce a parsing error.


## 2.5 Structures

SEN supports two composite structures: **objects** and **arrays**.

Only one value or key–value pair is allowed per line.

### 2.5.1 Object

```
server: {
    host: "localhost"
    port: 8080
    debug: true
}
```

### 2.5.2 Array

```
ips: [
    "127.0.0.1"
    "192.168.1.1"
    "10.0.0.1"
]
```

### 2.5.3 Array Type Consistency

All elements of an array MUST have the same type.

For object elements, only the top-level type is enforced; object shape
consistency is not required at this stage.

Example (valid):

```
ports: [
    80
    443
]
```

Example (invalid):

```
values: [
    1
    "two"
]
```

### 2.5.4 Structure Rules

- Exactly one value or key–value pair per line
- Single-line object or array syntax is forbidden
- Nested structures must follow the same rules recursively