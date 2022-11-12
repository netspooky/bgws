# Background

This section will run down a lot of the fundamental concepts for doing binary golfing and file format hacking in general. 

## What is Binary Golf?

<img width="50%" src="https://user-images.githubusercontent.com/26436276/201183059-c62bac7d-1808-46be-bc03-9cce3ca49cbd.png">

Binary golf is the practice of crafting small but functional files. Similar to [code golf](https://codegolf.stackexchange.com/) and [size coding](http://www.sizecoding.org/wiki/Main_Page), the goal is to create the smallest possible valid file. In the sport of golf, your goal is to get the ball into the hole in as few swings as possible.

Binary can mean both binary in the executable sense, and binary as in the data type. You create the smallest possible sequence of binary digits that can sufficiently represent a given thing.

## What even is a file?

The word file means different things to different people. For our purposes, a file is a simply a sequence of bytes. File format specifications are essentially a set of rules that tell a computer how it should parse and interpret this sequence of data. We can think of a file as a set of instructions that tell a computer to do something. Using the established rules, we can use a file to make the computer do something expected, or something entirely unexpected.

![sotn-Dracula What is a file A miserable little pile of parsing instructions](https://user-images.githubusercontent.com/26436276/200395736-45d10ade-3ee8-4545-9894-7f644a7297bd.png)

File formats can contain chunks that each follow specific rules on how to process them. Some chunks are simply informational and provide context to understand the file, while others contain data.

![image](https://user-images.githubusercontent.com/26436276/201205159-8b925ff8-af47-43be-9b63-6e8217f9348b.png)

Many file formats can also contain pointers to other data areas in the file. You can think of these almost like a map that you can follow!

## Why Golf?

This seems all well and good, but you may be asking yourself "why?". Aside from the obvious "why not?", there are actually quite a few answers to this question.

- Save disk space, network bandwidth, memory usage
- Fit the file into a small space (such as a flash memory chip)
- Reduce the amount of time it takes to read and write the file
- Obfuscate files
- Make files multi-functional
- Establish optimizations as a known trick, or even get added to a new version of the spec

Throughout the history of computing, engineers, scientists, and everyday people have battled with resource limits. Whether it's disk capacity, network throughput, memory, computing power, or even physical limitations, these constraints have influenced the way we interact with machines.

On top of these constaints also come the standards and best practices that have been cultivated. These are things like standard data sizes, byte order, file format and protocol limitations, and operating system resource limits, which we may take for granted due to their ubiquitous nature.

Everything from critical power grid infrastructure to the device you are reading this on must all agree on ways to communicate. Not everything is black and white though. There is a lot of grey area in what is already established that we can explore.

## About Complexity

Finding the shortest ways to represent a file has parallels to a problem called [Kolmogorov Complexity](https://en.wikipedia.org/wiki/Kolmogorov_complexity). 

Taken from Wikipedia:

> In algorithmic information theory (a subfield of computer science and mathematics), the Kolmogorov complexity of an object, such as a piece of text, is the length of a shortest computer program (in a predetermined programming language) that produces the object as output.
> 

In simple terms, this means that the more complex a stream of data is, the more difficult it is to find ways to compute it. This makes finding ways to shrink, combine, and overlay files very difficult to do with a computer alone.

This is an adaptation of the Wikipedia example:

Imagine we have two strings. How would you write a short program to generate them?

```
string1 = "abababababababababababababababab"
string2 = "4c1j5b2p0cv4w1x8rx2y39umgw5q85s7"
```

If we use python as our language, we can simplify strings like this.

```python
def printString1():
    print("ab"*16)

def printString2():
    print("4c1j5b2p0cv4w1x8rx2y39umgw5q85s7")
```

string1 can be printed with far less code than string2. 

Files can be thought of in a similar way. As data areas get largers and structures require more complexity, the ability to optimize a file may become more and more difficult, even with the aid of a compiler or other tool responsible for constructing a file.

There are many types of problems like this that aren’t easy for even machines to solve. You may find it humbling, that despite our ability to explain and analyze so many mechanisms of our world, there will always be new ways of optimizing and pushing the limits. Hackers explore these things for the art.

## Practical Example: Minification

![image](https://user-images.githubusercontent.com/26436276/201166735-5e9c3569-2e14-42d4-9701-ea62461f45c6.png)

Okay enough of this lofty talk, what's a real world example of this? An easy answer is something you likely experienced while loading this page: file minification.

When you "minify" a file, you remove all of the excess bits that you technically don't need, or that the file parser doesn't seem to care about. 

Much of the web runs courtesy of javascript which runs on your machine. Javascript programs are text files that are referenced by other web pages or scripts, which make web requests to fetch them from their server. Every character in the text file costs around 1 byte to send (assuming you are using ASCII and not another encoding).

This is an example of a piece of Javascript that adds two numbers and displays them in the page:

```javascript
var num1 = 10;
var num2 = 40;
var sum  = num1 + num2;
document.write("Sum of 10 and 40 is: " + sum);
````

It's a fairly short program, clocking in at 100 bytes. If we take out some of the unnecessary components, we can get it down to just 58 bytes.

```javascript
a=10;b=40;c=a+b;document.write("Sum of 10 and 40 is: "+c);
```

That's a 42% decrease in the size. Imagine you have a server that needs to send this script to 1 million computers a day. Reducing cost by 2/5 would start to make a huge difference. 

Minification is a fairly common practice, you may have seen scripts like jquery.min.js, which is pretty much this but with a whole library that many websites use.

Further Reading
- https://webplatform.github.io/docs/concepts/programming/javascript/minification/
- https://en.wikipedia.org/wiki/Minification_(programming)

---

Prev: [Intro](00_introduction.md) | Next: [Fundamentals](02_fundamentals.md)
