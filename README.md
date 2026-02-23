# SEN (Structured Environment Notation)

> A proposed standard for structured, type-safe, and composable configuration.

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Status](https://img.shields.io/badge/status-specification-orange.svg)]()

## The Problem

Software configuration has evolved, but our tools haven't. For too long, developers have relied on flat, unstructured text files to manage complex application environments.

Modern applications demand structure, types, and modularity. Existing solutions often force developers to choose between:
*   **Simplicity without structure** (e.g., `.env`)
*   **Structure without enforced type safety** (e.g., `YAML`, `JSON`)
*   **Complexity without clarity** (e.g., `HCL`, `TOML`)

## The SEN Solution

**SEN** is designed to bridge this gap. It provides a formal contract between software and its environment, offering:

*   **Structure:** Hierarchical grouping of configurations instead of flat namespaces.
*   **Type Safety:** A formal, enforceable type system (strings, numbers, booleans, arrays).
*   **Composition:** Modular configuration across multiple files and overlays.
*   **Clarity:** A human-readable notation designed for clarity and maintainability.

## Vision

The goal of SEN is not just to replace existing formats, but to establish a foundational standard for the next generation of runtime managers, package managers, and cloud-native tools.

## Specification

The official specification is currently under active development.
We are drafting the core syntax, type system, and variable resolution logic.

*   **Status:** Draft / Request for Comments (RFC)
*   **Target:** v0.1.0

---
Copyright © 2026 The SEN Authors.