# 02. Syntax

## 2.1 Lexical Rules
- File encoding: **UTF-8**
- File extension: `.sen`
- Tokens separated by one or more whitespace (space/tab)
- Statements terminated by newline (LF or CRLF)
- Indentation: ignored (cosmetic only)
- No commas, no semicolons anywhere

## 2.2 Comments
Single-line only:
```
# full line comment
key: value  # inline comment
```

No block comments.

## 2.3 Keys
- Pattern: `[a-zA-Z_][a-zA-Z0-9_]*`
- Case-insensitive (internally normalized to lowercase)
- Recommendation: always write in lowercase

## 2.4 Data Types

| Type     | Syntax                              | Notes |
|----------|-------------------------------------|-------|
| String   | `"..."`                             | Must be quoted, JSON escapes supported |
| Integer  | `42`, `-17`, `0`                    | No leading zeros except for zero |
| Float    | `3.14`, `-0.01`, `0.5`              | Must start with digit (`.5` forbidden) |
| Boolean  | `true` / `false`                    | Case-insensitive |
| Null     | `null`                              | Case-insensitive |

No bare strings allowed (except `true`/`false`/`null`).

SEN is dynamically typed. Implementations **should** emit warnings on type changes for the same key (e.g. number → string).

## 2.5 Structures (One-value-per-line only)

**Object**
```
server: {
    host: "localhost"
    port: 8080
    debug: true
}
```

**Array**
```
ips: [
    "127.0.0.1"
    "192.168.1.1"
    "10.0.0.1"
]
```

Rules:
- One value/pair per line
- Single-line syntax forbidden
- Nested structures follow same rule