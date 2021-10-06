# The Weird Javascript

This is [Mehedi hasan Shifat](https://www.github.com/jspw). I am trying to write about the things I feel **weird** about javascript (not saying bad :3). i will write something about javascript everyday whenever I get some free time.

**Note** : This is not a blog/article/repo to learn javascript. you can get some awesome blogs and video playlists about javascript which are really awesome.

# Table of Contents

- [The Weird Javascript](#the-weird-javascript)
- [Table of Contents](#table-of-contents)
  - [Contents](#contents)
    - [Hoisting](#hoisting)
          - [code-01](#code-01)
          - [code-02](#code-02)

## Contents

### Hoisting

At first forget about the section title. Let's look at some code snippets.

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

**Great!** if it matches with you thinking, if doesn't then let's discover the mystery of bermuda triangle :D

If **javascript**(hight level language) is your first one & only language then may be you will find it normal\* but people like us coming from a low level language like **C** will find this fucking weird :3

It's all about **hoisting**. Javascript moves declarations(like var num) to the top. So actually what / how the code was we can say like this :

```js
var num = undefined;
num = 10;
console.log(num);
```

Then why in the [first example](#code-01) it printed `undefined` ?Actually in the [first example](#code-02) the code were executed like this :

```js
var num = undefined;
console.log(num); // so it was undefined when we were logging num
num = 10;
```

If we look at the code carefully we can see that, at the [first code](#code-01) snippet, we print the value of num before store the value when it was undefined.But in the second case it was already initialized.

**Note** : This is not the actual scenario but something like this was happened. And one thing more about the words `insert` and `initialize` value to a variable , we will talk about it later.
