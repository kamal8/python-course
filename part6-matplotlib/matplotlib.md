A picture is worth a thousand words, and with Python’s matplotlib library, it fortunately takes far less than a thousand words of code to create a production-quality graphic.

However, matplotlib is also a massive library, and getting a plot to look just right is often achieved through trial and error. Using one-liners to generate basic plots in matplotlib is fairly simple, but skillfully commanding the remaining 98% of the library can be daunting.

One important big-picture matplotlib concept is its object hierarchy. A “hierarchy” here means that there is a tree-like structure of matplotlib objects underlying each plot.

A Figure object is the outermost container for a matplotlib graphic, which can contain multiple Axes objects. One source of confusion is the name: an Axes actually translates into what we think of as an individual plot or graph (rather than the plural of “axis,” as we might expect).

You can think of the Figure object as a box-like container holding one or more Axes (actual plots). The Axes in the hierarchy are smaller objects such as tick marks, individual lines, legends, and text boxes. Almost every “element” of a chart is its own manipulable Python object, all the way down to the ticks and labels.

Let's start by importing matplotlib:
```python
import matplotlib.pyplot as plt
```
Similar to importing pandas as pd, this alias is commonly used and you'll see it everywhere. 

Here’s an illustration of this hierarchy in action. Don’t worry if you’re not completely familiar with this notation, we'll cover it in a minute:

```python
fig, _ = plt.subplots()
type(fig)
```
Above, we created two variables with plt.subplots(). The first is a top-level Figure object. The second is a “throwaway” variable that we don’t need just yet, denoted with an underscore. Using attribute notation, it is easy to traverse down the figure hierarchy and see the first tick of the y axis of the first Axes object:
```python
one_tick = fig.axes[0].yaxis.get_major_ticks()[0]
type(one_tick)
```
Above, fig (a Figure class instance) has multiple Axes (a list, for which we take the first element). Each Axes has a yaxis and xaxis, each of which have a collection of “major ticks,” and we grab the first one.
Alright, we need one more chunk of theory before we can get around to the shiny visualizations: the difference between the stateful (state-based, state-machine) and stateless (object-oriented, OO) interfaces.

Above, we used import matplotlib.pyplot as plt to import the pyplot module from matplotlib and name it plt.

Almost all functions from pyplot, such as plt.plot(), are implicitly either referring to an existing current Figure and current Axes, or creating them anew if none exist. Hidden in the matplotlib docs is this helpful snippet:

“[With pyplot], simple functions are used to add plot elements (lines, images, text, etc.) to the current axes in the current figure.”

In English, this means that:

The stateful interface makes its calls with plt.plot() and other top-level pyplot functions. There is only ever one Figure or Axes that you’re manipulating at a given time, and you don’t need to explicitly refer to it.
Modifying the underlying objects directly is the object-oriented approach. We usually do this by calling methods of an Axes object, which is the object that represents a plot itself.

Tying these together, most of the functions from pyplot also exist as methods of the matplotlib.axes.Axes class.

This is easier to see by peeking under the hood. plt.plot() can be boiled down to five or so lines of code:
```python
def plot(*args, **kwargs):
    """An abridged version of plt.plot()."""
    ax = plt.gca()
    return ax.plot(*args, **kwargs)

def gca(**kwargs):
    """Get the current Axes of the current Figure."""
    return plt.gcf().gca(**kwargs)
```
Calling plt.plot() is just a convenient way to get the current Axes of the current Figure and then call its plot() method. This is what is meant by the assertion that the stateful interface always “implicitly tracks” the plot that it wants to reference.

Alright, enough theory. Now, we’re ready to tie everything together and do some plotting. From here on out, we’ll mostly rely on the stateless (object-oriented) approach, which is more customizable and comes in handy as graphs become more complex.

### My first plot
First let's see what a plot looks like with entirely made up numbers:
```python
plt.plot([1, 2, 3, 4])
plt.ylabel('some numbers')
plt.show()
```
You may be wondering why the x-axis ranges from 0-3 and the y-axis from 1-4. If you provide a single list or array to plot, matplotlib assumes it is a sequence of y values, and automatically generates the x values for you. Since python ranges start with 0, the default x vector has the same length as y but starts with 0. Hence the x data are [0, 1, 2, 3].

