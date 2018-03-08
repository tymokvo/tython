# tython
A little language goes a long way.

## purpose

This is my attempt to write a programming language to...

* ...learn more about programming, esp the nitty gritty
  * compilers?
  * parsing?
  * bootstrapping!?
* ...make a language that I like
  * I find the syntax of most languages confusing
  * Even friendly ones like Python and Ruby
* ...have fun!

## mission

1. Clarity/Readability
  1. It seems to me that we are at a point where most 2<sup>nd</sup> order high-level languages have had to adopt syntactical kludges due to their explosive use in production since the dawn of the internet. They approach this in several ways.
    1. Javascript lets anything go
    2. Python has an oligarchy
    3. Ruby leaves it up to you
  2. So now there are Rust and Go.
    1. I don't know anything about Go.
    2. Rust takes things from JS, Python, C++, OCaml?
      1. The more I learn, the more it feels like a missed opportunity
      2. But I also don't really know anything about it
2. Fast
  1. To learn
    1. The faster you can get your ideas into a testable state, the faster you can run them against the real world. This accelerates the theory -> experiment -> better theory -> ... loop
  2. To write
    1. syntax should be minimal
  3. To execute
    1. Make it work/satisfying to look at
    2. Make it fast

## syntax ideas

There should be minimal entropy between a directive in human language and its resolution into the language's syntax. It should feel natural for people who can construct logical arguments in their language to write programs in this language.

Variables should be statically-typed. I like that this forces you to turn ideas into datatypes in order to take seriously how you represent the world as data. After all the goal of programming is to take the state of the world, store it, reorganize/reshape it, and look at it again. This also serves point `3.2` above.

#### Literals

```
0
3.1415927
'hello, world'
00 # or # FF
```

#### comments
```
# <- that begins a comment, this ends it -> #
#
as such they can always be
multi-line comments
#
```
### assignment

Dear Computer,

I would like to create an integer, reference it by the symbol 'x' and assign to it the value `0`.

```
x<int> <- 0
```
or maybe require instantiation like Smalltalk...
```
x<int>
x <- 0
```

I like this one because it ***looks like what it is doing***. I think that this is an important point. Assignment in most languages (with which I am familiar) looks like equations:
```
python
x = 0

javascript
int x = 0;

rust
let x = 0;
or
let mut x = 0;
```
I think this is conceptually weird. `x` is not "equal" to `0`, it is a name to refer to, or a container for `0`. Thus, I think the arrow assignment `->` makes more sense. I think it can also be bidirectional, to let the programmer "think how they think" and use the language as feel natural to them. So
```
x<int>
x <- 0 # an integer named 'x' takes in the value '0' #
0 -> x # the value 0 is put into 'x' which is capable of holding an integer #
```
It may actually make more sense to declare type before all else. In this way, it can be statically typed and look like what it is doing.
```
<int>x <- 0
# or #
<int>x
x <- 0
```

### collections

Everything should be a collection. This is where I think there is something new to add. I think we should use a ***set-first*** mentality. e.g. this should work: (not sure about the more complicated syntaxes yet)
```
<int>x
x <- 0
0 \in x
>>> true

for element in x:
  print element
>>> 0
```
What this means is that:
```
<int>x
x <- 0
```
is equivalent to:
```
<set><int>x
x[0] <- 0
```
Ergo, everything is a collection to the point that all literals are superclasses of `<set>`

Why do this? Two reasons:
1. Computers are constructed from memory. This is just multi-dimensional set of physical locations in which we store things. The language puts this at the forefront of how to think.
2. I think this makes it easier to do the really cool stuff like geometry, graphics, and deep learning. All of these things rely on really fast array manipulation, and my goal is to translate that computation into a near-human langugage.

These things probably make this close to being a functional language. And indeed, I am tempted to say that there should be ***no methods***. There should be only **objects** and **actions**. Again, I think the goal of this is a kind of computational/physical hybrid language with which to think.

So, **objects** hold sets of similar information. While **actions** define computation, or ways in which we manipulate objects.

This means that we would translate the above:
```
0 \in x
```
into English as "Take the literal integer `0` and see if it is in the thing called `x`." In the language `0` and `x` are objects which superclass `<set>` and `\in` is an *action* that holds an algorithm for determining if the object on the left is contained in the object on the right. In the structure that I have defined so far, I think this means that:
```
x \in 0
```
would evaluate to `true` since they are both `<set>` of rank `1` that hold the integer `0`

I'm not sure about this syntax though. This is where it starts to get complicated. I think it might be a good idea to think of sets as equivalent to databases, and all actions to be structured as queries:
```
0 in? x
```

### sets

I guess this implies that the `<set>` object is equivalent to a pointer or a memory location. This means that it has a lot of work to do to abstract this away.

### modules/builtins

I think the package/module system is better than monolithic languages like Mathematica or Matlab.

That said, I like that Mathematica/Matlab roll all of their abilities up in a cohesive package. I wonder if this can be extended to this language working in environments.

So the `<set>` idea is extended to an environment just being a `<set>` of packages that contain a `<set>` of objects and actions.
