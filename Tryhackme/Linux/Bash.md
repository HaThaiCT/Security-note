Ok now that we have had a brief introduction to what bash is and what it is used for let's jump right into some examples!

  

First of all let’s lay out our structure.

A bash script always starts with the following line of code at the top of the script.

                                                                        ![](https://i.ibb.co/7W5mn0c/carbon-8.png)  

  

  

This is so your shell (whatever type of it) knows that it needs to run your file using bash in the terminal.

  
  

Lets get into some basic examples.

                                                                         ![](https://i.ibb.co/Hz1VQ1D/carbon-9.png)

  

  

This will return the string “Hello World”. The command “`echo`” is used to output text to the screen, the same way as “`print`” in python. I suggest you test this out in your terminal to get to grips with bash!

You can also perform normal Linux commands inside your bash script and it will be executed if formatted right. For example we can run the command “`ls`” inside our bash script and we will see the output when we run the file. So lets make it do this!

                                                                        ![](https://i.ibb.co/HX85VzF/carbon-10.png)  

  

  

Now from here on I am going to assume that you have a basic understanding of Linux and its commands, if you don't please go make sure to check out the Linux fundamentals 1 and then come back and try again. [https://tryhackme.com/r/room/linuxfundamentalspart1](https://tryhackme.com/r/room/linuxfundamentalspart1)

I'm also not going to include the `#!/bin/bash` at the start of my code snippets otherwise it will take up a lot of room so be aware that you need it always at the start of your files!

Now to run our bash script we must first give it executable permissions

`Chmod +x yourfile.sh`

And then we run it using `./`

                                                                        ![](https://i.ibb.co/ccWWddT/carbon-11.png)

  

  

Please run this for yourself and see what you get.

We can see it has outputted the results of the commands “`whoami`” and “`id`”.

Now we are moving onto variables,

                                                                       in bash these are quite simple and we create them like so:

                                                                         ![](https://i.ibb.co/F4c1DFx/carbon-2.png)

  

  

Where we give the value of `Jammy` and assign it to the variable `name`.

Please note that for variables to work you cannot leave a space between the variable name, the ”**=**” and the value. They cannot have spaces in.

So how would we now use our variable? Well its also very simple.

  

We have to add a `$` onto front of our variable name in order to use it.

                                                                          ![](https://i.ibb.co/CmF2xrZ/carbon-3.png)

  

  

If we test this out in our own terminal we get something like this:

`$ name="Jammy"`

`$ echo $name`

`Jammy`  

This would output “**Jammy**” to the screen.

  

Variables make it much easier to store data and rather than typing out the same thing in multiple places we could simply insert our variable with $var and then declare that to a certain value making it easier to fall back on if you do something wrong and need to change it. So how can we debug our code?

  

Debugging is a very important part of programming so we should get used to problem solving and fixing errors as early as possible. And bash has a few built in features that make our life simple.

When running at the command line you can do:

  

`bash -x ./file.sh`

You can make a simple bash script(now you know some basic syntax) and make something completely wrong. Then step through your program with debug mode and see what it looks like when it throws errors!

  

This tells you which lines are working and which lines are not. If you want to debug at a certain point you can insert `set -x` into your script and `set +x` to end the section like the following:

                                                                          ![](https://i.ibb.co/dWYJkjs/carbon-4.png)

  

  

So lets look at an example. This is our script from earlier being ran with `bash -x ./example.sh`

                                                                          ![](https://i.ibb.co/288ynDZ/carbon-5.png)

  

  

You can see its outputting a **+** for the command and then the output of what that command executed. If there was an error it would output a **-** on that line this makes it easy to spot where you have gone wrong so you can fix them.

  

We can also use multiple variables in something like an echo statement. You aren't just limited to using 1!

                                                                          ![](https://i.ibb.co/vVp45SD/carbon-6.png)  

  

  

Answer the following questions and use this piece of code to guide you.

                                                                         ![](https://i.ibb.co/NncnrQ2/carbon-7.png)






We will now look at one of the main features of bash and that's using parameters.

  

We will firstly  look at parameters specified using the command line when running the file. These come in many forms but often have the "$" prefix because a parameter is still a variable.

Lets start by declaring a parameter that is going to be our first argument when running our bash script.

                                                                     ![](https://i.ibb.co/LCnNVNN/carbon-12.png)

  

  

We now run our script with `./example.sh Alex`

And sure enough we get returned with “Alex”

  

So what if we wanted the 2nd argument? Well the process is very simple and we simply add a `$2` instead of `name=$1`

  

Then run with `./example.sh Alex Tony`

What do you think it would return?

  

And it would return "Tony".

  

What if we didn't want to supply them like this however, and instead it would let us type in our name in a more interactive way, we can do this using `read`.

                                                                       ![](https://i.ibb.co/tzK62bK/carbon-13.png)

  

  

  

This code will hang after its ran, this gives you the opportunity to type in your name.

                                                                     ![](https://i.ibb.co/BCn4ptM/carbon-14.png)

  

  

And we can see that it worked!

  

Maybe try making a little biography maker, where you take the name, age, and job as parameters. Store them inside a variable and then output them to the screen inside a sentence. 

However there is so much more that you can do with parameters and I advice you to play around with them, after all practice is what makes you better!










For this module i suggest you follow along in the attackbox or a standard linux terminal to make it easier to understand.

Arrays are used to store multiple pieces of data in one variable, which can then be extracted by using an index. Most commonly notated as `var[index_position]`.

Arrays use indexing meaning that each item in an array stands for a number.

In the array `['car', 'train', 'bike', 'bus']` each item has a corresponding index.

All indexes start at position 0

  

|   |   |
|---|---|
|item|index|
|car|0|
|train|1|
|bike|2|
|bus|3|

  

Now we have covered this, let's make an array in bash.  

The syntax is as follows.

  

We have the variable name, in our case ‘transport’

We then wrap each item in brackets leaving a space between each item.

`transport=('car' 'train' 'bike' 'bus')`

We can then echo out all the elements in our array like this:

`echo "${transport[@]}"`

You can try this in your own terminal and see what it outputs.

Where the "@" means all arguments, and the [] wrapped around it specifies its index.

So what if we wanted to print out the item `train`.

We would simply type:

`echo "${transport[1]}"`

because the train is at index position 1.

  

The last thing we will cover is if we want to change an element, or delete it. If we wanted to remove an element we would use the `unset` utility.

`unset transport[1]`

This now removes the `train` item, if we wanted to we could echo it back out and see that it is indeed gone,

Now lets set it to something else. We can do:

`transport[1]='trainride'`

If we echo the array then we get:

`car trainride bike bus`

  

So we successfully managed to swap out an element in our array!

  

As a little side project try building on your previous project of a biography maker, include arrays so that you can store multiple names and multiple facts about the person. Then in the next module we can expand even further.

Given the array please answer the following questions

`cars=('honda' 'audi' 'bmw' 'tesla')`




![](https://i.ibb.co/k2DgyGg/carbon-19.png)  

  

When we talk about conditionals it means that a certain piece of code relies on a condition being met, this is often determined with relational operators, such as equal to, greater than, and less than.

  

We will make a simple "if" statement to check if a variable is equal to a value, we will also make a script that checks if a file exists and that it is writeable, if it is we will write a message to that file, if not writeable it will delete it and make a new one. A Lot of new things will be taught here so pay attention.

  

First, we will discuss the basic syntax of an if statement.

All if statements look like so:

                                                                        ![](https://i.ibb.co/RBNwXHX/carbon-15.png)

  

  

Let's look at an example:

                                                                       ![](https://i.ibb.co/34LR4sT/carbon-16.png)

  

  

If statements always use a pair of brackets and in the case of the [] we need to leave a space on both sides of the text(the bash syntax). We also always need to end the if statement with `fi`

  

Here a variable is being declared as 10 and in the top line of the if statement the variable $count is being compared to the integer 10.

If they are equal then it outputs **true**, if its false it outputs **false**. As we know 10 is equal to 10 so it outputs true.

The **-eq** is one way of doing this, you could also use “**=**”

  

|   |   |
|---|---|
|Operator|Description|
|-eq|Checks if the value of two operands are equal or not; if yes, then the condition becomes true.|
|-ne|Checks if the value of two operands are equal or not; if values are not equal, then the condition becomes true.|
|-gt|Checks if the value of left operand is greater than the value of right operand; if yes, then the condition becomes true.|
|-lt|Checks if the value of left operand is less than the value of right operand; if yes, then the condition becomes true.|
|-ge|Checks if the value of left operand is greater than or equal to the value of right operand; if yes, then the condition becomes true.|

^^^^^ These are some examples.

  

So now let's use this to make a little script that compares an input(a parameter) and checks it against a value to check if it's true or not. A guessing game if you will.

  

                                                                         ![](https://i.ibb.co/R9gvH5J/carbon-17.png)

  

  

Now let's test this in our terminal.

`# ./example.sh guessme`

`"They are equal"`

`# ./example.sh hi`

`"They are not equal"`

And we can see that it works!

Feel free to play around with these and try making different combinations and using different operators.

  

Now let's create another script where we will use 2 conditions simultaneously and coming back to a concept we learnt in the first lesson.

Let's begin.

We want to make a script that we will perform on a file given by a **parameter**.

We then check if it exists and if it has **write** permissions. If it has write perms then we echo “**hello**” to it. If it is either non-accessible or doesn't exist we will create the file and echo “hello” to it. Let's begin!

                                                                        ![](https://i.ibb.co/k2DgyGg/carbon-19.png)  

  

`─# ./example.sh hello.txt                                                                                                                ─# cat hello.txt`

hello

And we can see that it worked!!

The **-f** checked if the file existed.

The **-w** checked if the file was writable, without write permissions we wouldn't be able to output our text into the file.

  

To finish off our little project from the previous task. You can build on your script using an if/else statement. Test to see if the age is under 18, if it is then echo out their name with "You are not eligible for work" or something along these lines, if they are over 18 then ask them for their job, you can do this with `read`