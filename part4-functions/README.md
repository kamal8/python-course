# Functions

Functions in programming languages are only partially similar to functions in math: it's a piece of code that can be parametrised and that results in some object. So if you need to perform a task multiple times throughout your program, you don’t need to type all the code for the same task again and again; you just call the function dedicated to handling that task, and the call tells Python to run the code inside the function.

## Defining a Function

The first part of a function is defining it. Here's a definition of a function that prints two lines every time you run it:

```python
def my_function():
    print("Hello")
    print("there")
```

The function definition itself has several distinct parts: the special word `def` tells python that this is a block of code that defines function. We have a function name then `my_function` followed by parenthesis and a colon (more on this later). Then every line of code in the indented block is called "function body" and python knows that these are the instructions needs to be run when you call this function. Once you define this function you can call it wherever you want in your code by using its name and the parenthesis: `my_function()`. Speaking of names though...

## Naming stuff **is** hard

Similar to setting a value to a variable, defining a function gives you something to call when you want to use that function. Also similar to a variable names, the function name should be long enough to be descriptive but short enough to make it easy to repeat. Here are a few examples:

```python
# too generic
def function():
    # some function statements

# too long
def function_to_do_all_the_things_i_want_it_to_do_and_more():
    # some function statements

# just right
def silly_name_generator():
    # some function statements
```

Don't become too attached to the name you pick, as you can always change it later if you realise that the function's purpose has changed too much. It is also a good idea to avoid generic names like `get`, `do_things`, or `run_stuff`: the ideal name should hint what the function does without you having to take a look at the definition.

## Passing Information to a Function

Those paranthesis are there to introduce parameters in your code.
You can pass information to the function by including _function arguments_ between the parentheses of your function definition. By adding the argument you allow the function to accept different values and perform the same tasks with this variable. You don't have to define arguments for a function to do something useful but it's usually a good idea to see what can be "templated".

Consider this function:

```python
def greet_user():
    print("Hello user")
```

It will print `Hello user` every time you call it. What if we want to parametrize it? We can do that if we set a username as a parameter:

```python
def greet_user(username):
    print(f"Hello {username}")
```

The function now expects you to provide a value for an argument each time you call it. When you call `greet_user("jesse")`, it will print "Hello jesse".
Here's a more advanced example: suppose we want to have a function which checks whether a specific drink is available in Berlin offices:

```python
def berlin_beverage_is_available(drink_name):
    available_beverages = ['mate', 'beer', 'wine', 'coffee', 'tea']
    if drink_name in available_beverages:
        print(f"We have {drink_name} in store!")
    else: 
        print(f"Sorry, we don't have {drink_name} in Berlin offices")
```

If we want to use the function we'll need to call it, and include a parameter for the argument `drink_name`.

```python
berlin_beverage_is_available('cocktail')
berlin_beverage_is_available('coffee')
```

And so, we can put anything we want as an argument for our `berlin_beverage_is_available` function.

## Passing Multiple Arguments

Because a function definition can have multiple parameters, a function call may need multiple arguments. When you call your function you can pass arguments to your functions in a two main ways: when using positional arguments they need to be passed in the same order the parameters were written; or you can use keyword arguments where each argument would consist of a variable name and a value. Let’s look at each of these in more details turn.

Suppose we have a function like this:

```python
def make_introduction(name, department, university):
    print(f"Hi, I'm {name}, and I am from {major} department at {university}")
```

If you want to use these as **positional** arguments, you just need to feed the parameters in the same order that the arguments are defined in the function:

```python
# feel free to make these match with your name, department, etc.
make_introduction('Igor','Materials','Stockholm University')
```

But remember, here order matters! If you call the function like that, it would work sure but the result might not be what you want: python cannot guess what you _meant_ to do it will only do what you _told_ it to do.

```python
make_introduction('Materials', 'Igor', 'Stockholm University')
```

Alternatively, you can use **keyword** arguments. Because you're passing a specific name-value pair, the order doesn't matter and it avoids confusion. It frees you from having to worry about correctly ordering your arguments in the function call and clarifies the role of each value in the function call.

```python
# again feel free to replace the info here with your info
make_introduction(university='Stockholm University', name='Igor', department='Materials')
```

## Default Values

When writing a function, you can also define a default value for each parameter. If an argument for a parameter is provided in the function call, Python uses the argument value. If not, it uses the parameter’s default value. So when you define a default value for a parameter, you can exclude the corresponding argument you’d usually write in the function call. Using default values can simplify your function calls and clarify the ways in which your functions are typically used.

```python
def berlin_beverage_is_available(drink='beer'):
    beverages = ['mate', 'beer', 'wine', 'cofffee', 'tea']
    if drink in beverages:
        print(f"We have {drink} in store!")
    else: 
        print(f"Sorry, we don't have {drink} in Berlin")
```

Now, whenever I call the `berlin_beverage_is_available` function I'll get a beverage check for _"beer"_, unless I include a different parameter explicitly.

```python
berlin_beverage_is_available() # -> automatically fills in "beer" as the argument
berlin_beverage_is_available('coffee')
berlin_beverage_is_available('wine')
```

