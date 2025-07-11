

 The first one is pretty simple: the **s**yscall **trace**r, `strace`.

Given a program to run, `strace` will use functionality of the Linux operating system to introspect and record every system call that the program invokes, and its result. For example, let's look at our program from the previous challenge:

```shell
hacker@dojo:~$ strace /tmp/your-program
execve("/tmp/your-program",["/tmp/your-program"], 0x7ffd48ae28b0 /* 53 vars */) = 0
exit(42)                                 = ?
+++ exited with 42 +++
hacker@dojo:~$
```

As you can see, `strace` reports what system calls are triggered, what parameters were passed to them, and what data they returned. The syntax used here for output is `system_call(parameter, parameter, parameter, ...)`. This syntax is borrowed from a programming language called C, but we don't have to worry about that yet. Just keep in mind how to read this specific syntax.

In this example, `strace` reports two system calls: the second is the `exit` system call that your program uses to request its own termination, and you can see the parameter you passed to it (42). The first is an `execve` system call. We'll learn about this system call later, but it's somewhat of a yin to `exit`'s yang: it starts a new program (in this case, `your-program`). It's not actually invoked by `your-program` in this case: its detection by `strace` is a weird artifact of how `strace` works, that we'll investigate later.

In the final line, you can see the result of `exit(42)`, which is that the program exits with an exit code of `42`!

Now, the `exit` syscall is easy to introspect without using `strace` --- after all, part of the point of `exit` is to give you an exit code that you can access. But other system calls are less visible. For example, the `alarm` system call (syscall number 37!) will set a timer in the operating system, and when that many seconds pass, Linux will terminate the program. The point of `alarm` is to, e.g., kill the program when it's frozen, but in this case, we'll use `alarm` to practice our `strace` snooping!

In this challenge, you must `strace` the `/challenge/trace-me` program to figure out what value it passes as a parameter to the `alarm` system call, then call `/challenge/submit-number` with the number you've retrieved as the argument. Good luck!


Next, lets move on to GDB. GDB stands for the **G**NU **D**e**b**ugger, and it is typically used to hunt down and understand bugs. More specifically, a debugger is a tool that enables the close monitoring and introspection of another process. There are many famous debuggers, and in the Linux space, gdb is by far the most common.

We'll learn gdb step by step through a series of challenges. In this one, we'll focus on simply launching it. That's done as so:

```console
hacker@dojo:~$ gdb /path/to/binary/file
```

In this challenge, the binary that holds the secret is `/challenge/debug-me`. Once you load it in gdb, the rest will happen magically: we'll handle the analysis and give you the secret number. In later levels, you'll learn how to get that number on your own!

Again, once you have the number, exchange it for the flag with `/challenge/submit-number`.



Debuggers, including gdb, observe the debugged program _as it runs_ to expose information about its runtime behavior. In the previous level, we automatically launched the program for you. Here, we will tone down the magic somewhat: you must start the execution of the program, and we'll do the rest (e.g., recover the secret value from it).

When you launch gdb now, it will eventually bring up a command prompt, that looks like this:

```gdb
(gdb) 
```

You start a program with the `starti` command:

```gdb
(gdb) starti
```

`starti` "**start**s the program at the very first **i**nstruction. Give it a try now, and we'll configure gdb to magically extract the secret value once the program is running.


-----------------------------------------

