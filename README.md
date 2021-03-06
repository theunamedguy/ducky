Ducky
=====

IRC: #ducky-lang at `irc.freenode.net`

## Introduction

Ducky is a BASIC-like programming language originally insipred by Duckyscript, the USB Rubber Ducky's scripting language.

## Examples

### Hello World

    #!/bin/ducky
    LOG Hello, world!
    NEWLINE

Simple!

### Fibonacci Sequence

    #!/bin/ducky
    LET a = 0; LET b = 0; LET iter = 0
    LABEL loop_start
    LOGVAR a
    NEWLINE
    LET c = a+b
    LET a = b
    LET b = c
    INC iter
    IF iter < 20; GOTO loop_start
    LOG Done!
    NEWLINE

### Prime Counter

    #!/bin/ducky
    LOG Counting...
    NEWLINE
    LET primes=0
    LET MAX=100000
    LET n = 2
    LBL test_number
    LET iter = 2
    LET stop = sqrt n
    LBL test_loop
    IF !(n % iter); GOTO composite
    INC iter
    IF iter <= stop; GOTO test_loop
    INC primes
    LBL composite
    INC n
    IF n < MAX; GOTO test_number
    LOG Number of primes below
    LOGVAR MAX
    LOG :
    LOGVAR primes
    NEWLINE

## Building

POSIX systems are supported, as are some Rockbox targets.

### Unix/Linux

    make
    sudo make install

This installs the `/bin/ducky` binary.

## Usage

### Running Directly (no compilation)

    ducky scriptname.ds

### Compiling to bytecode

    ducky -c scriptname.ds

This will create `a.out`, which contains the bytecode.

### Executing bytecode

    ducky a.out

### Full Compile (from ducky to machine code)

    ducky -a scriptname.ds
    ./a.out

## Technical Details

The program consists of four parts: the interpreter, compiler, bytecode interpreter, and C transcompiler.

### Interpreter

Executes ducky directly.

### Bytecode Compiler

Compiles ducky to a stack-machine based bytecode.

### Bytecode Interpreter

Executes the bytecode generated by the bytecode compiler.

### C Transcompiler

Translates bytecode generated by the bytecode compiler into C.

## Benchmark Results

21 Nov 2015:

    c - clang     26 27 27 27 27 27 27 27 27 27 - AVG 26.9
    c - gcc       29 29 29 29 29 29 29 29 29 29 - AVG 29
    c - tcc       28 28 28 28 28 28 28 28 28 28 - AVG 28
    ducky - clang 15 15 15 15 15 15 15 15 15 15 - AVG 15
    ducky - gcc   28 28 28 28 28 28 28 28 28 26 - AVG 27.8

26 Nov 2015:

<table>
<tr><th>Language</th><th>Compiler</th><th>Optimization Level</th><th>Scores</th><th>Mean score</th></tr>
<tr><td>Ducky</td><td>Clang</td><td>-O0</td><td>4 4 4 4 4 4 4 4 4 4</td> <td>4</td></tr>
<tr><td>Ducky</td><td>Clang</td><td>-O1</td><td>15 15 15 15 15 15 15 15 15 15</td><td>15</td></tr>
<tr><td>Ducky</td><td>Clang</td><td>-O2</td><td>21 21 21 21 21 21 21 21 21 21</td><td>21</td></tr>
<tr><td>Ducky</td><td>Clang</td><td>-O3</td><td>21 21 21 21 21 21 21 21 21 21</td><td>21</td></tr>
<tr><td>Ducky</td><td>GCC</td><td>-O0</td><td>5 5 4 5 5 5 5 5 5 5</td> <td>4.9</td></tr>
<tr><td>Ducky</td><td>GCC</td><td>-O1</td><td>22 23 23 23 23 23 23 23 23 23</td><td>22.9</td></tr>
<tr><td>Ducky</td><td>GCC</td><td>-O2</td><td>26 26 26 26 26 26 26 26 26 26</td><td>26</td></tr>
<tr><td>Ducky</td><td>GCC</td><td>-O3</td><td>26 26 26 26 26 26 26 26 26 26</td><td>26</td></tr>
<tr><td>C</td><td>Clang</td><td>-O0</td><td>28 28 28 28 28 28 28 28 28 28</td><td>28</td></tr>
<tr><td>C</td><td>Clang</td><td>-O1</td><td>28 29 29 28 28 28 28 28 29 29</td><td>28.4</td></tr>
<tr><td>C</td><td>Clang</td><td>-O2</td><td>28 29 29 29 28 29 29 28 28 28</td><td>28.4</td></tr>
<tr><td>C</td><td>Clang</td><td>-O3</td><td>28 28 28 29 28 29 28 29 28 28</td><td>28.3</td></tr>
<tr><td>C</td><td>GCC</td><td>-O0</td><td>28 28 28 28 28 28 28 28 28 28</td><td>28</td></tr>
<tr><td>C</td><td>GCC</td><td>-O1</td><td>30 30 30 30 29 30 29 30 30 29</td><td>29.7</td></tr>
<tr><td>C</td><td>GCC</td><td>-O2</td><td>30 30 30 30 30 30 30 30 30 30</td><td>30</td></tr>
<tr><td>C</td><td>GCC</td><td>-O3</td><td>30 30 30 30 30 30 30 30 30 30</td><td>30</td></tr>
</table>


## Future Directions

   - Refactor code
   - Input
   - Add more builtins
   - Arrays?
   - Functions?
