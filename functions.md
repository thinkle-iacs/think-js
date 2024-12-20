Functions
=========================

Functions
-------------------------

In Javascript, a **function** is a named sequence of statements
that belong together. Their primary purpose is to help us
organize programs into chunks that match how we think about
the problem.

The syntax for a **function definition**, using *arrow functions* is:

```javascript        
const NAME = ( PARAMETERS ) => {
  STATEMENTS
}
```

We can make up any names we want for the functions we create, except that
we can't use a name that is a Javascript keyword, and the names must follow the rules
for legal identifiers (the same rules that apply to variable names).

> *Arrow Functions*
>
> We call these functions arrows because the `=>` characters look like an arrow.
> JavaScript also supports another function syntax using the `function` keyword
> which differs from Arrow Functions in subtle but important ways. To keep things
> simple in this book, we will only use Arrow Functions, but you may find the
> `function` keyword in examples you find elsewhere.


There can be any number of statements inside the function, but they have to be
between the curly braces (`{}`). These statements make up the **function body**.
In the examples in this book, we will use the
standard indentation of two spaces. Function definitions are the second of
several **compound statements** we will see, all of which have the same
pattern:

1. A header line which begins with a keyword and ends with an opening (left) curly brace.
2. A **body** consisting of one or more Javascript statements, each
   indented the same amount — *we will use 2 spaces* — from
   the header line.
3. A closing (right) curly brace.

We've already seen the `for` loop which follows this pattern.

So looking again at the function definition, the parameter list may be empty, 
or it may contain any number of parameters separated from one another by commas. 
In either case, the parentheses are required. The parameters specify what information, 
if any, we have to provide in order to use the new function.

Suppose we are writing a program to calculate the amount of tip due on a
bill. We might write a function to "calculate tip". "calculate tip" is
an *abstraction*, or a mental chunk, of a number of smaller steps.  So
let's write a function to capture the pattern of this "building block":

```javascript
/*
  Calculate the tip on a bill, given the pct of the tip.
*/
const calculateTip = (bill, pct) => {
  let tip = bill * (pct * .01); // convert pct to a decimal and calculate
  let total = tip + bill;
  // convert to a number with 2 decimal places
  total = Number.parseFloat(total).toFixed(2);

  // now show the results to the user
  console.log("Bill amount: $" + bill);
  console.log("Tip percentage: " + pct + "%");
  console.log("Total amount due: $" + total);
}

// find the amount of an 18% tip on a $100 bill
calculateTip(100,18);
```

This function is named `calculateTip`.  It has two parameters: one to tell
the function the amount of the bill, and the other to tell it the percent
tip to calculate.

Here is the same `calculateTip` function implemented using the TextInterface library:
{% include codepen.html id="eYqaMMB" user="thinkle-iacs" %}


Defining a new function does not make the function run. To do that we
need a **function call**. We've already seen how to call some built-in
functions like **console.log**, **window.input**, and **Number.parseInt**. Function
calls contain the name of the function being executed followed by a list
of values, called *arguments*, which are assigned to the parameters in
the function definition. So in the last line of the example program
above, we call the function, and pass `100` as the amount of the bill
and `18` as the percentage of the tip. While the function is
executing, then, the variable `bill` refers to the value 100, and the
variable `pct` refers to 18. We can pass either variables (like `myBill`)
or literal values (like `100`) as arguments.

Once we've defined a function, we can call it as often as we like, and its
statements will be executed each time we call it. In the next example, we calculate 3 different
tip amounts for the same bill, using `calculateTip` defined above.

```javascript
let myBill = 100;
calculateTip(myBill, 15);
calculateTip(myBill, 18);
calculateTip(myBill, 20);
```


> ### Coding Style
>
>  Now that you are about to write longer, more complex pieces of Javascript,
  it is a good time to talk about coding style. Most languages can be
  written (or more concise, formatted) in different styles; some are more
  readable than others. Making it easy for others to read your code is
  always a good idea, and adopting a nice coding style helps tremendously
  for that.
