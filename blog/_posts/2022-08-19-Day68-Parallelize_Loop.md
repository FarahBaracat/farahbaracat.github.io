---
layout: post
title: Day 68 - Parallelization in Python, Multiprocessing & Threading
tags: [ICL Project]
include_toc: true
---

I want to train 6 models in parallel to save computation time. So I started looking into paralellizing python program.
Two main concepts kept hunting me 😀. Bear in mind that everything here is related to Python for now (I haven't 
looked into how things are for other programming languages)
- Multiprocesing or process-based parallelism
- Multithreading or thread-based parallelism

# Multiprocessing vs. Multithreading
Starting from the basics: threading in Python allows the executing of different parts of a program concurrently 
which speeds up execution.

## Definitions: Program, Process, Thread
3 core concepts in operating systems (can read more [here](https://www.quora.com/What-is-difference-between-thread-process-and-program))
- **A Program**: an executable file containing a set of instructions to perform a certain task on your computer. 
  Programs are stored on a disk or a secondary memory on the computer. They are fetched into the primary memort and 
  executed by te kernel.
- **A Process**: a program that is loaded into memory and is executing (it is an *executing* instance of a program). It 
  therefore 
  resides on 
  the primary memory 
  and leaves this memory if the system is rebooted. You can instanciate multiple executing instances of the same 
  program.
- **A Thread**: is the smallest executable unit of a process. That is to say that a process can have multiple 
  threads. Each thread having their own task to do (aka minding their own business like I wish many people would :D).
  Example, one thread can reading in user inputs and another thread doing some computation on those inputs. One 
  important thing to know is that <mark>threads share the memory of that process</mark>.


## Threading
**A thread** forks the flow of the program. This means that a program will have two things being executed at once. 
  For Python 3, and this is where things get interesting, in reality, the different threads **are not actually being 
  executed at the same time but rather appear to**. What kind of sorcery is that? 

- Python has a **global interpreter lock (GIL)**, is a lock that allows only one thread to have control of the 
  Python interpreter. So in reality, multiple threads cannot be executed in parallel (more on [GIL](https://realpython.
  com/python-gil/)).
- For code that required heavy CPU computation and spend little time waiting for external events, using 
  multithreading might not speed up the execution at all.

## Multiprocessing
Multiprocessing on the other hand uses multiple CPUs (and cores). The memory is hence not shared; every process has 
its own memory (or a separate memory space) which eliminated the need fo synchronization (because the ressources are 
not shared)

- It bypasses the GIL completely 
