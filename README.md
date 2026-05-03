# LLD Design Patterns

> A comprehensive reference for **Low-Level Design (LLD)** — covering SOLID principles, all 21 Gang of Four design patterns with diagrams, and Java/Python syntax quick references.

[![Java](https://img.shields.io/badge/Java-Design%20Patterns-ED8B00?logo=java)](https://www.java.com)
[![Python](https://img.shields.io/badge/Python-Syntax%20Reference-blue?logo=python)](https://python.org)
[![Patterns](https://img.shields.io/badge/Patterns-21%20GoF-green)](#design-patterns)
[![Reference](https://img.shields.io/badge/Book-Head%20First%20Design%20Patterns-orange)](https://www.oreilly.com/library/view/head-first-design/0596007124/)

---

## Contents

- [SOLID Principles](#solid-principles)
- [Design Patterns](#design-patterns)
  - [Creational](#-creational-patterns-5)
  - [Structural](#-structural-patterns-7)
  - [Behavioral](#-behavioral-patterns-9)
- [Java Syntax Reference](#java-syntax-reference)
- [Python Syntax Reference](#python-syntax-reference)

---

## SOLID Principles

📄 [solid_principle.md](./solid_principle.md)

| Principle | Description |
|---|---|
| **S** — Single Responsibility | A class should have only one reason to change |
| **O** — Open/Closed | Open for extension, closed for modification |
| **L** — Liskov Substitution | Subtypes must be substitutable for their base types |
| **I** — Interface Segregation | No client should depend on methods it doesn't use |
| **D** — Dependency Inversion | Depend on abstractions, not concrete implementations |

---

## Design Patterns

Based on **Head First Design Patterns** (Gang of Four). Each pattern includes intent, use cases, class diagram, and Java implementation.

### 🏗 Creational Patterns (5)

> Deal with object creation mechanisms.

| Pattern | Intent | Docs |
|---|---|---|
| **Singleton** | Ensures only one instance exists globally | [📄](./design_patterns/creational_design_patterns/singleton.md) |
| **Factory Method** | Creates objects without specifying the exact class | [📄](./design_patterns/creational_design_patterns/factory_method.md) |
| **Abstract Factory** | Creates families of related objects | [📄](./design_patterns/creational_design_patterns/abstract_factory.md) |
| **Builder** | Constructs complex objects step by step | [📄](./design_patterns/creational_design_patterns/builder_design.md) |
| **Prototype** | Creates objects by cloning an existing instance | [📄](./design_patterns/creational_design_patterns/prototype.md) |

### 🔧 Structural Patterns (7)

> Deal with object composition and relationships.

| Pattern | Intent | Docs |
|---|---|---|
| **Adapter** | Makes incompatible interfaces work together | [📄](./design_patterns/structural_design_patterns/adaptor_design.md) |
| **Bridge** | Decouples abstraction from implementation | [📄](./design_patterns/structural_design_patterns/bridge_design_pattern.md) |
| **Composite** | Treats individual objects and compositions uniformly | [📄](./design_patterns/structural_design_patterns/composite_design_pattern.md) |
| **Decorator** | Adds responsibilities to objects dynamically | [📄](./design_patterns/structural_design_patterns/decorater_design_pattern.md) |
| **Facade** | Provides a simplified interface to a subsystem | [📄](./design_patterns/structural_design_patterns/facade_method_design.md) |
| **Flyweight** | Shares state to efficiently support large numbers of objects | [📄](./design_patterns/structural_design_patterns/flyweight_design_pattern.md) |
| **Proxy** | Controls access to another object | [📄](./design_patterns/structural_design_patterns/proxy_design.md) |

### 🔄 Behavioral Patterns (9)

> Deal with communication and responsibility between objects.

| Pattern | Intent | Docs |
|---|---|---|
| **Observer** | Notifies dependents when an object changes state | [📄](./design_patterns/behavioral_design_patterns/observer_design.md) |
| **Strategy** | Selects an algorithm at runtime | [📄](./design_patterns/behavioral_design_patterns/strategy_design_pattern.md) |
| **State** | Alters behavior when internal state changes | [📄](./design_patterns/behavioral_design_patterns/state_design_pattern.md) |
| **Template Method** | Defines algorithm skeleton, defers steps to subclasses | [📄](./design_patterns/behavioral_design_patterns/template_method_design_pattern.md) |
| **Command** | Encapsulates a request as an object | [📄](./design_patterns/behavioral_design_patterns/command_design_pattern.md) |
| **Chain of Responsibility** | Passes request along a chain of handlers | [📄](./design_patterns/behavioral_design_patterns/chain_of_responsibility_design_pattern.md) |
| **Iterator** | Accesses elements sequentially without exposing structure | [📄](./design_patterns/behavioral_design_patterns/iterator_design_pattern.md) |
| **Memento** | Captures and restores an object's internal state | [📄](./design_patterns/behavioral_design_patterns/memento_design_pattern.md) |
| **Behavioral Overview** | General intro to behavioral patterns | [📄](./design_patterns/behavioral_design_patterns/behavioral_design.md) |

---

## Java Syntax Reference

Quick-reference cheat sheets for Java data structures and collections — useful for coding interviews and LLD implementations.

| Topic | File |
|---|---|
| General Syntax (Scanner, Comparators, all collections) | [java_general_syntax](./java_syntax/java_general_syntax) |
| Arrays | [java_syntax_array](./java_syntax/java_syntax_array) |
| ArrayList | [java_syntax_arraylist](./java_syntax/java_syntax_arraylist) |
| LinkedList | [java_syntax_linkedList](./java_syntax/java_syntax_linkedList) |
| HashMap | [java_syntax_hashmap](./java_syntax/java_syntax_hashmap) |
| HashSet | [java_syntax_hashset](./java_syntax/java_syntax_hashset) |
| Stack & Queue | [java_syntax_stack_queue](./java_syntax/java_syntax_stack_queue) |
| Deque | [java_syntax_de_queue](./java_syntax/java_syntax_de_queue) |
| Priority Queue (Heap) | [java_syntax_priority_queue](./java_syntax/java_syntax_priority_queue) |
| String | [java_syntax_string](./java_syntax/java_syntax_string) |
| StringBuilder | [java_syntax_stringBuilder](./java_syntax/java_syntax_stringBuilder) |
| Integer Class | [java_syntax_integerclass](./java_syntax/java_syntax_integerclass) |
| Iterator | [java_syntax_iterator](./java_syntax/java_syntax_iterator) |
| Things to Remember | [java_syntax_to_remberer](./java_syntax/java_syntax_to_remberer) |

---

## Python Syntax Reference

| Topic | File |
|---|---|
| General Python Syntax | [python_general_syntax](./java_syntax/python_general_syntax) |

---

## Resources

- 📘 [Head First Design Patterns — O'Reilly](https://www.oreilly.com/library/view/head-first-design/0596007124/)
- 📘 [Refactoring Guru — Design Patterns](https://refactoring.guru/design-patterns)