>
>  For our Javascript, we will follow the coding style described in the [Mozilla project developer's guide](https://developer.mozilla.org/en-US/docs/Mozilla/Developer_guide/Coding_Style). Here are the most important points extracted for you:
>
>  - Use 2-space indentation, and no tabs.
>  - Wrap lines so that they don’t exceed 80 characters.
>    - This helps users with small displays and makes it possible to have
      several code files side-by-side on larger displays.
>  - Use double quotes `"` for string literals, except when avoiding inline double quotes
>  - Use blank lines to separate functions and classes, and larger blocks
    of code inside functions.
>  - When possible, put comments on a line of their own.
>  - Use spaces around operators and after commas, but not directly inside
    bracketing constructs: a = f(1, 2) + g(3, 4).
>  - Name your variables, classes, and functions consistently; the convention is to use
    CamelCase for identifier names.
>  - Don’t use fancy encodings if your code is meant to be used in
    international environments. Use UTF-8 or plain ASCII.
    - Likewise, don’t use non-ASCII characters in identifiers.`


Composition: Functions can call other functions
--------------------------------------------------

So far, we have looked at the elements of a program—`variables`,
`expressions`, and `statements`—in isolation, without talking about how to
combine them.

One of the most useful features of programming languages is their
ability to take small building blocks and **compose** them. In our `calculateTip`
example, we call several Javascript built-in functions: `toFixed` to keep our amounts
to 2 decimal places and `Number.parseFloat` to convert the data to a float so that
we can use `toFixed`. We use `console.log` to print our output on the Javascript
console. As we will see, we can compose our programs of many functions
that we define ourselves.

There are some points worth noting here:

* Functions can call other functions.
* A caller of this function might say `calculateTip(myBill, 15)`.  The parameters
  of this function, `bill` and `tip`, are assigned the values of the myBill variable, and
  the number literal 15, respectively.
* In the body of the function they are just like any other variable.

So far, it may not be clear why it is worth the trouble to create all of these
new functions. Actually, there are a lot of reasons, but this example
demonstrates two:

1. Creating a new function gives us an opportunity to name a group of
   statements. Functions can simplify a program by hiding a complex computation
   behind a single command. The function (including its name) can capture our
   mental chunking, or *abstraction*, of the problem.  
2. Creating a new function can make a program smaller by eliminating repetitive
   code.  

As we might expect, we have to create a function before we can execute it.
In other words, the function definition has to be executed before the
function is called.

Flow of execution
----------------------------------

In order to ensure that a function is defined before its first use, we have to
know the order in which statements are executed, which is called the **flow of
execution**.

Execution always begins at the first statement of the program.  Statements are
executed one at a time, in order from top to bottom.

Function definitions do not alter the flow of execution of the program, but
remember that statements inside the function are not executed until the
function is called. In Javascript we can define one function
inside another. In this case, the inner definition isn't executed until the
outer function is called.

Function calls are like a detour in the flow of execution. Instead of going to
the next statement, the flow jumps to the first line of the called function,
executes all the statements there, and then comes back to pick up where it left
off.

That sounds simple enough, until we remember that one function can call
another. While in the middle of one function, the program might have to execute
the statements in another function. But while executing that new function, the
program might have to execute yet another function!

Fortunately, Javascript is adept at keeping track of where it is, so each time a
function completes, the program picks up where it left off in the function that
called it. When it gets to the end of the program, it terminates.

What's the moral of this sordid tale? When we read a program, don't read from
top to bottom. Instead, follow the flow of execution.

Functions that require arguments
---------------------------------------------

Most functions require arguments: the arguments provide for generalization, allowing the same
function to work with different data inputs.
For example, if we want to find the absolute value of a number, we have
to indicate what the number is. The Javascript `Math` class has a built-in function for
computing the absolute value:

```javascript        
⠕ Math.abs(5);
=> 5
⠕ Math.abs(-5);
=> 5
```


In this example, the arguments to the `abs` function are 5 and -5.

Some functions take more than one argument. For example the function `calculateTip`
function we wrote in the example above takes two arguments:
the amount of the bill and the percent tip to calculate.
Inside the function, the values that are
passed get assigned to variables called **parameters**.

```javascript
⠕ calculateTip(87, 10);
Bill amount: $87
Tip percentage: 10%
Total amount due: $8.70

```

Another built-in function that takes more than one argument is `Math.max`.

```javascript        
⠕ Math.max(7, 11);
=> 11
⠕ Math.max(4, 1, 17, 2, 12);
=> 17
⠕ Math.max(3 * 11, 5**3, 512 - 9, 1024**0);
=> 503
```

`Math.max` can be passed any number of arguments, separated by commas, and will
return the largest value passed. The arguments can be either simple values or
expressions. In the last example, 503 is returned, since it is larger than 33,
125, and 1. All of the expressions are resolved --- in this case the mathematical
operations are calculated --- before their values are assigned to the function
parameters.

Functions that return values
------------------------------------------------------------------------------

Some functions return values. In the previous section we saw that `Math.abs`
and `Math.max` return values. `calculateTip` does not return a value; it
uses `console.log` to produce output on the screen for the user.
We can use the return values from functions to compose more complex functions.

A function that returns a value is called a **fruitful function** in this book.
The opposite of a fruitful function is **void function** — one that is not executed
for its resulting value, but is executed because it does something useful.
(Languages like Java, C#, C and C++ use the term "void function", other languages like Pascal
call it a **procedure**.) Even though void functions are not executed
for their resulting value, Javascript always wants to return something. So if the programmer
doesn't arrange to return a value, Javascript will automatically return the value `undefined`.

How do we write our own fruitful function? Let's look at the standard
formula for compound interest as an example of a fruitful function:   

![](figs/compoundInterest.png)

{% include codepen.html user='thinkle' id='XWvBBKJ' %}

```javascript
/*
Apply the compound interest formula to p
to produce the final amount.
*/
const finalAmt = (p, r, n, t) => {
  let a = p * (1 + r/n) ** (n * t);
  // This is new, and makes the function fruitful
  return a;
}


//now that we have the function above, let's call it
let toInvest = Number.parseFloat( window.prompt("How much do you want to invest?") );
let fnl = finalAmt(toInvest, 0.08, 12, 5);
console.log("At the end of the period you'll have", fnl);
```

* The **return** statement is followed an expression (`a` in this case). This expression will be
  evaluated and returned to the caller as the "fruit" of calling this function.
* We prompted the user for the principal amount. The type of `toInvest` is a string, but
  we need a number before we can work with it. Javascript can automatically convert
  it to a number for us when we use it in the calculation. Because it is money, and could have decimal
  places, we've used the `Number.parseFloat` type converter function to parse the string and return a float.
* Notice how we entered the arguments for 8% interest, compounded 12 times per year, for 5 years.
* When we run this, if we enter `100` when prompted for the amount to invest, we get the output<br>
  _At the end of the period you'll have 148.9845708301606_<br>
  This is a bit messy with all these decimal places, but remember that
  Javascript doesn't understand that we're working with money: it just does the calculation to
  the best of its ability, without rounding. Later we'll see how to format the string that
  is printed in such a way that it does get nicely rounded to two decimal places before printing.
* The line `let toInvest = Number.parseFloat( window.prompt("How much do you want to invest?") );`
  also shows yet another example
  of *composition* — we can call a function like `Number.parseFloat`, and its arguments
  can be the results of other function calls (like `window.prompt`) that we've called along the way.

Notice something else very important here. The name of the variable we pass as an
argument — `toInvest` — has nothing to do with the name of the parameter
— `p`.  It is as if  `p = toInvest` is executed when `finalAmt` is called.
It doesn't matter what the value was named in
the caller, in `finalAmt` its name is `p`.  

These short variable names are getting quite tricky, so perhaps we'd prefer one of these
versions instead:       

```javascript
const finalAmtV2 = (principalAmount, nominalPercentageRate, numTimesPerYear, years) => {
  let a = principalAmount * (1 + nominalPercentageRate / numTimesPerYear) ** (numTimesPerYear * years);
  return a;
}

const finalAmtV3 = (amt, rate, compounded, years) => {
  let a = amt * (1 + rate / compounded) ** (compounded * years);
  return a;
}
```

They all do the same thing. Use your judgment to write code that can be best
understood by other humans!  
Short variable names are more economical and sometimes make
code easier to read:
<var>E = mc<sup>2</sup></var> would not be nearly so memorable if Einstein had
used longer variable names! If you do prefer short names,
make sure you also have some comments to enlighten the reader
about what the variables are used for.

-----------------------------------------------

When we declare a new **local variable** inside a function, it only exists inside
the function, and we cannot use it outside. For example, consider again this function:

```javascript

const finalAmt = (p, r, n, t) {
  let a = p * (1 + r/n) ** (n * t);
  return a;
}

```

If we try to use `a`, outside the function, we'll get an error like this:

```javascript        
⠕ a
ReferenceError: a is not defined
```

The variable `a` is local to `finalAmt`, and is not visible
outside the function.

Additionally, `a` only exists while the function is being executed —
we call this its **lifetime**.
When the execution of the function terminates, the local variables are destroyed.

Parameters are also local, and act like local variables.
For example, the lifetimes of `p`, `r`, `n`, `t`` begin when `finalAmt` is called,
and the lifetime ends when the function completes its execution.   

So it is not possible for a function to set some local variable to a
value, complete its execution, and then when it is called again next
time, recover the local variable. Each call of the function creates
new local variables, and their lifetimes expire* when the function returns
to the caller.

* Unless the function returns another function, in which case the local variables
  are kept alive as long as the returned function is still in use.

> *Local Variables*
>
> Actually, the keyword `let` (and the keyword `const`) define what
> are called *block-scoped* variables in JavaScript. The variable will
> be local to whatever block it's declared in, whether that block
> is part of a function or another structure such as an *if statement*,
> a *for loop* or a *while loop*.

Async/Await Functions
---------------------
JavaScript allows the keyword `async` before a function to indicate that the 
function will be called "asynchronously," which means it is not meant to 
return a value right away, but after a delay. This is a useful pattern when
your function needs to wait for something to happen, like a user to type a
message or a piece of data to load over a network.

The syntax for an asynchronous function is:

```javascript
const NAME = async ( PARAMETERS ) => {
  STATEMENTS
}
```

This function will return a `Promise` object, which is a special kind of object
that represents the eventual completion (or failure) of an asynchronous operation: in
practice, we will use the `await` keyword to wait for the result of asynchronous
functions.

In our TextInterface examples, all *input* calls are *asynchronous* functions,
which means any function you write *using* the input calls should also be 
asynchronous. You have to add the `await` keyword before any asynchronous call
to tell JavaScript to wait for the result, and you can *only* use the `await
keyword inside an `async` function.

```javascript
const ti = new TextInterface();

const getTotalPrice = async (price) => {
  ti.output("The subtotal is: "+price);
  let addTip = await ti.getYesOrNo("Do you want to add a tip?");
  if (addTip) {
    let percentTipAmount = await ti.promptNumber("What percentage tip will you add?");
    let tipAmount = (percentTipAmount/100) * price;
    return price + tipAmount;
  } else {
    return price;
  }
}
```

Anonymous Functions
----------------------------------
JavaScript allows what are called `anonymous functions` which means you don't have to 
name a function to use it. An anonymous function is a function that doesn't have the
`const` statement at all.

```(PARAMETERS) => { STATEMENTS }```

In addition, JavaScript arrow functions have a compact form that allows you to omit
the brackets if your function only consists of a single statement. Arrow functions *without* 
brackets are *all* **fruitful functions**: they return the result of the single statement.

```(PARAMETERS) => RETURN_VALUE```

Why would we use an anonymous function? There are numerous examples, such as when we pass
a function to another function as a parameter. 


Another example would be the one you've seen
in the `TextInterface` examples in this book, where we use what's called an *immediately invoked
function expression* to create and run a function in one statement. These are useful when we want
to use the `async/await` syntax, which is not always allowed outside of function calls (the full
explanation with async/await is more complicated, but beyond the scope of this chapter).

Here's an example of an anonymous function being used with the `setTimeout` function, a built
in function in JavaScript which allows us to run a function after a delay. The syntax for 
setTimeout is:

```javascript
setTimeout(FUNCTION, DELAY_IN_MILLISECONDS)
```

```javascript
setTimeout(
  () => {
    window.alert("It's been 10 seconds!");
  },
  10000 
);
```

Here's the syntax for an IIFE like we've been using in the Codepen examples in this book:

```javascript
(async () => { 
  STATEMENTS
})();
```

Notice that the parentheses *after* the expression mean the function is called immediately after
it is defined.

Here is an example which puts together *all* of the concepts we've just introduced (IIFE, anonymous 
functions, async/await):

{%include codepen.html user='thinkle-iacs' id='qBeGoeK' %}

```javascript
// Immediately Invoked Function Expression
(async () => {
  const ti = new TextInterface.TextInterface();
  // Await keyword used with TextInterface input
  const delay = await ti.promptNumber("How many seconds should I wait?");
  // Set timeout called with an anonymous function
  setTimeout(
    () => ti.output("It has been " + delay + " seconds!"),
    delay * 1000
  );
  ti.output("Waiting...");
})();
```

> *Anonymous Functions and Style*
>
> Any place you put an anonymous function, you can *also* put a named
> function. So why use an anonymous function? The answer is that it can
> make your code more readable. If the function is only used in one place,
> and is simple, it can be easier to read if you don't have to scroll up
> to find the function definition. If the function is more complex, or
> used in multiple places, it is better to give it a name.



Glossary
-------------------------------

---
**argument**

A value provided to a function when the function is called. This value
    is assigned to the corresponding parameter in the function.  The argument
    can be the result of an expression which may involve operators,
    operands and calls to other fruitful functions.

---
**body**

The second part of a compound statement. The body consists of a
    sequence of statements wrapped in curly brackets `{...}`. Each
    statement ends with a semicolon.    

---
**compound statement**

A statement that consists of two parts:

    1. header - which begins with a keyword determining the statement
       type (`function`, `if`, `while`)
    2. body - begins with a left curly bracket `{`, contains one or
       more statements ending with a semicolon `;`, and ends with a
       right curly bracket `}`.

    The syntax of a compound statement looks like this:

```javascript
    keyword ... {
        statement;
        statement; 
        ...
    }
```

---
**flow of execution**

The order in which statements are executed during a program run.

---
**frame**

A box in a stack diagram that represents a function call. It contains
    the local variables and parameters of the function.

---
**function**

A named sequence of statements that performs some useful operation.
    Functions may or may not take parameters and may or may not produce a
    result.

---
**function call**

A statement that executes a function. It consists of the name of the
    function followed by a list of arguments enclosed in parentheses.

---
**function composition**

Using the output from one function call as the input to another.

---
**function definition**

A statement that creates a new function, specifying its name,
    parameters, and the statements it executes.

---
**fruitful function**

A function that returns a value when it is called.

---
**header line**

The first part of a compound statement. 

---
**import statement**

A statement which permits functions and variables defined in another JavaScript
module. To import the turtle or TextInterface library, we began with an import
statement.

---
**lifetime**

Variables and objects have lifetimes — they are created at some point during
    program execution, and will be destroyed at some time.

---
**local variable**

A variable defined inside a function. A local variable can only be used
    inside its function.  Parameters of a function are also a special kind
    of local variable.

---
**parameter**

A name used inside a function to refer to the value which was passed
    to it as an argument.

---
**refactor**

A fancy word to describe reorganizing our program code, usually to make
    it more understandable.  Typically, we have a program that is already working,
    then we go back to "tidy it up".  It often involves choosing better variable
    names, or spotting repeated patterns and moving that code into a function.    

---
**stack diagram**

A graphical representation of a stack of functions, their variables,
    and the values to which they refer.

---
**traceback**

A list of the functions that are executing, printed when a runtime
    error occurs. A traceback is also commonly referred to as a
    *stack trace*, since it lists the functions in the order in which they
    are stored in the
    [runtime stack](http://en.wikipedia.org/wiki/Runtime_stack).

---
**void function**

The opposite of a fruitful function: one that does not return a value.  It is
    executed for the work it does, rather than for the value it returns.

Function Exercises
------------------

1.  Write a void (non-fruitful) function to that prints out a "hello" message. Your function
    should declare 3 parameters: `firstName`, `lastName`, and `title`. `title` will be
    Mr., Ms., Dr., etc. The function should print a message like this one:
    `Hello Dr. Matthew Curinga.`


2. Write a function `half(num)` which returns the value of `num` divided by 2.

3. Write a function `triple(num)` which return `num` * 3.

4. Write a function `areaOfACircle(r)` which returns the area of a circle of radius `r`.
   For the value of PI, use the constant `Math.PI`<br>
   (Hint: if you can't remember how to find the area of a circle, look it up or ask a friend.)

5. Write a function `hypotenuse(a, b)` which calculates the hypotenuse of a right triangle
   when given the length of sides `a` and `b`.
   Use the [Pythagorean theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem) `a^2 + b^2 = c^2`.<br>
   Note, you will need to be able to calculate square roots to solve this problem.
   You can use the built-in math function `Math.sqrt`.

6. (hard bonus) Write a function called `distance(x1, y1, x2, y2)` which calculates the
   distance between the point at (x1, y1) and (x2, y2) on a Cartesian Plane. You can
   find the formula for this at <http://www.mathsisfun.com/algebra/distance-2-points.html><br>
   Use the `hypotenuse` function from exercise 5 to compose this function.


Functions Lab
-------------

This is the first "lab" in our textbook. For this project, you will be asked to write
a complete program that solves a problem. The labs should break up parts of the program
into different functions. Your program should start when the `main()` function is
called. `main` is not a keyword in Javascript, but in many programming languages there
is a convention that the starting function is called `main`. Please take a look at the
Tip Calculator case study below for a sense of how your program should be structured.

For this first lab, too, please pay attention to your [coding style](#coding-style) to
make sure that the program is well formatted and easy for human readers to understand.

For this lab you are going to revisit the lemonade stand estimator from the exercises in
chapter 2. You will make an interactive program that asks the user to enter all of the
data for:

- prices of the ingredients
- prices for the materials (e.g. cups)
- sale price for a cup of lemonade
- and estimation of the number of cups sold

Once all of the data is entered, the program will print out a neatly formatted message
with the results of the estimation.
