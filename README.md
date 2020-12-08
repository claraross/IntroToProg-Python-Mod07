# IntroToProg-Python-Mod07
Module 07 Homework and Files

## Serialization and Exception Handling
### Introduction

This assignment had us learn about serialization in Python (specifically pickling and unpickling) as well as the basics of exception handling. We applied these concepts to a simple script of our choosing. I decided to create a script that let the user write a journal entry, then save as binary data in a file. 

### Topic 1: Serialization

Serialization is the process of transforming data into something that can be stored, then reconstructed later (Object Oriented Python, TutorialsPoint, https://www.tutorialspoint.com/object_oriented_python/object_oriented_python_serialization.htm, 2020) (External Site). Pickling is a way of serializing data into binary form, often making file sizes much smaller in the process. 
In order to pickle (and later unpickle) data, we need to use the Pickle module! For the purposes of simply pickling and unpickling data, it is simple. Your code must:
1.	Import the module
2.	Open files you will be working with in “binary” read/write mode
3.	Use the built-in pickle methods of pickle.dump and pickle.load to pickle/unpickle respectively. 

In order to accomplish the above three things, I included two methods in my Processing class in my code (Figure 1).

```
# add new entries to file (pickle data)
@staticmethod
def add_entries_to_file(list_of_entries, file_name):
    file = open(file_name, "wb")
    pickle.dump(list_of_entries, file)
    file.close()

# unpickle data
@staticmethod
def read_pickle_file(file_name):
    file = open(file_name, "rb")
    file_data = pickle.load(file)  # load() only loads one row of data.
    file.close()

    return file_data
```
##### Figure 1: pickling and unpickling methods in the Processor class

I was able to call on these methods in the main body of my script to load and save the data I wanted in the correct format. 

Something interesting about pickling data is that it is not secure. When you unpickle some python data, it can contain code that will run on your machine. This allows bad actors to run malicious programs without your consent. The official Python documentation as well as most other resources I came across on the subject recommended that you do not open pickled data if you do not know its source (pickle Module, Python.org, https://docs.python.org/3/library/pickle.html#module-pickle, 2020) (External Site). 

I work with JSON data quite regularly in my job, so it was interesting to learn that pickle and JSON are similar things. Pickle, however, is python specific whereas JSON can be used with pretty much any language. However, according to the Python documentation, JSON only works with a few Python built-in types (pickle Module, Python.org, https://docs.python.org/3/library/pickle.html#module-pickle) (External Site). 

### Topic 2: Exception Handling – Built-In Exceptions

The majority of this assignment revolved around exception handling. Already I had seen many of the default errors Python had to offer, ValueError, FileNotFoundError, TypeError, etc. Now that I am familiar with Python, these errors make sense, but previously they seemed very esoteric and left me unsure of what to do next. 
This is why exception handling is very important, particularly if you are working with a program that involves user input. Something may seem to be clear on what should be entered or any steps an end user must take before proceeding, but people are often surprising, leading to interesting impacts to your program. 

This assignment introduced the try, except block and how to raise exceptions. All code that falls under try: will run until an error comes up. If and when an error occurs, the code looks to the except: block to determine what to do next. 

My script included a menu of choices and an opportunity for the end user to input their choice. I expected the user to put in a 1, 2, 3, or 4, but there was nothing actually stopping them from inputting the word version of a number (e.g. “one”). 

Because the script was looking for an integer as the user’s choice, this meant that the program would throw a ValueError if the user put in a string. If you were the end user, Python’s built in message might not make sense. So to provide clearer instructions for my user, I specified that if a ValueError occurs, the program should print the message “Must input number, try again” (Figure 2):
```
except ValueError as e:
    print("Must input number, try again")
```
##### Figure 2: Handling if a user inputs a string rather than an integer

### Topic 3: Exception Handling – Custom Exceptions

Some exceptions won’t break the program, but should be stopped as they don’t work with what the script is trying to do. In this case, there is nothing stopping the user from putting in an integer outside of the available options as their choice. The program sees it is an integer, so no value error occurs, but it doesn’t know what to do with that choice as there was nothing defined for choices outside of 1-4. 

To handle this, I made a custom exception class called InvalidChoice (Figure 3). To make a custom exception, you define it as a new class that inherits from the Exception class (User-Defined Exceptions, https://www.programiz.com/python-programming/user-defined-exception, 2020) (External Site). 

This custom exception specified that if that exception was raised, the program should print a string saying "Please choose option 1, 2, or 3". Then, I added an else statement to my if statement that addressed each choice from the menu. This caused the program to raise InvalidChoice() for all other intergers entered besides 1, 2, or 3.
```
class InvalidChoice(Exception):
    def __str__(self):
        return "Please choose option 1, 2, or 3"
```
##### Figure 3: A custom error class

Of course, there were almost certainly other errors that could crop up. To address those, I added another Except block that printed the built-in error for any other cases that may arise. 

### Topic 4: Github

This assignment also had us using Github webpages for our documentation. After creating this document in word (and, honestly, writing these last few sentences), I copied everything over to the readme for my Module07 repository. Then I worked on formatting everything using Markdown. 
So far Github is clearly a great source for tracking code changes and giving others the resources to use your programs effectively. 

### Conclusion

This assignment was simple in some ways, but I am curious to see how these concepts are applied in more complex programs. Learning about serialization was particularly interesting as I did not even realize I worked with serialized data regularly. It is also a good reminder to be wary of unknown code, especially as I start to work with more programs directly on my machine. 
