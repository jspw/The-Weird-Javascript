# The Weird Javascript

This is [Mehedi Hasan Shifat](https://www.github.com/jspw). I am trying to write about the things I feel **weird** about javascript (not saying bad :3). i will write something about javascript everyday whenever I get some free time.

**Note** : This is not a blog/article/repo to learn javascript. you can get some awesome blogs and video playlists about javascript which are really awesome.

# Table of Contents

- [Contents](#contents)
  - [Undefined | Error ?](#undefined-error)(being written )
  - [Betrayal of Switch-Case](#betrayl-of-switch-case)(to be added)
  - [Reference in Javascript](#reference-in-javascript)(to be added)
  - [Type](#type)(to be added)

## Contents

### Undefined || Error ?

Let's look at some code snippets.

###### code-01

```js
console.log(num);
num = 10;
var num;
```

Guess, what is the output of the code ?
Is it a `compilation error` ? just kidding :v

output :

```
undefined
```

It says `undefined`. Okey, let's take another look -

###### code-02

```js
num = 10;
console.log(num);
var num;
```

Guess again `undefined` ? Shouldn't it be `undefined` as the variable `num` is declared after the `console.log()` ? or the code should break as `10` is inserted(? will talk about later) into `num` before initializing it ?

output :

```
10
```

**Great!** if it matches with your thinking, if doesn't then let's discover the mystery of bermuda triangle :D

If **javascript**(hight level language) is your first one & only language then may be you will find it normal\* but people like us coming from a low level language like **C** will find this fucking weird :3

It's all about **hoisting**. Javascript actually split the initialization and declaration and moves declarations(like var num) to the top. So actually what / how the code was we can say like this :

```js
var num = undefined;
num = 10;
console.log(num);
```

So for `var` a variable is declared with `undefined` at the top, then when the line of declaration comes it assign value to it.

Then why in the [first example](#code-01) it printed `undefined` ?
If we look at the code carefully we can see that, at the [first code](#code-01) snippet, we print the value of num before store the value when it was undefined.But in the second case it was already initialized.
Actually in the [first example](#code-02) the code were executed like this :

```js
var num = undefined;
console.log(num); // so it was undefined when we were logging num
num = 10;
```

**Note** : This is not the actual scenario but something like this was happened. And one thing more about the words `insert` and `initialize` value to a variable , we will talk about it later.

For that reason we can call a function in js before initializing it like this -

###### code-03

```js
printSum(100);

function printSum(n) {
  // print sum of 1 to n
  console.log((n * (n - 1)) / 2);
}
```

Let's find some corner cases how can we declare (?) or initialize variables in js.

###### code-04

```js
num = 10;
console.log(num);
```

Now i have just removed `var` from the previous code ([code-02](#code-02)). will it run properly ? Is it undefined for hoisting ? or `Reference error` ?

output :

```
10
```

As there is no `var num` in our code there is no hoisting. It just initialized x. This could be a different scenario if we were using `strict` mode. Strict mode is a feature of ES5. It applies some restrictions.

```js
"use strict";
num = 10;
console.log(num);
```

In this case we will get `ReferenceError: num is not defined`

You can also set strict mode for individual functions too.

```js
var note = "The whole script is not in strict mode now";

function strictMode() {
  "use strict";
  // do your stuffs
}
```

We have learnt about hoisting. Javascript has now a few more declaration keys like the weird `var` , they are `let`, `const`. Why the hack we need let or const as we already have var ? We have enough weirdness in js, why adding some more?

Wait, think positive. May be it can save us from the devil var :3

Before going to `let` & `const`, let's observe some weirdness of `var` and why `var` is the devil :3

###### code-05

```js
var x = 10;
var x = "hello";
var x = true;
console.log(x);
```

What the hack is this ? I have initialized x with 10 which is a number , then again with "hello" string and at last with a boolean true. Is the program runnable ? `error` `error` `error` ? `reference` error ?

Let's see the output :

```
true
```

For hoisting, `x` was declared at the top before execution and then it was initialized with 10,"hello" and true accordingly.As at the last before logging it was a boolean, it printed `true`.

`var` actually declares a function-scoped or globally-scoped variable. There are some interesting facts here. Using`var` for declaration javascript moves the declaration at the top of the function(\*) actually. Let's see the code -

###### code-06

```js
function foo() {
  var x = 10;

  if (x > 50) {
    var x = 51;
  } else {
    var x = -1;
  }

  console.log(x);
}

foo();
```

output :

```
-1
```

Inside the function its always the same `x`.

###### code-07

```js
function goo() {
  var x = 10;
  function foo() {
    var x = 20;
  }
  foo();
  console.log(x);
}
goo();
```

Can you guess the output this time ? `20` haa ??

Output :

```
10
```

Shouldn't surprise as I have told before that `var` declares a function scoped variable so `x` inside `foo` is hoisted at the top of the `foo` function not globally. That's why global `x` and `x` inside `foo` is not same.Let's see another example -

###### code-08

```js
var x = 10;
function foo() {
  var y = 10;
}
foo();
console.log(y);
```

Output :

```js
ReferenceError: y is not defined
```

YES! Successfully created a `reference error` again :3

You can't access a variable out of its scope, and thats actually gooood!

here is a nested functional scope example of var -

###### code-09

```js
function google() {
  function foo() {
    var y = 10;
    function bar() {
      var p = 12;
      console.log("value of y : ", y); // will print 10
    }
    bar();
    console.log("value of p : ", p); // reference error for p
  }
  foo();
}
google();
```

Actually when we declare a variable it is available everywhere in the scope as well as any lower/child/inner scopes.

Beside that, as we can see declaring variables with `var` is risky. There is a very good possibility of using the same name of two different variables for different task and it can produce a bug which will be difficult to find out and fix it.

To solve this problem, they introduced `let`. `const` is the constant form of `let` actually.

In mathematics we used to say, `let x .....`. Most languages like **Scheme** adopt let from mathematical statement. If you have done some study on `how js was created or how`, it will be more clear to understand. btw **Scheme** has also `let*`.

Let's rewrite some of the previously written code snippets with `let`.

###### code-10

```js
console.log(num);
let num = 10;
```

Output :

```
ReferenceError: Cannot access 'num' before initialization
```

###### code-11

```js
let x = 10;
// .......
// .......
// .......
// .......
let x = "shifat"; // SyntaxError: Identifier 'x' has already been declared
```

###### code-12

```js
let num = 10;
if (1) {
  let num = 1000; // num is a new variable here ,not the global one
}

console.log(num);
```

output :

```
10
```

`let` declares block-scoped which is limited to the scop of the block.The variable is said to be in a "temporal dead zone" (TDZ) from the start of the block until the initialization has completed. The variables are not accessible until fully initialization. `let` saves us a lot. Most of the weird stuffs of `var` is covered with `let` . So its safer to use `let` then `var`.
