---
title: "Forking, Piping and Redirection"
author: ASM 2024
logo: https://avatars.githubusercontent.com/u/96961500?s=200&v=4
---

# Introduction

Today you are going to learn how processes are handled in C. This will also teach you the basics of inter-process communication using redirections.

Here is the skeleton for this part:
[Skeleton](????)

To extract the files use the following command:

```bash
asm$ tar -xf <filename>.tar.gz
```

# Tonight, the nightmare is back

Remember the yesterday's practical ? Today will be handling it once again but in a different context. Now that you've acquired some new low-level skills, we will be using them to defeat the game.

The context under which we will approach the subject is automatization necessary in many areas of your life as an engineer.

Your goal today is to make a program that will play the signals game (possibly) win against it. The general behaviour of the program is going to be the following : 

```bash
asm$ ./cheater ./<game_binary>
```

## cheater.c

In this file there's one provided function and four that you'll have to do. Have a look at `cheater.h` to see what how the signal are defined.

### string_to_signal

This function will be used in the `main` function. It's goal is to retrieve the number of the signal based on its textual representation.

Hint : do not forget that in C, arrays are zero-based!

### read_until

This function is also used in the `main` function. It's purpose is to read from the file descriptor `fd` until the character `delim` is found. You may assume that in this exercise the buffer `buf` of size `buf_size` is large enough. Do not forget append a null byte after the last character read otherwise the sequence won't be considered as a valid string.

### execute

Here comes the heavy lifting. In this function, you'll directly use what you've learned this morning.

The goal of this function is to execute the `executable` (a `NULL` terminated array of strings) in a child process after doing the necessary redirections.

For this function you'll need to have a look at `man 3 execvp` which will allow you to execute the `executable`.

But before you do so, you will have to do the appropriate redirection using `man 2 dup`. Do not forget to close the appropriate end of the pipe `P` after having "duplicated" the standard output file descriptor.

### main

After having done all the functions from above, it is time to link them together in the main function.

To initialize the pipes, have a look at `man 2 pipe`. To wait for the children you may use the `wait()` (see `man 2 wait`).

# Extra exercise
For anyone willing to do extra exercises regarding low-level process handling and redirection, we suggest you take a look at the practical given during the past years [right here](https://prepa.pages.epita.fr/asm/strasbourg-c-unix-seminar/practicals/D3/practical3.html)

# Correction

A correction will be given this weekend. It will be on the Github repository and the link will be given here. This will **not** be the **only** nor **the best** solution to the problem but do take the time to read it as it uses advanced concepts!
