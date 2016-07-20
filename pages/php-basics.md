---
layout: page
title: "Php Basics"
description: ""
---
{% include JB/setup %}

{% include menu/php-basics.md %}

## PHP Tags

Standard Tags – best solution for portability and backwards compatibility,
because they are guaranteed to be available and cannot be disabled by changing
PHP’s configuration file. 

{% highlight php5 linenos %}
<?php 
... code
?>
{% endhighlight %}

However there can be only one open tag in the begining of the page `<?php `.

Short Tags - can be disabled (often for XML compliance) with `short_open_tag`
directive in php.ini:

{% highlight php5 linenos %}
<?
... code
?>
{% endhighlight %}

This virant of short tag is identical to  `<? echo`:
{% highlight php5 %}
<?=$variable ?>
{% endhighlight %}

Script tags is also guaranted access, same as standart tags: 

{% highlight html linenos %}
<script language="php">
... code
</script>
{% endhighlight %}

ASP Tags - must be enabled specifically in the php.ini file via the `asp_tags`
directive:

{% highlight php5 linenos %}
<%
... code
%>
<%=$variable; %>
{% endhighlight %}

* * *

## Comments

The "one-line" comment styles only comment to the end of the line or the current
block of PHP code, whichever comes first. This means that HTML code after 
`// ... ?>` or `# ... ?>` WILL be printed: `?>` breaks out of PHP mode and returns to 
HTML mode, and // or # cannot influence that. If the `asp_tags` configuration directive
is enabled, it behaves the same with `// %>` and `# %>`. However, the `</script>` tag
doesn't break out of PHP mode in a one-line comment.

{% highlight php5 linenos %}
<?php
// This is a single line comment

# This is also a single line comment 
# New line comment ?> Here new line comment dont work, and this will be printed
{% endhighlight %}

Multi-line comments end at the first `*/` encountered. Make sure you don't nest 
multi-line comments. It is easy to make this mistake if you are trying to comment out
a large block of code.

{% highlight php5 linenos %}
<?php
/*
This is a multi-line
comment
*/

/* this is also
commented */ but this not */
?>
{% endhighlight %}

