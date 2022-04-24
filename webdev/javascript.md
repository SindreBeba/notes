---
layout: default
title: JavaScript
parent: Web development
---

# JavaScript

## Types

JavaScript is a loosely typed programming language, meaning that the variable types are not declared with the variable. It's also a dynamically typed language where type checking happens at run time. This means that variables don't have types, but values do.

`undefined`, `string`, `number`, `boolean`, `object`, and `symbol` are the primitive types in JavaScript, and you can use the `typeof` operator to check the type of a value.

However, both declared variables with no assigned value and undeclared variables will return `undefined` as the type when using `typeof`.

There is also a historical bug present in JavaScript where `typeof null` will return `object`.