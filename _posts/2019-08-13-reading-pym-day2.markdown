---
layout: post
title:  "Reading PYM book: Day 2"
date:   2019-08-13 10:10:57 +0530
categories: jekyll update
---

+ # if-else 
   Want to give your program the power of decision-making? 
   Just add if-else statements to the code.
   
   This is where the identation practices come into play. (Wrong output despite the if-else statement can frustate you :P)

   if-else can be nested and can also be extended by elif statements (if you have more than 2 choices)

   - Truth value testing:
     Another good practice 
      ```python
      if x:
          # code statements
      ```
     and not `x == True:`
     
     I have made this mistake many times. 

     The reason you shouldn't do this is that every single object in Python can be evaluated to True or False. 
     The PEP 8 Style Guide recommends against comparing a value to True or False as it is less readable and will frequently return an unexpected Boolean.
     (I found the reason with the help of this [link][reason-link])

+ # Looping
   Want the program do to a task repeatedly? 
   Loop the task instead of writing it multiple times

+ # Lists
   A data structure. Implemented using square brackets.
   You can use slicing to access specific elements of list: `list[start:stop-before:step]`

   - Learnt about range() function from a new perspective. Did not realize earlier that it was a generator function.
   
   


[reason-link]: https://www.digitalocean.com/community/tutorials/understanding-boolean-logic-in-python-3