plot is a versatile function, and will take an arbitrary number of arguments. For example, to plot x versus y, you can write:
```python
plt.plot([1, 2, 3, 4], [1, 4, 9, 16])
```
For every x, y pair of arguments, there is an optional third argument which is the format string that indicates the color and line type of the plot. The letters and symbols of the format string are from MATLAB, and you concatenate a color string with a line style string. The default format string is 'b-', which is a solid blue line. For example, to plot the above with red circles, you would write:
```python
plt.plot([1, 2, 3, 4], [1, 4, 9, 16], 'ro')
plt.axis([0, 6, 0, 20])
plt.show()
```
See the plot documentation for a complete list of line styles and format strings. The axis function in the example above takes a list of [xmin, xmax, ymin, ymax] and specifies the viewport of the axes.

If matplotlib were limited to working with lists, it would be fairly useless for numeric processing. Generally, you will use numpy arrays. In fact, all sequences are converted to numpy arrays internally. The example below illustrates plotting several lines with different format styles in one function call using arrays.
```
import numpy as np

# evenly sampled time at 200ms intervals
t = np.arange(0., 5., 0.2)

# red dashes, blue squares and green triangles
plt.plot(t, t, 'r--', t, t**2, 'bs', t, t**3, 'g^')
plt.show()
```

## Plotting with Pandas
Now we're going to work with pandas dataframe and plotting:
```python
import pandas as pd

dataframe = pd.read_csv("scottish_hills.csv")
```
Let’s have a look at the relationship between two varibles in our Scottish hills data. Suppose I have a hypothesis that the height of Scottish hill increases with latitude northwards. Were going to plot height against latitude. To save typing later on, we can extract the Series for “Height” and “Latitude” by assigning each to a new variable, x and y, respectively.
```python
plt.scatter(dataframe['Height'], dataframe['Latitude'])
plt.show()
```
Cool, but the strength of plotting with matplotlib is being able to add to your plot. See some of the options below.

```python
# Change the default figure size
plt.figure(figsize=(10,10))

# Change the default marker for the scatter from circles to x's
plt.scatter(dataframe['Height'], dataframe['Latitude'], marker='x')

# Add x and y lables, and set their font size
plt.xlabel("Height (m)", fontsize=20)
plt.ylabel("Latitude", fontsize=20)

# Set the font size of the number lables on the axes
plt.xticks(fontsize=18)
plt.yticks(fontsize=18)

plt.savefig("python-linear-reg-custom.png")
```

So now we know enought plt to be dangerous, let's further explore plotting... with pandas (surprise twist!).
The pandas package has a .plot() method in the dataframe class that uses matplotlib.

For this we're going to use a different dataset, that you should be able to download like this:

```python
import pandas as pd

download_url = ("https://raw.githubusercontent.com/fivethirtyeight/data/master/college-majors/recent-grads.csv")

df = pd.read_csv(download_url)
```
Now to display the plot in the jupyter notebook immediately (without calling plt.show())
```python
%matplotlib inline
```
Now you simply call the plot method of your dataframe
```python
df.plot(x="Rank", y=["P25th", "Median", "P75th"])
```
.plot() returns a line graph containing data from every row in the DataFrame. The x-axis values represent the rank of each institution, and the "P25th", "Median", and "P75th" values are plotted on the y-axis.

.plot() has several optional parameters. Most notably, the kind parameter accepts eleven different string values and determines which kind of plot you’ll create:

"area" is for area plots.
"bar" is for vertical bar charts.
"barh" is for horizontal bar charts.
"box" is for box plots.
"hexbin" is for hexbin plots.
"hist" is for histograms.
"kde" is for kernel density estimate charts.
"density" is an alias for "kde".
"line" is for line graphs.
"pie" is for pie charts.
"scatter" is for scatter plots.

