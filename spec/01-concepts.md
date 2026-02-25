# 1. Core Concepts

This document defines the fundamental concepts and mental model of the  
**SEN (Structured Environment Notation)** specification.

These concepts describe *what SEN is* and *how it should be understood*,  
independent of any concrete syntax or implementation.

---

## 1.1 Configuration as a Contract

In SEN, configuration is treated as a **formal contract** between a software
system and its runtime environment.

This contract:
- Declares **what values are required**
- Defines **their structure and types**
- Establishes **clear expectations** between configuration authors and software consumers

This contract is **machine-verifiable** and designed to support **schema
generation, validation, and tooling**.

Unlike ad-hoc key/value files, SEN configurations are intentional, explicit,
and inspectable.

---

## 1.2 Environment

An **Environment** represents a logical runtime context in which software operates.

Common examples include:
- `development`
- `testing`
- `staging`
- `production`

In SEN:
- Environments are first-class concepts
- Configuration may vary by environment
- Environment-specific overrides remain explicit and predictable

SEN does not dictate *how* an environment is selected—only how configuration
is represented and resolved once selected.

---

## 1.3 Namespace and Hierarchy

SEN configurations are **hierarchical by design**.

Instead of a flat global namespace, configuration values are organized into
logical namespaces forming a tree-like structure.

Benefits of hierarchy include:
- Reduced key collisions
- Improved readability
- Better alignment with real-world system structure
- Clearer ownership of configuration domains

Hierarchy may be expressed using nested structures or qualified paths
(e.g. dot notation); concrete syntax is defined in later sections.

---

## 1.4 Typed Values

Every configuration value in SEN has an **explicit type**.

Conceptual value types include:
- String
- Number (integer and floating-point)
- Boolean
- Array

Additional composite types (such as Object / Map) may be introduced in future
versions without violating core principles.

Explicit typing enables:
- Early error detection
- Safer configuration consumption
- Clear intent for both humans and tools

Implicit type coercion is intentionally avoided.

---

## 1.5 Composition

SEN configurations are **composable**.

A final resolved configuration may be assembled from:
- Shared base files
- Environment-specific overrides
- External inputs (e.g. environment variables)

Example (conceptual):

```

base.sen

* production.sen
* ENV variables
  = resolved configuration

```

Composition allows large systems to remain maintainable without unnecessary
duplication.

---

## 1.6 Deterministic Resolution

Configuration resolution in SEN is **deterministic**.

Given the same inputs:
- The same resolved configuration is produced
- Resolution order is well-defined
- Conflicts are resolved predictably

Determinism is essential for reproducibility, debugging, and trust in
configuration behavior.

---

## 1.7 Immutability and Overrides

Once resolved, configuration values are considered **immutable**.

Overrides:
- Are explicit and intentional
- Follow clearly defined composition rules
- Do not rely on hidden precedence or implicit behavior

This model ensures configurations remain understandable as systems scale.

---

## 1.8 Configuration vs Logic

SEN deliberately separates **configuration** from **application logic**.

Accordingly:
- SEN is not a programming language
- It does not support loops, conditionals, or arbitrary computation
- Configuration expresses *state*, not *behavior*

Any need for logic should be addressed in application code or external tools
(e.g. build systems or template engines).

---

## 1.9 Tooling-Oriented Design

SEN is designed to be both human-friendly and tool-friendly.

Its conceptual model enables:
- Static validation
- Linting
- Schema generation
- IDE and editor integrations

Tools should be able to analyze SEN configurations without executing them.

---

## 1.10 Conceptual Comparison (Informal)

At a high level:

- `.env` provides simplicity, but lacks structure and safety
- JSON and YAML provide structure, but weak typing and composition
- TOML and HCL add features, but increase cognitive and syntactic complexity

SEN focuses on **structured, typed, and composable configuration** without
becoming a programming language.

---

## 1.11 Summary

SEN is built on the following core ideas:

- Configuration is a verifiable contract
- Structure is mandatory
- Types are explicit
- Composition is intentional
- Resolution is deterministic
- Logic is excluded by design

All subsequent sections of this specification are built upon these concepts
and must not contradict them.