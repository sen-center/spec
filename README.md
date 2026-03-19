# SEN (Structured Environment Notation)

> A proposed standard for **structured, type-safe, and composable configuration**.

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)  
[![Status](https://img.shields.io/badge/status-specification-orange.svg)]()

## The Problem

Software configuration has evolved, but our tools haven't.

For decades, developers have relied on **flat, string-based configuration files** to manage increasingly complex systems. Modern applications now require hierarchical structure, explicit types, and maintainable configuration models.

Existing solutions often force developers to choose between:

- **Simplicity without structure** — `.env`
- **Structure without strong typing** — `YAML`, `JSON`
- **Complexity without clarity** — `HCL`, `TOML`

As systems scale, configuration becomes harder to reason about, validate, and maintain.

## The SEN Solution

**SEN (Structured Environment Notation)** introduces a configuration language designed specifically for modern runtime environments.

It provides a formal contract between software and its environment.

Key principles:

- **Structured Configuration**  
  Hierarchical grouping replaces flat namespaces.

- **Type Safety**  
  Native support for strings, numbers, booleans, arrays, and null.

- **Composability**  
  Configuration can be split across multiple files and merged cleanly.

- **Clarity**  
  A human-readable syntax designed for maintainability.

## Quick Example

```sen
app: {
    name: "Example Service"
    version: "1.0"
    debug: false
}

server: {
    host: "0.0.0.0"
    port: 8080
}
```

SEN replaces flat environment variables like:

```
APP_NAME=Example Service
APP_VERSION=1.0
APP_DEBUG=false
SERVER_HOST=0.0.0.0
SERVER_PORT=8080
```

with a **structured and typed configuration model**.

## Examples

Configuration examples of increasing complexity:

- Basic configuration  
  `examples/01-basic.sen`

- Intermediate structured configuration  
  `examples/02-intermediate.sen`

- Production‑grade application configuration  
  `examples/03-production.sen`

## Specification

The official specification is currently under active development.

Core documents:

- `spec/00-scope.md`
- `spec/01-concepts.md`
- `spec/02-syntax.md`
- `spec/03-functions.md`

Current status:

- **Stage:** Draft / Request for Comments (RFC)
- **Target version:** v0.1.0

## Vision

SEN aims to become a foundational configuration standard for modern software systems.

Potential integrations include:

- application runtimes
- package managers
- container platforms
- cloud orchestration systems
- framework configuration layers

The long-term goal is to provide a **portable, structured, and type-safe configuration layer** across ecosystems.

## License

Apache License 2.0 — see `LICENSE`. 

Copyright © 2026 The SEN Authors.