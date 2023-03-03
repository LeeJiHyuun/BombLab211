# BombLab 211
2022-2 컴퓨터SW시스템개론 Lab1


## 1 Introduction
  The nefarious Dr. Evil has planted a slew of “binary bombs” on our class machines. A binary bomb is a
  program that consists of a sequence of phases. Each phase expects you to type a particular string on stdin.
  If you type the correct string, then the phase is defused and the bomb proceeds to the next phase. Otherwise,
  the bomb explodes by printing "BOOM!!!" and then terminating. The bomb is defused when every phase
  has been defused.
  There are too many bombs for us to deal with, so we are giving each student a bomb to defuse. Your mission,
  which you have no choice but to accept, is to defuse your bomb before the due date. Good luck, and
  welcome to the bomb squad!

## Step 1: Get Your Bomb
You can obtain your bomb by pointing your Web browser at:
https://drive.google.com/drive/folders/1e0-
blqX0N5SG0y8kk9O01GjCOUs25GuH?usp=sharing
You can find your own binary bomb on the website. Download the tar file with your student id and upload
it on programming2.postech.ac.kr. Then give the command: tar -xvf <yourID>.tar.
This will create a directory called ./<yourID> with the following files:
• README: Identifies the bomb and its owners.
• bomb: The executable binary bomb.
• bomb.c: Source file with the bomb’s main routine and a friendly greeting from Dr. Evil.
  
## Step 2: Step 2: Defuse Your Bomb
Your job for this lab is to defuse your bomb.
You must do the assignment on one of the class machines. In fact, there is a rumor that Dr. Evil really is
evil, and the bomb will always blow up if run elsewhere. There are several other tamper-proofing devices
built into the bomb as well, or so we hear.
You can use many tools to help you defuse your bomb. Please look at the hints section for some tips and
ideas. The best way is to use your favorite debugger to step through the disassembled binary.
Each time your bomb explodes it, you will be sad, instead of losing your assignment points. So there are no
consequences to exploding the bomb. But, don’t abuse it! You need to explain your answers on your handin.
The first four phases are worth 10 points each. Phases 5 and 6 are a little more difficult, so they are worth
15 points each. So the maximum score you can get is 70 points.
Although phases get progressively harder to defuse, the expertise you gain as you move from phase to phase
should offset this difficulty. However, the last phase will challenge even the best students, so please don’t
wait until the last minute to start.
The bomb ignores blank input lines. If you run your bomb with a command line argument, for example,
$ ./bomb < solution.txt
then it will read the input lines from solution.txt until it reaches EOF (end of file), and then switch
over to stdin. In a moment of weakness, Dr. Evil added this feature so you don’t have to keep
retyping the solutions to phases you have already defused.
To avoid accidentally detonating the bomb, you will need to learn how to single-step through the assembly
code and how to set breakpoints. You will also need to learn how to inspect both the registers and the
memory states. One of the nice side-effects of doing the lab is that you will get very good at using a debugger.
This is a crucial skill that will pay big dividends the rest of your career.
                       
## Hint
There are many ways of defusing your bomb. You can examine it in great detail without ever running the
program, and figure out exactly what it does. This is a useful technique, but it not always easy to do. You
can also run it under a debugger, watch what it does step by step, and use this information to defuse it. This
is probably the fastest way of defusing it.
We do make one request, please do not use brute force! You could write a program that will try every
possible key to find the right one. But this is no good for several reasons:
• You need to explain your answers, like how did you find the answers with gdb.
• We haven’t told you how long the strings are, nor have we told you what characters are in them.
Even if you made the (incorrect) assumptions that they all are less than 80 characters long and only
contain letters, then you will have 2680 guesses for each phase. This will take a very long time to
run, and you will not get the answer before the assignment is due.
Note that you need to defuse your own bomb. Your submission might be ignored if the bomb isn’t yours.
Please double check when you download the bomb.
There are many tools which are designed to help you figure out both how programs work, and what is
wrong when they don’t work. Here is a list of some of the tools you may find useful in analyzing your
bomb, and hints on how to use them.
• gdb
The GNU debugger, this is a command line debugger tool available on virtually every platform. You
can trace through a program line by line, examine memory and registers, look at both the source code
and assembly code (we are not giving you the source code for most of your bomb), set breakpoints,
set memory watch points, and write scripts. The CS:APP web site
http://csapp.cs.cmu.edu/public/students.html
4
has a very handy single-page gdb summary that you can print out and use as a reference. Here are
some other tips for using gdb.
– To keep the bomb from blowing up every time you type in a wrong input, you’ll want to learn
how to set breakpoints.
– For online documentation, type “help” at the gdb command prompt, or type “man gdb”,
or “info gdb” at a Unix prompt. Some people also like to run gdb under gdb-mode in
emacs.
• objdump -t
This will print out the bomb’s symbol table. The symbol table includes the names of all functions and
global variables in the bomb, the names of all the functions the bomb calls, and their addresses. You
may learn something by looking at the function names!
• objdump -d
Use this to disassemble all of the code in the bomb. You can also just look at individual functions.
Reading the assembler code can tell you how the bomb works.
Although objdump -d gives you a lot of information, it doesn’t tell you the whole story. Calls to
system-level functions are displayed in a cryptic form. For example, a call to sscanf might appear
as:
8048c36: e8 99 fc ff ff call 80488d4 <_init+0x1a0>
To determine that the call was to sscanf, you would need to disassemble within gdb.
• strings
This utility will display the printable strings in your bomb.