As seen by your program, computer memory is a huge place where data is housed. Like houses on a street, every part of memory has a numeric _address_, and like houses on a street, these numbers are (mostly) sequential. Modern computers have enormous amounts of memory, and the view of memory of a typical modern program actually has large gaps (think: a portion of the street that hasn't had houses built on it, and so those addresses are skipped). But these are all details: the point is, computers store data, mostly sequentially, in memory.

In this level, we will practice accessing data stored in memory. How might we do this? Recall that to move a value into a register, we did something like:

```assembly
mov rdi, 31337
```

After this, the value of `rdi` is `31337`. Cool. Well, we can use the same instruction to access memory! There is another format of the command that, instead, uses the second parameter as an address to access memory! Consider that our memory looks like this:

```text
  Address │ Contents
+────────────────────+
│ 31337   │ 42       │
+────────────────────+
```

To access the memory contents at memory address 31337, you can do:

```assembly
mov rdi, [31337]
```

When the CPU executes this instruction, it of course understands that `31337` is an _address_, not a raw value. If you think of the instruction as a person telling the CPU what to do, and we stick with our "houses on a street" analogy, then instead of just handing the CPU data, the instruction/person _points at a house on the street_. The CPU will then go to that address, ring its doorbell, open its front door, drag the data that's in there out, and put it into `rdi`. Thus, the `31337` in this context is the _memory address_ and serves to _point to_ the data stored at that memory address. After this instruction executes, the value stored in `rdi` will be `42`!

Let's put this into practice! I've stored a secret number at memory address `133700`, as so:

```text
  Address │ Contents
+────────────────────+
│ 133700  │ ???      │
+────────────────────+
```

You must retrieve this secret number and use it as the exit code for your program. To do this, you must read it into `rdi`, whose value, if you recall, is the first parameter to `exit` and is used as the exit code. Good luck!




Let's learn to write text!

Unsurprisingly, your program writes text to the screen by invoking a system call. Specifically, this is the `write` system call, and its syscall number is `1`. However, the write system call also needs to specify, via its parameters, _what_ data to write and _where_ to write it to.

You may remember, from the [Practicing Piping](https://pwn.college/linux-luminarium/piping) module of the [Linux Luminarium](https://pwn.college/linux-luminarium) dojo, the concept of _File Descriptors_ (FDs). As a reminder, each process starts out with three FDs:

- **FD 0:** Standard _Input_ is the channel through which the process takes input. For example, your shell uses Standard Input to read the commands that you input.
- **FD 1:** Standard _Output_ is the channel through which processes output normal data, such as the flag when it is printed to you in previous challenges or the output of utilities such as `ls`.
- **FD 2:** Standard _Error_ is the channel through which processes output error details. For example, if you mistype a command, the shell will output, over standard error, that this command does not exist.

It turns out that, in your `write` system call, this is how you specify _where_ to write the data to! The first (and only) parameter to your `exit` system call was your exit code (`mov rdi, 42`), and the first (but, in this case, not only!) parameter to `write` is the file descriptor. If you want to write to standard output, you would set `rdi` to 1. If you want to write to standard error, you would set `rdi` to 2. Super simple!

This leaves us with _what_ to write. Now, you could imagine a world where we specify what to write through yet another register parameter to the `write` system call. But these registers don't fit a ton of data, and to write out a long story like this challenge description, you'd need to invoke the `write` system call multiple times. Relatively speaking, this has a lot of performance cost --- the CPU needs to switch from executing the instructions of your program to executing the instructions of Linux itself, do a bunch of housekeeping computation, interact with your hardware to get the actual pixels to show up on your screen, and then switch back. This is slow, and so we try to minimize the number of times we invoke system calls.

Of course, the solution to this is to write multiple characters at the same time. The `write` system call does this by taking _two_ parameters for the "what": a _where_ (in memory) to start writing from and a _how many_ characters to write. These parameters are passed as the second and third parameter to `write`. In the kinda-C syntax that we learned from `strace`, this would be:

```c
write(file_descriptor, memory_address, number_of_characters_to_write)
```

For a more concrete example, if you wanted to write 10 characters from memory address `1337000` to standard output (file descriptor 1), this would be:

```c
write(1, 1337000, 10);
```

Wow, that's simple! Now, how do we actually specify these parameters?

1. We'll pass the first parameter of a system call, as we reviewed above, in the `rdi` register.
2. We'll pass the second parameter via the `rsi` register. The agreed-upon convention in Linux is that `rsi` is used as the second parameter to system calls.
3. We'll pass the third parameter via the `rdx` register. This is the most confusing part of this entire module: `rdi` (the register holding the first parameter) has such a similar name to `rdx` that it's really easy to mix up and, unfortunately, the naming is this way for historic reasons and is here to stay. Oh well... It's just something we have to be careful about. Maybe a mnemonic like "`rdi` is the **i**nitial parameter while `rdx` is the **x**tra parameter"? Or just think of it as having to keep track of different friends with similar names, and you'll be fine.

And, of course, the `write` syscall index into `rax` itself: `1`. Other than the `rdi` vs `rdx` confusion, this is really easy!

Now, you know how to point a register at a memory address (from the [Memory](https://pwn.college/computing-101/memory) module!), and you know how to set the system call number, and how to set the rest of the registers. So, this should be cake!

Similar to before, we wrote a single secret character value into memory at address `1337000`. Call `write` to that single character (for now! We'll do multiple-character writes later) value onto standard out, and we'll give you the flag!


