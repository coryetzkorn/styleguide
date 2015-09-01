---
layout: library
title: JS Style
permalink: /library/js-style/
---

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Spacing
Spaces are good!

These rules encourage liberal spacing for improved readability. The minification process creates a file that is optimized for browsers to read and process.

* Indentation with tabs.
* No whitespace at the end of line or on blank lines.
* Lines should usually be no longer than 80 characters, and should not exceed 100 (counting tabs as 4 spaces). This is a “soft” rule, but long lines generally indicate unreadable or disorganized code.
`if`/`else`/`for`/`while`/`try` blocks should always use braces, and always go on multiple lines.
* Unary special-character operators (e.g., `++`, `--`) must not have space next to their operand.
* Any `,` and `;` must not have preceding space.
* Any `;` used as a statement terminator must be at the end of the line.
* Any `:` after a property name in an object definition must not have preceding space.
* The `?` and `:` in a ternary conditional must have space on both sides.
* No filler spaces in empty constructs (e.g., `{}`, `[]`, `fn()`).
* Any `!` negation operator should have a following space.

Right:

```javascript
var i;
 
if ( condition ) {
  doSomething( 'with a string' );
} else if ( otherCondition ) {
  otherThing({
      key: value,
      otherKey: otherValue
  });
} else {
  somethingElse( true );
}

while ( ! condition ) {
  iterating++;
}
 
for ( i = 0; i < 100; i++ ) {
  object[ array[ i ] ] = someFn( i );
  $( '.container' ).val( array[ i ] );
}
 
try {
  // Expressions
} catch ( e ) {
  // Expressions
}
```
Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#spacing>

### Objects
Object declarations can be made on a single line if they are short (remember the line length guidelines). When an object declaration is too long to fit on one line, there must be one property per line. Property names only need to be quoted if they are reserved words or contain special characters:

Right:

```javascript
// Preferred
var map = {
  ready: 9,
  when: 4,
  'you are': 15
};
 
// Acceptable for small objects
var map = { ready: 9, when: 4, 'you are': 15 };
 
// Bad
var map = { ready: 9,
  when: 4, 'you are': 15 };
```

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#objects>

### Arrays and Function Calls
Include extra spaces around arguments, but not properties:

Right:

```javascript
array = [ a, b ];
 
foo( arg );
 
foo( 'string', object );
 
foo( options, object[property] );
 
foo( node, 'property', 2 );
```

Inspired by: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#arrays-and-function-calls>

## Semicolons
Yes! Use them. Never rely on Automatic Semicolon Insertion (ASI).

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#semicolons>

## Indentation and Line Breaks
Indentation and line breaks add readability to complex statements.

Tabs should be used for indentation. Even if the entire file is contained in a closure (i.e., an immediately invoked function), the contents of that function should be indented by one tab:

Right:

```javascript
(function( $ ) {
    // Expressions indented
 
    function doSomething() {
        // Expressions indented
    }
})( jQuery );
```

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#indentation-and-line-breaks>

### Blocks and Curly Braces
`if`, `else`, `for`, `while`, and `try` blocks should always use braces, and always go on multiple lines. The opening brace should be on the same line as the function definition, the conditional, or the loop. The closing brace should be on the line directly following the last statement of the block.

Right:

```javascript
var a, b, c;
 
if ( myFunction() ) {
    // Expressions
} else if ( ( a && b ) || c ) {
    // Expressions
} else {
    // Expressions
}
```

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#blocks-and-curly-braces>

## Assignments and Globals

### Declaring Variables
Each function should begin with a single comma-delimited `var` statement that declares any local variables necessary. If a function does not declare a variable using `var`, that variable can leak into an outer scope (which is frequently the global scope, a worst-case scenario), and can unwittingly refer to and modify that data.

Assignments within the `var` statement should be listed on individual lines, while declarations can be grouped on a single line. Any additional lines should be indented with an additional tab. Objects and functions that occupy more than a handful of lines should be assigned outside of the `var` statement, to avoid over-indentation.

```javascript
// Good
var k, m, length,
    // Indent subsequent lines by one tab
    value = 'lorem';
 
// Bad
var foo = true;
var bar = false;
var a;
var b;
var c;
```

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#declaring-variables>

## Naming Conventions
Variable and function names should be full words, using camel case with a lowercase first letter.

Constructors intended for use with new should have a capital first letter (UpperCamelCase).

Names should be descriptive, but not excessively so. Exceptions are allowed for iterators, such as the use of `i` to represent the index in a loop.

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#naming-conventions>

## Comments
Comments come before the code to which they refer, and should always be preceded by a blank line. Capitalize the first letter of the comment, and include a period at the end when writing full sentences. There must be a single space between the comment token (`//`) and the comment text.

Single line comments:

```javascript
someStatement();
 
// Explanation of something complex on the next line
$( 'p' ).doSomething();
```

Multi-line comments should be used for long comments:

```javascript
/*
This is a comment that is long enough to warrant being stretched
over the span of multiple lines.
*/
```

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#comments>

## Equality
Strict equality checks (`===`) must be used in favor of abstract equality checks (`==`).

## Type Checks
These are the preferred ways of checking the type of an object:

* String: `typeof object === 'string'`
* Number: `typeof object === 'number'`
* Boolean: `typeof object === 'boolean'`
* Object: `typeof object === 'object'` or `_.isObject( object )`
* Plain Object: `jQuery.isPlainObject( object )`
* Function: `_.isFunction( object )` or `jQuery.isFunction( object )`
* Array: `_.isArray( object )` or `jQuery.isArray( object )`
* Element: `object.nodeType` or `_.isElement( object )`
* null: `object === null`
* null or undefined: `object == null`
* undefined:
  * Global Variables: `typeof variable === 'undefined'`
  * Local Variables: `variable === undefined`
  * Properties: `object.prop === undefined`
  * Any of the above: `_.isUndefined( object )`

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#type-checks>

## Strings
Use single-quotes for string literals:

```javascript
var myStr = 'strings should be contained in single quotes';
```

When a string contains single quotes, they need to be escaped with a backslash (`\`):

```javascript
// Escape single quotes within strings:
'Note the backslash before the \'single quotes\'';
```

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#strings>

## Best Practices

### Arrays
Creating arrays in JavaScript should be done using the shorthand `[]` constructor rather than the `new Array()` notation.

```javascript
var myArray = [];
```

You can initialize an array during construction:

```javascript
var myArray = [ 1, 'Lorem', 2, 'Ipsum' ];
```

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#arrays>

### Objects
There are many ways to create objects in JavaScript. Object literal notation, {}, is both the most performant, and also the easiest to read.

```javascript
var myObj = {};
```

Object properties should be accessed via dot notation, unless the key is a variable, a reserved word, or a string that would not be a valid identifier:

```javascript
prop = object.propertyName;
prop = object[ variableKey ];
prop = object['default'];
prop = object['key-with-hyphens'];
```

Source: <https://make.wordpress.org/core/handbook/coding-standards/javascript/#objects>