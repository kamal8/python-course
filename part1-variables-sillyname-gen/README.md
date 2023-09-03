# Naming and Using Variables
In python, a variable is when you set a value along with its associated information to it to an alias. For example, if you wanted to use a variable `name` (which we will below) then you'd need to set the variable within your python environment.
```python
name = "write your name here"
```
Try it out in a jupyter notebook, or within ipython in your terminal. Now when you run the following (in either your ipython or jupyter notebook):
```python
print(name)
```
You should see the name the name you put in returned.

When you’re using variables in Python, you need to adhere to a few rules and guidelines. Breaking some of these rules will cause errors; other guidelines just help you write code that’s easier to read and understand. Be sure to keep the following variable rules in mind:
* Variable names can contain only letters, numbers, and underscores. They can start with a letter or an underscore, but not with a number. For instance, you can call a variable message_1 but not 1_message.
* Spaces are not allowed in variable names, but underscores can be used to separate words in variable names. For example, greeting_message works, but greeting message will cause errors.
* Variable names in Python are all lowercase, with the exception of constant values that are all uppercase (e.g. `PI_APPROXIMATION = 22 / 7`)
* Avoid using Python keywords and function names as variable names; that is, do not use words that Python has reserved for a particular programmatic purpose, such as the word print.
* Variable names should be short but descriptive. For example, `name` is better than `n`, `student_name` is better than `s_n`, and `name_length` is better than `length_of_persons_name`.
* Be careful when using the lowercase letter l and the uppercase letter O because they could be confused with the numbers 1 and 0.

Because most programs define and gather some sort of data, and then do something useful with it, it helps to classify different types of data. Here we'll go through three commonly used data types, before delving into the project for this week.

## Integers
Ints are simply whole numbers. You can add (+), subtract (-), multiply (*), and divide (/) integers in Python.
```python
print(1 + 1)
print(2 - 1)
print(2 * 1)
print(4 * 1)
```
You can also set variables to integers and then do normal mathematical operations on them
```python
a = 2
b = 1
print(a + b)
```
## Floats
Python calls any number with a decimal point a float. This term is used in most programming languages, and it refers to the fact that a decimal point can appear at any position in a number. Every programming language must be carefully designed to properly manage decimal numbers so numbers behave appropriately no matter where the decimal point appears.

For the most part, you can use decimals without worrying about how they behave. Simply enter the numbers you want to use, and Python will most likely do what you expect:
```python
print(0.1 + 0.1)
print(2.5 - 1.5)
print(2.6 * 1.7)
print(4.5 * 1.75)
```
But be aware that you can sometimes get an arbitrary number of decimal places in your answer:
```python
print(0.2 + 0.1)
print(3 * 0.1)
```
This happens in all programming languages and for right now isn't something to worry about.

You can do the same thing with floats that you could do with integers and set them as variables:
```python
a = 0.2
b = 0.11
print(a * b)
```

You can mix float types and integer types in arithmetical operations resulting in a float type.

## Strings
Since we're going to be using strings to write our silly name generator, our setup will lead to your new program. So, what is a string? A string is simply a series of characters. In Python, anything inside quotes is considered a string. You can use single or double quotes, it really doesn't matter.

So to start, make a new file named `silly_name_generator.py` and write your first string:
```python
silly_name = "bendylick cricketbat"
another_silly_name = 'galileo humpkins'
print(silly_name)
print(another_silly_name)
```
Feel free to use your own silly names, these are just suggestions.

Try running your file in your terminal:
```bash
python3 silly_name_generator.py
```
You'll notice that we set our strings to variables, but you could just have easily printed them without doing that (try it and let your instructor know if you have problems).

Note that if you see an error that says `can't open file 'silly_name_generator.py'`, that probably means that you're trying to run it in a different directory. You might need to change to that directory (using `cd` command) in your terminal. You can always check the lists of the files and their names in the current directory using `ls` command. Use the command `pwd` to check in which directory you are currently.

Now the good thing about strings is that they are easily manipulated in Python. You can change the case in the string, such as making it a title. Going back to your `silly_name_generator.py` file change the `silly_name` variable to a title:
```python
silly_name = "bendylick cricketbat"
another_silly_name = 'galileo humpkins'
print(silly_name.title())
print(another_silly_name)
```
Here the method `title` appears after your variable `silly_name`, which changes the string so it has the grammatical syntax of a title. A method is an action that Python can perform on a piece of data. The dot (.) after name in name.title() tells Python to make the title() method act on the variable name. Every method is followed by a set of parentheses, because methods often need additional information to do their work. That information is provided inside the parentheses. The title() function doesn't need any additional information, so its parentheses are empty. title() displays each word in titlecase, where each word begins with a capital letter. This is useful because you’ll often want to think of a name as a piece of information.

It's worth noting that the method `title` is not changing the value of the variable `silly_name`: if you `print` the variable, you'll see that the result is still all lowercase.
The method `title` is simply returning a new value, that can itself either be used, like in the example with `print`, or saved into another variable.

You can also use methods to change your names into upper case or lower case. The `lower` method is particularly good for data processing.
```python
silly_name = "bendylick cricketbat"
another_silly_name = 'galileo humpkins'
print(silly_name.upper())
print(another_silly_name.lower())
```

