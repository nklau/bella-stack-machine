![Logo](https://raw.githubusercontent.com/rtoal/bella/main/docs/bellalogo.png)

# Bella

A simple programming language, used for a compiler course.

```
let dozen = 12;
print(dozen % 3 ** 1);
function gcd(x, y) = return y == 0 ? x : gcd(y, x % y);
while (dozen >= 3 || (gcd(1, 10) != 5)) {
  let y = 0;
  dozen = dozen - 2.75E+19 ** 1 ** 3;
}
```

## Language Specification

The language is specified at its [home page](http://cs.lmu.edu/~ray/notes/bella/).

## Building

Nodejs is required to build and run this project. Make sure you have a recent version of Node, since the source code uses a fair amount of very modern JavaScript.

Clone the repo, then run `npm install`.

You can then run `npm test`.

## Usage

To run from the command line:

```
node src/bella.js <filename> <outputType>
```

The `outputType` indicates what you wish to print to standard output:

<table>
<tr><th>Option</th><th>Description</th></tr>
<tr><td>parser</td><td>A message saying the syntax is ok or that there is an error</td></tr>
<tr><td>analyzed</td><td>The decorated AST</td></tr>
<tr><td>optimized</td><td>The optimized decorated AST</td></tr>
<tr><td>js</td><td>The translation of the program to JavaScript</td></tr>
</table>

Example runs:

```
$ cat examples/small.bella
let x = sqrt(9);
function f(x) = 3 * x;
while (true) {
  x = 3;
  print(0 ? f(x) : 2);
}
```

```
$ node src/bella.js examples/small.bella parsed
Syntax is ok
```

```
$ node src/bella.js examples/small.bella analyzed
   1 | Program statements=[#2,#6,#10]
   2 | VariableDeclaration variable=#3 initializer=#4
   3 | Variable name='x' readOnly=false
   4 | Call callee=#5 args=[9]
   5 | Function name='sqrt' paramCount=1
   6 | FunctionDeclaration fun=#7 params=[#8] body=#9
   7 | Function name='f' paramCount=1
   8 | Variable name='x' readOnly=true
   9 | BinaryExpression op='*' left=3 right=#8
  10 | WhileStatement test=true body=[#11,#12]
  11 | Assignment target=#3 source=3
  12 | PrintStatement argument=#13
  13 | Conditional test=0 consequent=#14 alternate=2
  14 | Call callee=#7 args=[#3]
```

```
$ node src/bella.js examples/small.bella optimized
   1 | Program statements=[#2,#4,#8]
   2 | VariableDeclaration variable=#3 initializer=3
   3 | Variable name='x' readOnly=false
   4 | FunctionDeclaration fun=#5 params=[#6] body=#7
   5 | Function name='f' paramCount=1
   6 | Variable name='x' readOnly=true
   7 | BinaryExpression op='*' left=3 right=#6
   8 | WhileStatement test=true body=[#9,#10]
   9 | Assignment target=#3 source=3
  10 | PrintStatement argument=2
```

```
$ node src/bella.js examples/small.bella js
let x_1 = 3;
function f_3(x_2) {
return (3 * x_2);
}
while (true) {
x_1 = 3;
console.log(2);
}
```

## Contributing

I’m happy to take PRs. As usual, be nice when filing issues and contributing. Do remember the idea is to keep the language tiny; if you’d like to extend the language, you’re probably better forking into a new project. However, I would love to see any improvements you might have for the implementation or the pedagogy.

Make sure to run `npm test` before submitting the PR.

![GoodDog](https://raw.githubusercontent.com/rtoal/bella/main/docs/bella.jpg)
