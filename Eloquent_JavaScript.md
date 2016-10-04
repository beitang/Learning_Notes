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

#### Logical Operations
> JavaScript supports three logical operators: and(&&), or(||), and not(!).
> 
> The last logical operator I will discuss is not unary, not binary, but ternary, operating on three values.
> 
> `console.log(true ? 1 : 2);`
> 
> This one is called the conditional operator. The value on the left of the question mark "picks" which of the other two values will come out. When it is true, the middle value is chosen, and when it is false, the value on the right comes out.

### Undefined Values
> There are two special values, written null and undefined, that are used to denote the absence of a meaningful value. They are themselves values, but they carry no information.
> 
> The difference in meaning between undefined and null is an accident of JavaScript design, and it does not matter most of the time.

### Automatic Type Conversion
> In the introduction, I mentioned that JavaScript goes out of its way to accept almost any program you give it, even programs that do odd things.
> 
> When an operator is applied to the wrong type of value, JavaScript will quietly convert that value to the type it wants, using a set of rules that often are not what you want or expect. This is called type coercion.
> 
> When you want to test whether a value has a real value instead of null or undefined, you can simply compare it to null with the == (or !=) operator.
> 
> But what if you want to test whether something refers to the precise value false? The rules for converting strings and numbers to Boolean values state that 0, NaN, and the empty string ("") count as false, while all the other values count as true. Because of this, expressions like 0 == false and "" == false are also true. For cases like this, where you do not want any automatic type conversions to happen, there are two extra operators: === and !==. The first tests whether a value is precisely equal to the other, and the second tests whether it is not precisely equal. So "" === false is false as expected.
> 
> I recommend using the three-character comparsion operators defensively to prevent unexpected type conversions from tripping you up. But when you are certain the types on both sides will be the same, there is no problem with using the shorter operators.

#### Short-Circuiting of Logical Operators
> The logical operators && and || handle values of different types in a peculiar way. They will convert the value on their left side to Boolean type in order to decide what to do, but depending on the operator and the result of that conversion, they return either the original left-hand value or the right-hand value.
> 
> The || operator, for example, will return the value of its left when that can be converted to true and will return the value one its right otherwise. This conversion works as you would expect for Boolean values and should do something analogous for values of other types.
> 
> ```
> console.log(null || "user")
> // -> user
> console.log("Karl" || "user")
> // -> Karl
> ```
>
> This functionality allows the || operator to be used as a way to fall back on a default value. If you give it an expression that might produce an empty value on the left, the value on the right will be used as a replacement in that case.
> 
> The && operator works similarly, but the other way around. When the value to its left is something that converts to false, it returns that value, and otherwise it returns the value on its right.
> 
> Another important property of these two operators is that the expression to their right is evaluated only when necessary. This is called short-circuit evaluation.
> 
> The conditional operator works in a similar way. The first expression is always evaluated, but the second or third value, the one that is not picked, it not.


## Chapter 2: Program Structure
### Expressions and Statements
> A fragment of code that produces a value is called an expression. Every value that is written literally is an expression. An expression between parentheses is also an expression, as is a binary operator applied to two expressions or a unary operator applied to one.
> 
> If an expression corresponds to a sentence fragment, a JavaScript statement corresponds to a full sentence in a human language. A program is simply a list of statements.
> 
> The simplest kind of statement is an expression with a semicolon after it.
> 
> side effects
> 
> In some cases, JavaScript allows you to omit the semicolon at the end of a statement. In other cases, it has to be there, or the next line will be treated as part of the same statement. The rules for when it can be safely omitted are somewhat complex and error-prone. In this book, every statement that needs a semicolon will always be terminated by one. I recommend you do the same in your own programs, at least until you’ve learned more about subtleties involved in leaving out semicolons.

### Variables
> To catch and hold values, JavaScript provides a thing called a variable.
> 
> `var caught = 5 * 5;`
> 
> And that gives us our second kind of statement. The special word (keyword) var indicates that this sentence is going to define a variable. It is followed by the name of the variable and, if we want to immediately give it a value, by an = operator and an expression.
> 
> Variable names can be any word that is not a reserved word. They may not include spaces. Digits can also be part of variable names, but the name must not start with a digit. A variable name cannot include punctuation, except for the characters $ and _.
> 
> If you ask for the value of an empty variable, you will get the value undefined.
> 
> A single var statement may define multiple variables. The definitions must be separated by commas.



## [Eloquent JavaScript](http://eloquentjavascript.net)