### Concatenate Strings
It’s often useful to combine strings. For example, you might want to store a first name and a last name in separate variables, and then combine them when you want to display someone’s full name (almost like we're going to do that in a minute). Change your `silly_name_generator.py` file so it has only a single silly name, but they are split into first and last variables:
```python
first_name = "bendylick"
last_name = "humpkins"
full_name = first_name + " " + last_name
print(full_name)
```
You'll notice I included a blank space between my two variables. What would happen if I forgot this? Try it out if you have time.

Note: even if Python uses the symbol `+` for concatenating strings, you should not assume that it can be safely used with different data types: using it between a string and an int will cause an error.

### F in strings, or string interpolation
As useful as it is to concatenate strings, sometimes you want to place a variable in a string. Enter the f string.
```python
first_name = "bendylick"
last_name = "humpkins"
print(f"{first_name} {last_name}")
```
You'll notice this is much easier than what we wrote above. In Python, simpler is always better.

There are a million things to do with strings, including stripping out white spaces, adding new lines or tabs, and finding an replacing characters. For now, we'll use the above, but feel free to go search out new and interesting things to do with strings in Python!

## Lists
A list is a collection of items in a particular order. You can make a list that includes the letters of the alphabet, the digits from 0–9, or the names of all the people in your family. You can put anything you want into a list, and the items in your list don’t have to be related in any particular way. Because a list usually contains more than one element, it’s a good idea to make the name of your list plural, such as letters, digits, or names.

In Python, square brackets ([]) indicate a list, and individual elements in the list are separated by commas. Here’s a simple example of a list that contains a few names:
```python
names = ["CJ", "Prasoon", "Mihail", "Mariia"]
```
If you put this into your ipython or jupyter notebook, and then `print(names)`, it'll return the list including the brackets. 

### Accessing Elements in a List
Lists are ordered collections, so you can access any element in a list by telling Python the position, or index, of the item desired. To access an element in a list, write the name of the list followed by the index of the item enclosed in square brackets.
For example, let’s pull out the first name in the list `names` (I'm not saying the first position is the best, I'm just saying I wrote this exercise. So in this case... it's the best):
```python
names[0]
```
The above code should return the name of the best instructor in this class.

### Index positions start at 0, not 1
Python considers the first item in a list to be at position 0, not position 1. This is true of most programming languages, and the reason has to do with how the list operations are implemented at a lower level. If you’re receiving unexpected results, determine whether you are making a simple off-by-one error.
The second item in a list has an index of 1. Using this simple counting system, you can get any element you want from a list by subtracting one from its position in the list. For instance, to access the fourth item in a list, you request the item at index 3.
The following asks for the name at index 2 (which is the third name in our list):
```python
names[2]
```

Python has a special syntax for accessing the last element in a list. By asking for the item at index -1, Python always returns the last item in the list:
```python
names[-1]
```

You can use individual values from a list just as you would any other variable. For example, you can use concatenation to create a message based on a value from a list.
Let’s try pulling the first name from the list and composing a message using that value:
```python
message = f"The best instructor in this course is {names[0]}."
print(message)
```

# Putting it all together: Writing a Silly Name Generator
Here we're going to add on to the code you've written above to make a silly name generator. Specifically, we're going to start with two lists: the first and last names. The lists will be relatively short, so they won’t be memory intensive, won’t need to be dynamically updated, and shouldn’t present any runtime issues.

To start you'll need to import some packages. So open your file named `silly_name_generator.py` and write at the top:
```python
import random
```
The random package is included in the python installation, but later in the course we'll use packages we need to import from external repositories. 

Now we'll need two lists. Remember the syntax for lists:
```python
name of list = [things in the list]
```
I can promise that if you copy and paste this code it won't work (bonus if you can explain to your instructor WHY it won't work). But if you make your own list using this syntax: make one named first and one named second and fill each with 5 silly first names and 5 silly last names.

Next you'll need to randomly choose the first name, and the last name from your lists. We start with randomly choosing first name from the list of names:
```python
first_name = random.choice(names)
```
Since the first one is done, you'll need to do the same for the second list. Hint: it would be more fun and sillier if you use different lists for first names and second names.

When you have a silly first name and a silly last name in a variables, we have to put them together, which we'll do with f-strings:
```python
silly_name = f"{first name} {last name}"
```
You'll want to change the above code so it works, and remember to print it out. 


Now go to your terminal and run the code, you should have generated a random silly name, and successfully written another python program! 
If it didn't work, or you have errors, no worries. Just tell CJ, or your instructor and they'll help you work through the errors.

## (optional) A note on style

At this point you might've noticed that we can write strings with either single-quotes or double-quotes. The python language does not distinguish between these two different types of quotes, so these two lines are equivalent:
```
var1 = 'my first string variable'
var2 = "my second string variable"
```

Of course, if you need to write something like `"It's python time"`, it's easier to use double quotes `"` as your "outside string markers". Otherwise it's recommended to just pick either single-quoted strings or double-quoted strings as your 'default' style and then use it everywhere.

In many places, python itself doesn't force you to use any particular style. There's a document called [PEP-8](https://www.python.org/dev/peps/pep-0008/) that recommends a lot of tiny details on where to place spaces and how to format your code. It has a section on quotes, but in case it feels too overwhelming, just add it to your bookmarks and take a look in a few weeks once you are more comfortable with python
