---
title: "SyntaxError: missing name after . operator"
slug: Web/JavaScript/Reference/Errors/Missing_name_after_dot_operator
page-type: javascript-error
sidebar: jssidebar
---

The JavaScript exception "missing name after . operator" occurs when there is a problem
with how the dot operator (`.`) is used
for [property access](/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors).

## Message

```plain
SyntaxError: missing name after . operator (Firefox)
SyntaxError: Unexpected token '['. Expected a property name after '.'. (Safari)
```

## Error type

{{jsxref("SyntaxError")}}

## What went wrong?

The dot operator (`.`) is used for [property access](/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors).
You will have to specify the name of the property that you want to access.
For computed property access, you might need to change your property access from using a
dot to using square brackets. These will allow you to compute an expression. Maybe you
intended to do concatenation instead? A plus operator (`+`) is needed in that
case. Please see the examples below.

## Examples

### Property access

[Property accessors](/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors)
in JavaScript use either the dot (.) or square brackets (`[]`), but not both.
Square brackets allow computed property access.

```js-nolint example-bad
const obj = { foo: { bar: "baz", bar2: "baz2" } };
const i = 2;

obj.[foo].[bar]
// SyntaxError: missing name after . operator

obj.foo."bar"+i;
// SyntaxError: missing name after . operator
```

To fix this code, you need to access the object like this:

```js example-good
obj.foo.bar; // "baz"
// or alternatively
obj["foo"]["bar"]; // "baz"

// computed properties require square brackets
obj.foo["bar" + i]; // "baz2"
// or as template literal
obj.foo[`bar${i}`]; // "baz2"
```

### Property access vs. concatenation

If you are coming from another programming language (like [PHP](/en-US/docs/Glossary/PHP)), it is also easy to mix up the dot operator
(`.`) and the concatenation operator (`+`).

```js-nolint example-bad
console.log("Hello" . "world");

// SyntaxError: missing name after . operator
```

Instead you need to use a plus sign for concatenation:

```js example-good
console.log("Hello" + "World");
```

## See also

- [Property accessors](/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors)
