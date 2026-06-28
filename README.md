# Semantica Language Specs

[transpiler and specs here](http://semantica.replit.app)

Welcome to the specifications of the **Semantica programming language**. These specs will walk you through Semantica's unique syntax, program structure, and features, using enclosed examples

**Semantica** is designed with a primary goal: to make **AI coding** easier, much like natural writing. This is achieved through a few core syntactical changes that streamline the AI development process

\---

## 1\. The Basics: Syntax \& Variables

First, let's cover the fundamental building blocks of the Semantica language.

### Key Concepts

**It's time to change syntax of programming languages**

* **First: New Assignment Operator:** The most significant change is the assignment operator. Instead of `variable = value`, Semantica uses `value > variable`. This allows for a natural left-to-right flow mimicking handwriting. For example: `a + b > a`. in conditionals symbol `>` is 'greater than' comparison, everywhere else - assignment operator

* **Second: Renamed Keywords:** 
  * if - when
  * else - other
  * while - repeat
  * for - iterate
  * function - sub (subroutine)
  * return - back

* **Third: Semitagged Keywords:** Control flow and structural keywords are started and ended with symbol "|", much like a markup language. Examples include `repeat|`...`|repeat` , `sub|`...`|sub` , and `when|`...`|when` This makes it easy to find mistakes. So, blocks are explicit and self-closing with pipes.

* **Comments:** Single-line comments begin with `//`.

### Data Types & Operators

Semantica supports standard data types:

* `int`: integer
* `float`: float decimal
* `char`: character
* `string`: vector of "char"
* `bool`: boolean "true" or "false"

It also supports standard arithmetic operators: `+`, `-`, `*`, `/`, and `%` (mod) .

### Variable Declaration

You can declare a variable with or without an initial value

* **Declaration only:** `int i`
* **Declaration with initialization:** `int i(0)` (i becomes 0)   , `char c("a")`   , `bool l(true)`   , `string s("abcde")` .

\---

## 2\. Program Structure \& Functions

Semantica programs are organized into modules and functions.

### Modules

A program is defined within a `module|` block.

```Semantica
module| Euclidean 		// module itself
    ...
|module
```



### Function Declaration

Function declarations are also reversed to fit the left-to-right flow .

* **Syntax:** `sub|   <input_parameters> > <function_name> : <return_type>`
* **Example:** `sub| int a, int b > Euclid : int`   (This declares a function named `Euclid` that takes two `int` parameters and returns an `int` ).
* **Calling a function:** `a, b > f`

### The `main` Function

The entry point for your program is the `main` function.

* **Declaration:** `sub|  string args| | > main : int`

### Example 1: `Euclidean` Program

This full example demonstrates a simple module, function declaration, and Semantica's powerful I/O syntax.

```Semantica
module| Euclidean 		// module itself

    sub| int a, int b > Euclid : int  // function with type int
							
	repeat| b!= 0
		when| a > b
			    a - b > a
		    other|
			    b - a > b
		    |other
    	|when
	|repeat

	back| a |back     //this return of value by function, not a vector

    |sub

  
  sub|	string args| | > main : int	// main function

	int a, b

    in > a , b > Euclid > out

    // combined input and output and subction call
  // seamless input to output syntax

  |sub

|module
```



Notice the line: `in > a , b > Euclid > out`. This single line seamlessly:

1. Takes input (`in`)
2. Assigns it to variables `a` and `b`
3. Passes `a` and `b` to the `Euclid` function
4. Takes the return value from `Euclid`
5. Sends that result to output (`out`)

Here, in control flow of program: input, function call and output are seamed together in one transparent **Semantica** motion, allowing coding in the direction from left to right , like in regular handwriting

\---

## 3\. Control Flow & Vectors

Semantica provides standard control flow mechanisms and vector support.

### Conditional: `when|` / `other|`

The `Euclidean` example shows a simple `when|` / `other|` block.

```Semantica
when| a > b
        a - b > a
    other|
        b - a > b
    |other
|when
```



### Loop: `repeat|`

The `Euclidean` example also uses a `repeat|` loop.

```Semantica
repeat| b!= 0
    ...
|repeat
```



### Vectors

* We use vectors instead of arrays because they are more efficient
* Notice | | brackets instead of [ ]

  * **Declaration:** `int a|n|` (declares an integer vector with `n` elements).
  * **Initialization:** `int a|4|(|1, 2, 3, 4|)`.
  * **Access:** `a|i|` (0-based indexing).

### Loop: `iterate|`

Semantica has a specific syntax for `iterate|` loops .

* **Syntax:** `iterate|int i(0)++ <n`
* **Explanation:**

  * `int i(0)`: The iterator `i` is declared and initialized to 0 .
  * `++`: The iteration step is by 1 .
  * `< n`: The loop continues as long as `i` is less than `n` .

Here is an example of a `iterate|` loop used to populate an vector:

```Semantica
iterate| int k(0)++ < n       // fill with true
    true > primes|k|
|iterate
```



\---

## 4\. Advanced Example: Sieve of Eratosthenes

The following program, `primes`, uses vectors and loops to implement the Sieve of Eratosthenes algorithm.

```Semantica
module| primes 

        sub| int n > Eratosthenes : int       // function declaration
             
            bool primes | n |        // variable declaration
            int l(0), i(0), index_square(3)         

            int first, last, factor 

            iterate| int k(0)++ < n       // fill with true
                true > primes|k|
            |iterate   
                
            repeat| index_square < n         
                when| primes|i|             

                    0 + index_square > first
                    0 + n > last  
                    i + i + 3 > factor
                    false > primes|first|  

                    repeat| last - first > factor 
                        first + factor > first
                        false > primes|first|   
                    |repeat
                    
                |when  
                i + 1 > i 
                2 * i * (i + 3) + 3 > index_square   

            |repeat          

            ' 2' >  out  // print out

            iterate| i(0)++ < n         // print out
                when| primes|i| 
                    when| 2 * i + 3 > n 
                         break
                    |when

                    ' ' 2 * i + 3  >  out
                    l + 1 > l
 
                    when| l % 10 == 0 
                        '\n'  >  out
                    |when   
          
                |when        // when
            |iterate         // print out

            '\n number: ',  l  >  out

        |sub            // erato sub
     
        sub|  string args| | > main : int 		// main function
 
                   1000 > Eratosthenes       // function call

        |sub

|module
```



This example demonstrates vector manipulation (e.g., `false > primes|first|`), nested loops (`repeat|` inside `repeat|`  ), and sending formatted output to the console (e.g., `'\\n' > out` ).

\---

## 5\. Object-Oriented Programming: Classes

Semantica also supports classes, allowing for object-oriented design.

* **Declaration:** `class| ClassName ... |class`.
* **Members:** You can define data members (e.g., `int a, int b`)   and member functions (e.g., `sub| ...: Euclid`)  inside a class.
* **Object Creation:** `GCD N` creates an instance (object) `N` of the class `GCD`.
* **Access:** Members are accessed using the dot operator (e.g., `N.a`, `N.Euclid`).

### Example 3: `GCD` Class

Here is the `Euclidean` algorithm refactored into a class.

```Semantica
module| Euclidean

    class| GCD    //class declaration

        int a, int b    //data members

        sub| int a, int b > Euclid : int    //member function

            repeat| b!=0
               when| a > b
                        a - b > a
                    other|
                        b - a > b
                    |other
                |when
            |repeat

            back| a |back

        |sub
    |class


    sub| string args| | > main : int   //main function

        GCD N    //object N of class GCD

         in > N.a, N.b > N.Euclid > out    
         
         //input, output in one line

    |sub

|module
```



Once again, the `main` function showcases Semantica's natural flow.  The line `in > N.a, N.b > N.Euclid > out` reads input directly into the object's data members `N.a`, `N.b`, calls the object's member function `N.Euclid`, and prints the returned result.

\---

## 6.Intermodular

Semantica modules are connected through Intermodulars.

### Intermodular

Every module can be connected to other modules through intermodulars. Intermodular goes before module itself

### Example: Intermodular and Module

This example demonstrates flexibility and interconnection of module using mentioned before `Euclidian` algorithm

```Semantica

intermodular|

   link| in2out.sem |link  //using standard input and output
   link| module2.sem |link  //connecting to another module

    sub| int a, int b > Euclid : int |sub  //function that can be used by another modules

|intermodular

module| Euclidean

    sub| int a, int b > Euclid : int

    ...

    |sub

    ...

|module

```

In the beginning intermodular gives module access to standard I/O and then access to functions of another module. Also declaration of function that can be used by another module. Notice that source code extension of Semantica modules is `.sem`



\---

## 7.File System

### File Declaration

`file f(name, type, options)` - file declaration and creating

* name includes path
* type can be: bin, txt, or hex
* options: r - read, w - write

### Example: writing and reading text file

```Semantica

file f("Readme.md", txt, wr+)  //creating text file
string s //srtring for reading and writing

f.open
repeat| s  
//string for writing exists like reading "in > s" from standard input
    s > f  //writing string to file
|repeat
f.close

f.open
repeat| not f.eof  //reading
    f > s  //reading string from file
|repeat
f.close

```

\---

## 8.Generics

This language utilizes C++ like generics

```Semantica

module| generics

template| typename Iter, typename Val, typename Op |template

sub| (Iter first, Iter last, Val s, Op operator) > connect : Val       // here arguments are in () for clarity

    repeat| first != last

        operator(s, *first) > s    // *first - element of type Val pointed by iterator first

        ++first

    |repeat

    back| s |back       // this is function return not a vector

|sub


sub| string args| | > main : int

    float vec|4| (|1,2,3,4|)       // vector with 4 elements

    float (vec, vec + 4, 0.0, +) > connect > s1   // finding sum of floats, sum initialization 0.0

    float (vec, vec + 4, 0, + ) > connect > s2      // finding sum of integers, sum initialization 0

    float (vec, vec + 4, 1.0, * ) > connect > s3   // finding product of floats, product  initialization 1.0

    float (vec, vec + 4, 1, * ) > connect > s4   // finding product of integers, product initialization 1

|sub

|module

```

Here you can see usage of generics for **different types**: ` float ` and ` integer ` and for **different operators**: **` + `** and **` * `**

\---

## 9.Concurrency

**Semantica** achieves concurrency through **Multiplex**:

```Semantica

Multiplex tasks||       //vector of tasks

a, b > function1 > tasks|0|     //list of fuctions for each task
i, n > function2 > tasks|1|
...

int i(0)
repeat| !eot        //end of time of execution

tasks|i++|.concur       //running tasks concurrently

|repeat

```

\---


## Origins

* **Semantica** language has its roots in **C++** and **Pascal** programming languages
* It has variable declaration ` int i ` and generics from **C++**, and function declaration ` f : int ` from **Pascal**
* Also **C++** ` stream ` input and output:

```C++
cin >> a >> b 
cout << Euclid(a, b)
```

Inspired **Semantica** input and output:
```Semantica
in > a, b > Euclid > out
```


