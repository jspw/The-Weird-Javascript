This is [Mehedi hasan Shifat](https://www.github.com/jspw). I am trying to write about the things I feel **weird** about javascript (not saying bad :3). i will write something about javascript everyday whenever I get some free time.

**Note** : This is not a blog/article/repo to learn javascript. you can get some awesome blogs and video playlists about javascript which are really awesome.

# Table of Contents

- [Table of Contents](#table-of-contents)
  - [Contents](#contents)
    - [Hoisting](#hoisting)
          - [example-1](#example-1)
          - [example-2](#example-2)

## Contents

### Hoisting

###### example-1

```js
console.log(num);
num = 10;
var num;
```

Guess what is the output ? `compilation error` ? just kidding :v

output :

```
undefined
```

It says `undefined`

Let's take another look

###### example-2

```js
num = 10;
console.log(num);
var num;
```

`undefined` again? shouldn't it be `undefined` as the variable `num` is declared after the `console.log()` ? or the code should break as `10` is inserted(?) into `num` before initializing it ? Let's see the output :

```
10
```

If **javascript**(hight level language) is your first one & only language then may be you will find it normal\* but people like us coming from a low level language like **C** will find this fucking weird :3

It's all about **hoisting**. Javascript moves declarations(like var num) to the top.
So actually what / how the code was we can say like this :

```js
var num = undefined;
num = 10;
console.log(num);
```

Then why in the [first example](#example-1) it printed `undefined` ?Actually in the [first example](#example-2) the code were executed like this :

```js
var num = undefined;
console.log(num); // so it was undefined when we were logging num
num = 10;
```
