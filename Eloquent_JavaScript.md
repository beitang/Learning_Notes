# Eloquent JavaScript - Second Edition

## Introduction
> But without care, a program size and complexity will grow out of control, confusing even the person who created it. Keeping programs under control is the main problem of programming. When a program works, it is beautiful. The art of programming is the skill of controlling complexity. The great program is subdued - made simple in its complexity.
> 
> A good programming language helps the programmer by allowing them to talk about the actions that the computer has to perform on a higher level. It helps omit uninteresting details, provides convenient building blocks, allows you to define your own building blocks, and make those blocks easy to compose.
> 
> In practice, the terms ECMAScript and JavaScript can be used interchangeably - they are two names for the same language.
> 
> Web browsers are not the only platforms on which JavaScript is used. Some databae, such as MangoDB and CouchDB, use JavaScript as their scripting and query language. Several platforms for desktop and server programming, most notably the Node.js project are providing a powerful environment for programming JavaScript outside of the browser.

## Chapter 1: Values, Types, and Operators
### Values
> To be able to work with such quantities of bits without getting lost, you can separate them into chuncks that represent pieces of information. In a JavaScript environment, those chunks are called values. Though all values are made of bits, they play different roles. Every value has a type that determines its role. There are six basic types of values in JavaScript: numbers, strings, Booleans, objects, functions, and undefined values.
> 
> To create a value, you must merely invoke its name.
>
> Every value has to be stroed somewhere, and if you want to use a gigantic amount of them at the same time, you might run out of bits. Fortunately, this is a problem only if you need them all simultaneously. As soon as you no longer use a value, it will dissipate, leaving behind its bits to be recycled as building material for the next generation of value.
> 
> This chapter introduces the atomic elements of JavaScript programs, that is, the simple value types and the operators that can act on such values.

### Numbers
> Values of the number type are, unsurprisingly, numeric values. Like 13, -13, 9.81, 2.998e8.
> 
> JavaScript uses a fixed number of bits, namely 64 of them, to store a single number value.
> 
> Calculations with whole numbers (also called integers) smaller than the aforementioned 9 quadrillion are guaranteed to always be precise. Unfortunately, calculations with fractional numbers are generally not. This is a shame, but it causes practical problems only in specific situations. The important thing is to be aware of it and treat fractional digital numbers as approximations, not as precise values.

#### Arithmetic
> 100 + 4 * 11: The + and * symbols are called operators.
> 
> When operators appear together without parentheses, the order in which they are applied is determined by the precedence of the operators.

#### Special Numbers
> There are three special values in JavaScript that are considered numbers but do not behave like normal numbers.
> 
> The first two are Infinity and -Infinity, which represent the positive and negative inifities. Infinity - 1 is still Infinity, and so on. Do not put too much trust in infinity-based computation. It is not mathematically solid, and it will quickly lead to our next special number: NaN.
> 
> NaN stands for "not a number", even though it is a value of the number type. You will get this result when you, for example, try to calculate 0 / 0, Infinity - Infinity, or any number of other numeric operations that do not yield a precise, meaningful result.

### Strings
> Strings are used to represent text. They are written by enclosing their content in quotes. "Patch my boat with chewing gum", 'Monkeys wave goodbye'.
> 
> To make it possible to include such characters in a string, the following notation is used: whenever a backslash (\) is found inside quoted text, it indicates that the character after it has a special meaning. This is called escaping the character. "This is the first line\nAnd this is the second"
> 
> Strings cannot be divided, multiplied, or substracted, but the + operator can be used on them. It does not add, but it concatenates - it glues two strings together. "con" + "cat" + "e" + "nate"

### Unary Operators
> Not all operators are symbols. Some are written as words. One example is the typeof operator, which produces a string value naming the type of the value you give it.
```
console.log(typeof 4.5)
console.log(typeof "x")
```
>
> Operators that use two values are called binary operators, while those that take one are called unary operators. The minus operator can be used both as binary operator and as unary operator. `console.log(- (10 - 2))`

### Boolean Values
> true and false

#### Comparisons
```
console.log(3 > 2)
console.log(3 < 2)
console.log("Aardvark" < "Zoroaster")
```
>
> The way strings are ordered is more or less alphabetic: uppercase letters are always “less” than lowercase ones, so "Z" < "a" is true, and non-alphabetic characters (!, -, and so on) are also included in the ordering. The actual comparison is based on the Unicode standard. This standard assigns a number to virtually every character you would ever need, including characters from Greek, Arabic, Japanese, Tamil, and so on. Having such numbers is useful for storing strings inside a computer because it makes it possible to represent them as a sequence of numbers. When comparing strings, JavaScript goes over them from left to right, comparing the numeric codes of the characters one by one.
> 
> `>=, <=, ==, !=`
> 
> There is only one value in JavaScript that is not equal to itself, and that is NaN, which stands for "not a number".
> 
> `console.log(NaN == NaN)`: -> false
> 
> NaN is supposed to denote the result of a nonsensical computation, and as such, it is not equal to the result of any other nonsensical computations.



## [Eloquent JavaScript](http://eloquentjavascript.net)
