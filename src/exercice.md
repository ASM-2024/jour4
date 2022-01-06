---
title: "Forking, Piping and Redirection"
author: ASM 2024
logo: https://avatars.githubusercontent.com/u/96961500?s=200&v=4
---

# Introduction

Today you are going to learn how to handle processes in C. This will also teach you the basics of inter-process communication using redirections.

Here are the provided files for this part:
[Skeleton](subject.tar)

Use the following command to extract the files :
```bash
asm$ tar -xvf <filename>.tar.gz
```

# Tonight, the nightmare is back

Remember yesterdays' practical ? Today, will be handling it once more... Now that you've acquired some new low-level skills, we will be using them to defeat the game.

You probably haven't succeeded in finishing the game by hand, that's why you're going to have to let someone else that is way faster than you do it: your computer. 

Your goal today is to write a program that will complete the signal game.

Your program will:
1. Launch the binary file given by argument
2. Get the  ``stdout``  output of the program through a pipe
3. Read through the created pipe the signal currently required by the game
4. Send the required signal to the process

Here is the expected behavior of the program:
```bash
asm$ ./cheater ./<game_binary>
```

You can get the binary from [yesterdays' practical](https://asm-2024.github.io/jour3/signals.html#sending-signals).

## cheater.h

We would strongly recommend you to have a look at `cheater.h` to see all the included headers and the defined macros.

You will have access through this header to:
- signals: global variable of type ``char **`` which is an array of all the signal strings in the correct order.
- NB_SIGNALS: macro that will enable you to access the number of elements inside the `signals` array.
- BUFF_SIZE: macro that you should use for your buffer size.

## cheater.c

In this file, we have given you a simple structure containing different functions to complete. You'll have to complete them by following the described steps.

### string_to_signal

This function will be used in the `main` function. The goal is to retrieve the number of the signal based on its textual representation.

Hint : do not forget that in C, arrays are zero-based!

### read_until

This function is also used in the `main` function. Its purpose is to read from the file descriptor `fd` until the character `delim` is found. You may assume that in this exercise the buffer `buf` of size `buf_size` is large enough. Do not forget to append a null byte after the last character read otherwise the sequence won't be considered as a valid string.

### execute

Here comes the heavy lifting. In this function, you'll directly use what you've learned this morning.

The goal of this function is to execute the `executable` binary in a child process after doing the necessary redirections.

For this function you'll need to have a look at `execvp(3)` which will allow you to execute the `executable` along with `fork(2)`.

But before you do so, you will have to do the appropriate redirections using `dup2(2)` and `pipe(2)`. Do not forget to close the appropriate ends of the pipe created after having "duped" the standard output.

---
Now it's up to you to try and win the game! 
---
# Extra exercise
For anyone willing to do extra exercises regarding low-level process handling and redirection, we suggest you take
a look at the practical given during the past years [right here](https://prepa.pages.epita.fr/asm/strasbourg-c-unix-seminar/practicals/D3/practical3.html)

# Correction

A correction will be given this weekend. It will be on the Github repository and the link will be given here. This will **not** be the **only** nor **the best** solution to the problem but do take the time to read it as it uses advanced concepts!