The default value is "line". Line graphs, like the one you created above, provide a good overview of your data. You can use them to detect general trends. They rarely provide sophisticated insight, but they can give you clues as to where to zoom in.

If you don’t provide a parameter to .plot(), then it creates a line plot with the index on the x-axis and all the numeric columns on the y-axis. While this is a useful default for datasets with only a few columns, for the college majors dataset and its several numeric columns, it looks like quite a mess.

The next plots will give you a general overview of a specific column of your dataset. First, you’ll have a look at the distribution of a property with a histogram. Then you’ll get to know some tools to examine the outliers.

### Distributions and Histograms
DataFrame is not the only class in pandas with a .plot() method. As so often happens in pandas, the Series object provides similar functionality.

You can get each column of a DataFrame as a Series object. Here’s an example using the "Median" column of the DataFrame you created from the college major data:
```python
median_column = df['Median']
```
Now that you have a Series object, you can create a plot for it. A histogram is a good way to visualize how values are distributed across a dataset. Histograms group values into bins and display a count of the data points whose values are in a particular bin.

Let’s create a histogram for the "Median" column:
```python
median_column.plot(kind="hist")
```
You call .plot() on the median_column Series and pass the string "hist" to the kind parameter. That’s all there is to it!

### Analyze Categorical Data
To process bigger chunks of information, the human mind consciously and unconsciously sorts data into categories. This technique is often useful, but it’s far from flawless.

Sometimes we put things into a category that, upon further examination, aren’t all that similar. In this section, you’ll get to know some tools for examining categories and verifying whether a given categorization makes sense.

Many datasets already contain some explicit or implicit categorization. In the current example, the 173 majors are divided into 16 categories.

### Grouping
A basic usage of categories is grouping and aggregation. You can use .groupby() to determine how popular each of the categories in the college major dataset are:
```python
cat_totals = df.groupby("Major_category")["Total"].sum().sort_values()
```
With .groupby(), you create a DataFrameGroupBy object. With .sum(), you create a Series.

Let’s draw a horizontal bar plot showing all the category totals in cat_totals:

```python
cat_totals.plot(kind="barh", fontsize=4)
```
### Determining Ratios
Vertical and horizontal bar charts are often a good choice if you want to see the difference between your categories. If you’re interested in ratios, then pie plots are an excellent tool. However, since cat_totals contains a few smaller categories, creating a pie plot with cat_totals.plot(kind="pie") will produce several tiny slices with overlapping labels .

To address this problem, you can lump the smaller categories into a single group. Merge all categories with a total under 100,000 into a category called "Other", then create a pie plot:
```python
small_cat_totals = cat_totals[cat_totals < 100_000]

big_cat_totals = cat_totals[cat_totals > 100_000]

small_sums = pd.Series([small_cat_totals.sum()], index=["Other"])

big_cat_totals = big_cat_totals.append(small_sums)

big_cat_totals.plot(kind="pie", label="")
```

### Zooming in on Categories
Sometimes you also want to verify whether a certain categorization makes sense. Are the members of a category more similar to one other than they are to the rest of the dataset? Again, a distribution is a good tool to get a first overview. Generally, we expect the distribution of a category to be similar to the normal distribution but have a smaller range.

Create a histogram plot showing the distribution of the median earnings for the engineering majors:
```python
df[df["Major_category"] == "Engineering"]["Median"].plot(kind="hist")
```

## Extra
This has been a lot. But if you're eager for more here are some additional resources:
* We only went through one of the popular plotting libraries for python. If you want to try another, take seaborn out for a spin: [https://seaborn.pydata.org/tutorial.html]
* Or try plotly, for interactive plots: [https://plotly.com/python/plotly-fundamentals/]
* Or Prasoon's personal favorite plotting, Altair, similar to ggplot in R: [https://www.datacamp.com/community/tutorials/altair-in-python]
*  Or here are some pandas and matplotlib projects you can try your hand at:
[https://www.fullstackpython.com/pandas-code-examples.html]
[https://github.com/schlende/practical-pandas-projects]