Below you can find DocComment example. For PHP itself it looks like regular comment.
For futher information you can visit [phpDocumentor](http://www.phpdoc.org/) site.

{% highlight php5 linenos %}
<?php
/**
* API Documentation Example
*
* @param string $bar
*/
function foo($bar) { }
?>
{% endhighlight %}

* * *

## Operators

An operator is something that takes one or more values (or expressions, in
programming jargon) and yields another value (so that the construction itself
becomes an expression).

Operators can be grouped according to the number of values they take. Unary
operators take only one value, for example `!` (the logical not operator) or
`++` (the increment operator). Binary operators take two values, such as the
familiar arithmetical operators `+` (plus) and `-` (minus), and the majority of
PHP operators fall into this category. Finally, there is a single ternary
operator, `? :`, which takes three values; this is usually referred to simply as
"the ternary operator" (although it could perhaps more properly be called the
conditional operator).

The precedence of an operator specifies how "tightly" it binds two expressions
together. For example, in the expression `1 + 5 * 3`, the answer is 16 and not
18 because the multiplication `*` operator has a higher precedence than the
addition `+` operator. Parentheses may be used to force precedence, if
necessary. For instance: `(1 + 5) * 3` evaluates to 18.

When operators have equal precedence, their associativity decides whether they
are evaluated starting from the right, or starting from the left.

For the understanding of the operators precede please look at the table on the 
[PHP manual page](http://php.net/manual/en/language.operators.precedence.php)

### Arithmetic Operators

Works same for the real world:

{% highlight php5 linenos %}
<?php

echo 2 + 2; // Addition. Will print 4
echo 3 - 2; // Subtraction. will print 1
echo 1 * 2; // Multiplication. Will print 2
echo 4 / 2; // Division . Will print 2
echo -2; // Negation. Will print -2
echo 3 % 2 // Modulus. Will print 1

?>
{% endhighlight %}

The division operator `/` returns a float value unless the two operands are
integers (or strings that get converted to integers) and the numbers are evenly
divisible, in which case an integer value will be returned. If try to division
by zero then `PHP Warning: Division by zero` will be thrown.

Operands of modulus are converted to integers (by stripping the decimal part)
before processing.

The result of the modulus operator % has the same sign as the dividend — that
is, the result of $a % $b will have the same sign as $a.

### Assignment Operators

The basic assignment operator is `=`. It means that the left operand gets set to
the value of the expression on the right (that is, "gets set to").

The value of an assignment expression is the value assigned. That is, the value
of `$a` in expression `$a = 3` equal to 3.

For arrays, assigning a value to a named key is performed using the `=>`
operator. The precedence of this operator is the same as other assignment
operators.

In addition to the basic assignment operator, there are "combined operators" for
all of the binary arithmetic, array union and string operators that allow you to
use a value in an expression and then set its value to the result of that
expression. For example:

{% highlight php5 linenos %}
<?php
$a = 3;
$a += 5; // Equal 8
?>
{% endhighlight %}

Note that the assignment copies the original variable to the new one (assignment
by value), so changes to one will not affect the other

#### Assignment by Reference

Assignment by reference is also supported, using the `$var = &$othervar;` syntax
(ampersand `&` before variable). Assignment by reference means that both
variables end up pointing at the same data, and nothing is copied anywhere.

{% highlight php5 linenos %}
<?php
$a = 3;
$b = &$a; // $b is a reference to $a

print "$a\n"; // prints 3
print "$b\n"; // prints 3

$a = 4; // change $a

print "$a\n"; // prints 4
print "$b\n"; // prints 4 as well, since $b is a reference to $a
?>
{% endhighlight %}

As of PHP 5, the new operator returns a reference automatically, so assigning
the result of new by reference results in an **E_DEPRECATED** message in PHP 5.3
and later.

More information on references and their potential uses can be found in the
[References Explained](http://php.net/manual/en/language.references.php) section
of the manual.

### Bitwise Operators

Bitwise operators allow evaluation and manipulation of specific bits within an
integer. Integral numbers are internally converted into bits: 
`5 -> 0101 = 0*8 + 1*4 + 0*2 + 1*1`

Bit shifting in PHP is arithmetic. Bits shifted off either end are discarded.
Left shifts have zeros shifted in on the right while the sign bit is shifted out
on the left, meaning the sign of an operand is not preserved. Right shifts have
copies of the sign bit shifted in on the left, meaning the sign of an operand is
preserved.

Use parentheses to ensure the desired precedence. For example, `$a & $b == true`
evaluates the equivalency then the bitwise and; while `($a & $b) == true`
evaluates the bitwise and then the equivalency.

Be aware of data type conversions. If both the left-hand and right-hand
parameters are strings, the bitwise operator will operate on the characters
ASCII values.

* `$a & $b` (And) — Bits that are set in both $a and $b are set. Matching `1`
in both. 
* `$a | $b` (Or (inclusive or)) — Bits that are set in either $a or $b are set.
At least one `1`.
* `$a ^ $b` (Xor (exclusive or)) — Bits that are set in $a or $b but not both 
are set. Only one `1` in both.
* `~ $a` (Not) — Bits that are set in $a are not set, and vice versa. Convet `0`
in to `1` and `1` in to `0`
* `>>` (Shift Right) – All of the bits in the binary number shift N places to 
the rightin the number, the right most digit(s) falls out, and the resulting 
number is padded on the left with 0s. A right shift of one is equivalent to 
dividing a number by two, and tossing the remainder.
* `<<` (Shift Left) – All of the digits shift N places to the left, padding the 
right with 0s. A left shift of one is equivalent to multiplying a number by two.

More information, converation and examples you can find in 
[php manual page](http://php.net/manual/en/language.operators.bitwise.php)

### Comparison Operators

Comparison operators, as their name implies, allow you to compare two values.

* `$a == $b` (Equal) — **TRUE** if $a is equal to $b after type juggling.
* `$a === $b` (Identical) — **TRUE** if $a is equal to $b, and they are of the 
same type.
* `$a != $b` `$a <> $b` (Not equal) — **TRUE** if $a is not equal to $b after 
type juggling.
* `$a !== $b` (Not identical) — **TRUE** if $a is not equal to $b, or they are 
not of the same type
* `$a < $b` (Less than) — **TRUE** if $a is strictly less than $b.
* `$a > $b` (Greater than) — **TRUE** if $a is strictly greater than $b.
* `$a <= $b` (Less than or equal to) — **TRUE** if $a is less than or equal to 
$b.
* `$a >= $b` (Greater than or equal to) — **TRUE** if $a is greater than or 
equal to $b.

If you compare a number with a string or the comparison involves numerical
strings, then each string is converted to a number and the comparison performed
numerically. The type conversion does not take place when the comparison is 
`===` or `!==` as this involves comparing the type as well as the value.

For various types, comparison is done according to the following:

* `null` to `string` — Convert NULL to "", or other words to empty string
* `bool or null` to anything — Convert to `bool`
* `object` to `object` — When using the comparison operator `==`, object 
variables are compared in a simple manner, namely: Two object instances are 
equal if they have the same attributes and values, and are instances of the same 
class. On the other hand, when using the identity operator `===`, object 
variables are identical if and only if they refer to the same instance of the 
same class
* `string, resource or number` to `string, resource or number` — Translate 
strings and resources to numbers
* `array` to `array` — Array with fewer members is smaller, if key from operand 
1 is not found in operand 2 then arrays are uncomparable, otherwise - compare 
value by value
* `array` to anything — array is always grater
* `object` to anything — object is always grater.

**Warning**: Because of the way floats are represented internally, you should 
not test two floats for equality. See the documentation for 
[float](http://php.net/manual/en/language.types.float.php) for more information

#### Ternary Operator

Another conditional operator is the `?:` (or ternary) operator. The expression
`(expr1) ? (expr2) : (expr3)` evaluates to expr2 if expr1 evaluates to **TRUE**,
and expr3 if expr1 evaluates to **FALSE**. Since PHP 5.3, it is possible to
leave out the middle part of the ternary operator. Expression `expr1 ?: expr3`
returns expr1 if expr1 evaluates to **TRUE**, and expr3 otherwise.

Please note that the ternary operator is a statement, and that it doesn't
evaluate to a variable, but to the result of a statement. This is important to
know if you want to return a variable by reference. The statement 
`return $var == 42 ? $a : $b;` in a return-by-reference function will therefore 
not work and a warning is issued in later PHP versions.

It is recommended that you avoid "stacking" ternary expressions. PHP's behaviour
when using more than one ternary operator within a single statement is 
non-obvious.

### Error Control Operators

PHP supports one error control operator: the at sign `@`. When prepended to an
expression in PHP, any error messages that might be generated by that expression
will be ignored.

If you have set a custom error handler function with `set_error_handler()` then it
will still get called, but this custom error handler can (and should) call
`error_reporting()` which will return 0 when the call that triggered the error was
preceded by an `@`.

If the `track_errors` feature is enabled, any error message generated by the
expression will be saved in the variable `$php_errormsg`. This variable will be
overwritten on each error.

**Note**: The `@` works only on expressions. A simple rule of thumb is: if
you can take the value of something, you can prepend the `@` operator to it. For
instance, you can prepend it to variables, function and include calls,
constants, and so forth. You cannot prepend it to function or class definitions,
or conditional structures such as if and foreach, and so forth.

**Warning**: Currently the `@` error-control operator prefix will even disable
error reporting for critical errors that will terminate script execution. Among
other things, this means that if you use `@` to suppress errors from a certain
function and either it isn't available or has been mistyped, the script will die
right there with no indication as to why.

### Execution Operators

PHP supports one execution operator: backticks (`` ` ` ``). PHP will attempt to
execute the contents of the backticks as a shell command; the output will be
returned (i.e., it won't simply be dumped to output; it can be assigned to a
variable). Use of the backtick operator is identical to shell_exec(). Example:

{% highlight php5 linenos %}
<?php
$ls = `ls -la`;
print_r($ls); // will pint output of ls command
?>
{% endhighlight %}

### Incrementing/Decrementing Operators

PHP supports C-style pre- and post-increment and decrement operators.

* `++$a` (pre-increment) — Increments `$a` by one, then return `$a`
* `$a++` (post-increment) — Returns `$a`, then increments in by one
* `--$a` (pre-decrement) — same as pre-increment, but decrement
* `$a--` (post-decrement) — same as post-increment, but decrement

PHP follows Perl's convention when dealing with arithmetic operations on
character variables. For example, in PHP and Perl $a = 'Z'; $a++; turns $a into
'AA'. Note that character variables can be incremented but not decremented and
even so only plain ASCII characters (a-z and A-Z) are supported.
Incrementing/decrementing other character variables has no effect, the original
string is unchanged.

**Note**: The increment/decrement operators do not affect boolean values.
Decrementing NULL values has no effect too, but incrementing them results in 1.

### Logical Operators

* `$a and $b` (And) — TRUE if both `$a` and `$b` are TRUE.
* `$a or $b` (Or) — TRUE if either `$a` or `$b` is TRUE.
* `$a xor $b` (Xor) — TRUE if either `$a` or `$b` is TRUE, but not both.
* `! $a` (Not) — TRUE if `$a` is not TRUE.
* `$a && $b` (And) — TRUE if both `$a` and `$b` are TRUE.
* `$a || $b` (Or) — TRUE if either `$a` or `$b` is TRUE.

The reason for the two different variations of *and* and *or* operators is that
they operate at different precedences, `&&` and `||` operators have more
precedence level then `and` and `or`.

### String Operators

There are two string operators. The first is the concatenation operator `.`,
which returns the concatenation of its right and left arguments. The second is
the concatenating assignment operator `.=`, which appends the argument on the
right side to the argument on the left side.

### Array Operators

* `$a + $b` (Union) — Union of `$a` and `$b`.
* `$a == $b` (Equality) — TRUE if $a and $b have the same key/value pairs.
* `$a === $b` (Identity) — TRUE if $a and $b have the same key/value pairs in 
the same order and of the same types.
* `$a != $b` (Inequality) — TRUE if $a is not equal to $b.
* `$a <> $b` (Inequality) — TRUE if $a is not equal to $b.
* `$a !== $b` (Non-identity) — TRUE if $a is not identical to $b.

The `+` operator returns the right-hand array appended to the left-hand array;
for keys that exist in both arrays, the elements from the left-hand array will
be used, and the matching elements from the right-hand array will be ignored.

### Type Operators

`Instanceof` – Returns true if the indicated variable is an instance of the
designated class, one of it’s subclasses or a designated interface.

* * *

## Variables

### Naming:

* Can only contain letters, numbers or underscores
* Must start with a letter or an underscore

### Types

* Scalar types: boolean, string, integer, float.
* Compound types: array, object.
* Special Types: resource, null.

### Strings

Each character is represented by a single byte. PHP has no native support for multi-byte character sets (like Unicode).

Ordered collections of binary data.

Can be quoted in one of three ways:

* `'some text'` - characters within single quotes will be recorded as is, without variable or escape sequences interpreted and replaced
* `"some text"` – variables and escape sequences will be interpreted and replaced
* `<<<` – Heredoc functions in a similar manner to double quotes, but is designed to span multiple lines, and allow for the use of quotes without escaping.

{% highlight php5 linenos %}
<?php
$greeting = <<<GREETING
She said "That is $name's" dog!
While running towards the thief
GREETING;
{% endhighlight %}

### Integer

Can be specified in decimal (base 10), hexadecimal (base 16, precede with a 0x), or octal (base 8, precede with a 0) notation and optionally preceded by a sign (+, -)

The maximum size of an integer is platform dependent, a maximum of ~2Billion is common

### Float

`1.234, 1.2e3, 7E-10`

The size of a float is platform-dependent, although a maximum of `~1.8e308` with a precision of roughly 14 decimal digits is a common value

### Boolean

* Any integer other than 0 is cast to TRUE
* TRUE & FALSE are case-insensitive, though the all caps representation is common

### Arrays

Arrays can contain any combination of other variable types, even arrays or objects

### Objects

Objects allow data and methods to be combined into one cohesive structure

### Resource

Special variable that represents some sort of operating system resource, generally an open file or database connection.

While variables of the type resource can be printed out, their only sensible use is with the functions designed to work with them.

### null

* it has no value and no type
* is not the same as the integer zero or an zero length string (which would have types)

### Variable Variables

{% highlight php5 linenos %}
<?php
$a = 'name';
$$a = "Paul";
echo $name; //Paul
{% endhighlight %}

* * *

## Constants

Can not be changed once set.

{% highlight php5 linenos %}
<?php
define('ERROR', 'Something went wrong.');
const FOO = 'bar';
{% endhighlight %}

Only scalar.

* * *

## Controle Structures

### if

Alternate:

{% highlight php5 linenos %}
<?php
if ():
  ... 
else: 
  ... 
elseif:
  ... 
endif;
{% endhighlight %}

Short:

{% highlight php5 linenos %}
<?php
$expr ? true : false)
{% endhighlight %}

### switch

### while

### do

### for

continue

break

### foreach

### functions

Paramaters:

* Optional
* Byref
* Byval
* Objects
* Variable functions

### Objects

* * *

## Language Constructs

Elements that are built-into the language.

Do not have return value.

{% highlight php5 linenos %}
<?php
echo 'something'; 
die();
exit();
{% endhighlight %}

End a script in PHP5:

{% highlight php5 linenos %}
<?php
__halt_compiler()
die();
exit();
{% endhighlight %}

* * *

## Namespaces

[http://www.php.net/manual/en/language.namespaces.php](http://www.php.net/manual/en/language.namespaces.php)

Solves two problems:

* Name collisions between code you create, and internal PHP classes/functions/constants or third-party classes/functions/constants.
* Ability to alias (or shorten) Extra_Long_Names designed to alleviate the first problem, improving readability of source code.

Only three types of code units are affected by namespaces: 

* classes
* functions
* constants. 

A file containing a namespace must declare the namespace at the top of the file before any other code - with one exception: the [declare](http://www.php.net/manual/en/control-structures.declare.php) keyword. 

Namespace name can be defined with sub-levels.

A class name can be referred to in three ways:

1. Unqualified name, or an unprefixed class name like `$a = new foo();` or `foo::staticmethod();`. If the current namespace is `currentnamespace`, this resolves to `currentnamespace\foo`. If the code is global, non-namespaced code, this resolves to `foo`. One caveat: unqualified names for functions and constants will resolve to global functions and constants if the namespaced function or constant is not defined. See [Using namespaces: fallback to global function/constant](http://www.php.net/manual/en/language.namespaces.fallback.php) for details.
2. Qualified name, or a prefixed class name like `$a = new subnamespace\foo();` or `subnamespace\foo::staticmethod();`. If the current namespace is `currentnamespace`, this resolves to `currentnamespace\subnamespace\foo`. If the code is global, non-namespaced code, this resolves to `subnamespace\foo`.
3. Fully qualified name, or a prefixed name with global prefix operator like `$a = new \currentnamespace\foo();` or `\currentnamespace\foo::staticmethod();`. This always resolves to the literal name specified in the code, `currentnamespace\foo`.

Two kinds of aliasing or importing: aliasing a class name, and aliasing a namespace name.

{% highlight php5 linenos %}
<?php
namespace my\name; // see "Defining Namespaces" section

class MyClass {}
function myfunction() {}
const MYCONST = 1;

$a = new MyClass;
$c = new \my\name\MyClass; // see "Global Space" section

$a = strlen('hi'); // see "Using namespaces: fallback to global
                   // function/constant" section

$d = namespace\MYCONST; // see "namespace operator and __NAMESPACE__
                        // constant" section
$d = __NAMESPACE__ . '\MYCONST';
echo constant($d); // see "Namespaces and dynamic language features" section
?>
{% endhighlight %}

{% highlight php5 linenos %}
<?php
namespace foo;
use My\Full\Classname as Another;

// this is the same as use My\Full\NSname as NSname
use My\Full\NSname;

// importing a global class
use \ArrayObject;

$obj = new namespace\Another; // instantiates object of class foo\Another
$obj = new Another; // instantiates object of class My\Full\Classname
NSname\subns\func(); // calls function My\Full\NSname\subns\func
$a = new ArrayObject(array(1)); // instantiates object of class ArrayObject
// without the "use \ArrayObject" we would instantiate an object of class foo\ArrayObject
?>
{% endhighlight %}

* * *

## Extensions

[http://devzone.zend.com/article/1021](http://devzone.zend.com/article/1021)

The PHP source bundle comes with around 86 extensions, having an average of about 30 functions each. Do the math, that's about 2500 functions. As if this weren't enough, [the PECL repository](http://pecl.php.net/) offers over 100 additional extensions, and even more can be found elsewhere on the Internet. 

* * *

## Config

[http://www.php.net/manual/en/configure.about.php](http://www.php.net/manual/en/configure.about.php)

[http://php.net/manual/en/configuration.php](http://php.net/manual/en/configuration.php)

* * *

## Performance. Bytecode caching

