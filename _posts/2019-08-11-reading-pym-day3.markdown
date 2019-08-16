---
layout: post
title:  "Reading PYM book: Day 3"
date:   2019-08-11 10:00:57 +0530
categories: jekyll update
---

+ # Data Structures
   - Lists were discussed in more detail.
   - Lists were used as stack using the `pop()` function and as queues using `pop(index)` function.
   - List comprehension: _concise way of creating lists_
   - Tuples: _elements seperated by commas, enclosed within parentheses. Tuples are immutable._

     I didn't know that we could create a tuple with a single value by adding a trailing comma. 
    
     `a = (123,)`  
   - Set: _data structure with no duplicate items, elements enclosed within curly braces._
   - Dictionaries: _unordered set of key-value pairs, where keys are unique. Enclosed by curly braces_
     Mutable objects such as list, cannot be used as a key in dictionaries.
   - `enumerate()` function for getting iteration number as well as the value when looping through a list. `zip()` function for iterating through two sequences at the same time.

+ # Strings
   - Text in simple terms. Learnt that string literals alongside each other, behave like single string. 
   - String object has many builtin methods. Some of ones I have used less often are:
      * `title()` _which returns titlecased string_
      * `isalnum()` _for checking if the string has alphanumeric characters or not_
      * `isalpha()` _for checking if the string has alphabets or not_
      * `lstrip(chars)` _for removing characters from the left_ and `rstrip(chars)` _for removing characters from the right_ 
      * `swapcase()` _for swapping the cases in the string, uppercase to lowercase and vice-versa_
      
+ # Functions
   - Reusing a code that is required many times in a program.
   
     Functions are defined using the `def` keyword.
   
     `if __name__ == '__main__':` had been a long lost doubt of mine. I finally understood why to use it.
     
     `__name__` is a Python variable that gets its value depending upon execution method of the script. It is set to `__main__` if it is executed as a script.
     If it is imported as a module, it is set to the name of the script.
     So basically, `if __name__ == '__main__':` is used to add code that will be executed in the script but not when used as a module.
     I learnt about it from this [link][name-main-link]    

   - Local and Global variables.Unless declared, functions work on local variables. To make global variables, just use `global` keyword.

   - Default argument values (in case the user refuses to give a value :P) 

     You cannot have arguments without default values after an argument has been given default values. (changing the order can resolve this problem if you don't want to give a default value) 

   - An interesting thing I learnt: if your default argument is an empty list (mutable object), things can wrong. It's better to set list as None and then set to [] if it remains None. 
   
   - Learnt about keyword only argument, which forces the user to use correct keyword for each parameter.

     ```python
     def func (*, arg = value):
     ```
     All the other arguments are included in *.To input the specific argument, you will have to use the keyword. You can read more about this from [here][pep-3102-link]    

   - Docstrings were also introduced in this section. I learnt about auto-documentation.

   - Higher order functions were a new thing for me.They include functions that take one or more functions as arguments or return another function as output.

   - Learnt about `map()` function properly this time. It basically 'maps' an iterator to a function, so each value of the iterator is passed to the function.

+ # File Handling
   - As the name suggests, handling files, which involves opening,reading, writing and closing files.
   - `open()` function is used to open files.It takes two arguments, the filepath and the mode in which it needs to be opened.
   - Some of the reading modes are:
     * r _read-only mode_
     * w _allows writing on file_
     * a _allows appending on the file_

   - File handling is a tough business to handle in code.Make sure you take precautions, i.e., close files after their work is done, read and write on files of known size. Your main memory will thank you for it. In case the file is too big, just read it line by line :)

   - Now to help you a bit in file handing, we have `open with ('filpath','mode') as filename:` method to the rescue. This ensures that the file closes in case you forget to.

+ # Error Handling
   Errors can come any time. While testing, and even after deployment. You must now how to handle errors.
     Some of the errors that we see most of the time are NameError and TypeError. (happens to newbies all the time :P)

     - NameError: literal sense - error in name. 
       Happens when python doesn't understand a name. Generally this error occurs when we misspell a variable name.

     - TypeError: literal sense - error in type. 
       This error happens when type is wrong, i.e. the datatype you are performing the operation on is incompatible for it.

   With bugs crashing the programs (and all hope for peace of mind :P), your only hope is try-except blocks.

   ```python
   try:
       # code statments that may lead to an error
   except:
       # code statements that run in case an error does take place
   ``` 
   Code in the try block just runs like a normal code. If in case, an error is encountered, control goes to except block, which then runs code for handling errors.

[name-main-link]: https://www.freecodecamp.org/news/whats-in-a-python-s-name-506262fe61e8/
[pep-3102-link]: https://www.python.org/dev/peps/pep-3102/


