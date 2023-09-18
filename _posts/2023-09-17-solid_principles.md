---
layout: post
author: "praconfi"
tags: 'interview'
title: "SOLID Principles"
---

# SOLID Principles

solid principles are a set of principles that should be followed to create software with good design that responds well to change. This makes the code more extensible and easier to maintain.

Single Responsibility Principle: 

- One class should have only one responsibility, and all methods of the class should be focused on performing that responsibility
- In other words, there should be only one reason to change a class
- This prevents ripple effects, from one responsibility to another

Open Close Principle:

- Software components should be open for extension and closed for modification.
- Even if there are changes or additional requirements in the specifications, the existing components should not be modified, they should be easily extended and reused.
- Distinguishing between what will change and what will remain, connect them through interfaces. Then, extend a new class depending on the interfaces.

Liskov Substitution Principle

- sub-class should always be replaceable with its parent class.

Interface Segregation Principle

- Using multiple specific interfaces is better than using a single generic interface.
- The single responsibility of an interface

Dependency Inversion Principle

- Depends on an abstracted superclass rather than a sub-class.
- Depends on the interface rather than the concrete class.
- Depends on what changes less rather than what changes frequently.