It is a good idea when you write code to spot tho most common values for parameters so that you wouldn't need to specify them every time.

## Return values

A function doesn’t always have to display its output directly. Instead, it can process some data and then return a value or set of values. The value the function returns is called a return value. The return statement takes a value from inside a function and sends it back to the line that called the function. Return values allow you to move much of your program's grunt work into functions, which can simplify the body of your program.

Let's write a function that uses dictionary, checks for values and returns a value from dict _or_ prints an error and returns nothing. Something like this:

```python
def sunday_activity(mood="relaxing"):
    mood_action_dict = {
        'relaxing': 'took a nice walk outside',
        'focused': 'work or write python class', 
        'nervous': 'cleaned', 
        'lazy': 'watched a movie', 
        'athletic':'rode a bike', 
        'hungry': 'had a picnic with friends', 
        'clear': 'read'
    }

    if mood not in mood_action_dict:
        print(f"Sorry, the emotional range does not extend to {mood}")
        return

    return mood_action_dict[mood]
```

So when you want to figure out what was the mood-related activity on Sunday, you can call the function like this:

```python
activity = sunday_activity() # -> see default parameter in the function
print(activity)
```

or like this:

```python
activity = sunday_activity('focused')
print(activity)
```

The example is a bit complex and this might seem to look like a lot of work to just figure out what was the Sunday activity, but when you work with larger programs small functions like this can be very useful. Don't let the "smalliness" of the code you're using stop you from creating a function. 

There's a rule of thumb you can use to decide when to write a function: if you have some code that you wrote already three times in you program, then it's a good idea to step back and think if this code can be a function instead. The main reason is that when you would want to change it later, you want to change the code in as few places as possible and functions are awesome at helping you achieve that.

## Today's project

In today's project you're going to revisit things you have already done and wrap them into functions. I'll give you the building blocks, but the majority of the function is going to be empty and you'll need to figure out what belongs there (hint: it's the code from the previous sessions). If you get stuck, don't worry, just ask your instructor.

### Section1: silly name generator function

In first section we would build a silly name generator, using two lists and choosing from the lists at random.
Here we'll write a function to do that. We'll start with the definition. The function is using two lists so we will pass them as parameters:

```python
def silly_name_generator(first_names, last_names):
```

and we'll want to return our silly name:

```python
def silly_name_generator(first_names, last_names):
    # complete this function by replacing these comments with correct logic
    # YOUR CODE TO GET A SILLY NAME GOES HERE
    # some code statement1
    # some code statement2
    # some code statement3
    # etc

    return silly_name
```

Now your task is to fill in the logic to complete the function. Don't forget that you'll need to call the function with a list of silly first names and silly last names. So the code you'll use to run the function will look like this:

```python
silly_first_names = [] # -> fill this with a bunch of silly first names
silly_last_names = [] # -> fill this with a bunch of silly last names

silly_name = silly_name_generator(silly_first_names, silly_last_names)
print(silly_name)
```

### Section2: word counter function

Here you'll actually want to have two functions: one to load in your dataset and return the list of words, and one to count the words.

```python
def load_word(path_to_word_file):  
    
    # YOUR CODE TO LOAD THE WORD FILE

    return loaded_text
```

and now call the `load_word` function WITHIN your word counter function:

```python
def word_counter():
    loaded_text = load_word('path where your file is located')

    # YOUR CODE TO COUNT WORDS

    return num_of_words
```

### Section3: anagram finder function

Finally, let's make your anagram finder into a function. It might make more sense to have two functions, one where you clean and sort your word, and one which looks for the anagrams of your cleaned and sorted word. But I leave that up to you.

```python
def anagram_finder():
    
    # YOUR CODE TO FIND ANAGRAMS
    # THIS MAY INCLUDE FUNCTION TO CLEAN YOUR WORD 🤷‍♀️

    return anagram_list
```

### More exercises?

That's a lot for today, but if you want/need/crave more python function writing practice, try a few of the below:

* Write a function called `make_shirt()` that accepts a size and the text of a message that should be printed on the shirt. The function should print a sentence summarizing the size of the shirt and the message printed on it (a function like that might be used in context of an online catalogue). Call the function once using positional arguments to make a shirt. Call the function a second time using keyword arguments.
* Modify the `make_shirt()` function so that shirts are large by default with a message that reads _"I love Python"_. Make a large shirt and a medium shirt with the default message, and a shirt of any size with a different message.
* Write a function called `city_country()` that takes in the name of a city and its country. The function should return a string formatted like this: `Santiago, Chile`. Then, call your function with at least three city-country pairs, and print the value that’s returned.
* Write a function called `make_album()` that builds a dictionary describing a music album. The function should take in an artist name and an album title, and it should return a dictionary containing these two pieces of information. Use the function to make three dictionaries representing different albums. Print each return value to show that the dictionaries are storing the album information correctly.

## "Fun" fact

Everything in python is an object, more or less. Therefore, python functions are objects as well. You can use the function `type` to check what type it has:

```python
def func():
    print("test func")

print(type(f))
```
