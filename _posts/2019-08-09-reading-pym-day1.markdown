---
layout: post
title:  "Reading PYM book: Day 1"
date:   2019-08-09 10:00:57 +0530
categories: jekyll update
---
Recently, I was suggested to read the book ["Python for you and me"][pym-book-link], for learning Python programming language.

Although I know a bit of Python, I thought it would be good to revise my fundamentals again.

- # Beginning Section
   The beginning section was really good. It mentions about : 
   + Python Interpreter : _The interpreter which can access the code_
   + Whitespaces and Indentation : _How to handle spaces while writing code_
   + Source Files : _making py files executable_ 
   + Comments : _writing comments to remember why you did this_
   + Modules : _stuff made by others that you can use for free_
   

   I liked the fact that best practices are mentioned alongside programming concepts. 
   Some new best practices I learnt were: 
   + One blank line between functions.
   + Two blank lines between classes.
   + Add a space after “,” in dicts, lists, tuples, and argument lists and after “:” in dicts.
   + Spaces around assignments and comparisons (except in argument list)
   + No spaces just inside parentheses.
   + Add a space after the # in comments

   Though most of them won't give errors if you don't follow them. However, they `increase code readability` and make it `easier to correct any errors`.

   Also,  one basic thing that I learnt just some days before reading the book was making the a .py file executable.
   ```bash
   $ chmod +x helloworld.py
   ```
   One raging doubt I had was how does the compiler gets to know about she-bang,
   `#!/usr/env/bin python` as # used for comments in python.
   After some more study, I realized that I was thinking all wrong, the python interpreter comes into picture after the she-bang part.
   
   > In Unix-like operating systems, when a text file with a shebang is used as if it is an executable, the program loader mechanism parses the rest of the file's initial line as an interpreter directive. 
   > The loader executes the specified interpreter program, passing to it as an argument the path that was initially used when attempting to run the script, so that the program may use the file as input data.
   > 
   > ~ Wikipedia
   
  (In short, program loader calls the appropriate interpreter after seeing the she-bang :P )
 
- # mu Editor
   Also, I got to know about mu editor for python. (I only knew about IDLE :P) 
   
   mu is more beginner-friendly. 

   Learnt about REPL (read-evaluate-print-loop). It basically means reading user input, evaluating it, printing the result and then repeat these 3 steps.
   You can know more about them from [here][repl-link]
   
   It basically refers to the shell you run by typing python in the terminal. Used it many times but didn't know about REPL.  

- # Variables and Datatypes
   + Learnt about f-strings and why they were included from the talk mentioned in the book.
     The reason was that the previous method of formatting was error-prone, inflexible and cumbersome.  

     We had .format, but code becomes longer, and we are repeating things. It will be cumbersome to make small changes, so then f-strings were introduced.
 
     Just remove the .format part and then added 'f' before the string
     (Too easy, isn't it? XD)
  
     Also learnt about PEP(Python Enhancement Proposal) from the talk.
     
   + Learnt about tuple packing and unpacking. I had used them but didn't intuitively associate them with tuples.
     I found myself using unpacking more often after reading that (Baader-Meinhof phenomenon maybe :P)

- # Operators and Expression 
   + An important and basic section. 
     Operators: _Arithmetic, Logical, Relational, Shorthand_ 
     Expression: Collection of operators and operands (with seom parentheses along the way)

   + Also mentioned type-conversion (we change type of a variable whose type you never declared :P)

[pym-book-link]: 
[repl-link]: https://pythonprogramminglanguage.com/repl/
[github-pages]: https://pages.github.com/

