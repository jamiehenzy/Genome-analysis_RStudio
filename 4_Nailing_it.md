# For loops and the apply family of functions
A few useful commands: function(), is.na, which, var, length, for(){ }, 
 points, print, paste, plot, unique, sample
 
for loops: 
In many languages, the best way to repeat a calculation is to use a for-loop:
For example, we could square each number 1 to 10
```{r, echo=T}
squares = rep(NA, 10) # use rep to create a vector length 10 of NAs to store the result
for (i in 1:10) { # for loop
  squares[i] = i^2
}
squares
```
An alternative to for-loops in R is using the 'apply' family, while for-loops apply a function to one item at a time and then go on to the next one, "apply" applies functions to every item at once
## apply family
### sapply
There are several apply functions that vary in the output the return and vary somewhat in the input they require. We'll go over **sapply** "simplifying" apply which returns a vector, first.
```{r, echo=T}
#?sapply 
# syntax: sapply(X = object_to_repeat_over, FUN = function_to_repeat)
# simple example of sapply over a vector
# we can use an in-line function definition
sapply(1:10, function(x)  x^2)
# equivalently, we can define our own functions separately for sapply
# e.g. a function that calculates the area of a circle radius r, pi*r^2
areaCircle = function(r){
  return(pi * r^2)
}
sapply(1:10, areaCircle)
# in R, we can also just use short-hand for simple vector calculations:
pi*(1:10)^2
# but unlike the short-hand, sapply can also iterate over elements in a list
listy = list(a = TRUE, b = c("a", "b", "c"), c = 10:100)
str(listy) # look at the structure of 'listy'
length(listy) # look at the length of 'listy'
# use sapply to return a vector for length of each object within the list
sapply(listy, FUN = length) 
```
You can also use sapply to create plots! For example, use sapply to plot these 4 dataframes at once:
```{r, label='5-33', echo=T}
df1 = data.frame(x1 = 1:10, y1 = 1:10)
df2 = data.frame(x2 = 1:10, y2 = -1:-10)
df3 = data.frame(x3 = 1:10, y3 = 10:1)
df4 = data.frame(x4 = 1:10, y4 = 1:10)
my_list = list(df1, df2, df3, df4) # put 4 data frames together in a list
par(mfrow = c(2,2)) # set up frame for 4 plots
sapply(my_list, plot) # plot my_list with sapply
```
### apply 
The apply function is highly useful for applying a function to rows or columns of a dataframe or matrix. 
Example syntax for the dataframe or matrix X:
`apply(X = over this object, MARGIN 1 for rows or 2 for columns,FUN = apply this function)`
You can also use apply on a dataframe we worked with earlier the states data to plot each column against Population
```{r, echo=T}
#load in the data
data(state)
states = as.data.frame(state.x77) # convert data to a familiar format - data frame
str(states) # let's take a look at the dataframe
# calculate the mean for each column
apply(states, 2, mean)
# note you could get this with colMeans() or summary(), along with the min and max and other values, but there may be instances where you only want the mean
# you could also plot each column against Population in ggplot
```
```{r, label='5-29', echo=T}
apply(states, 2, FUN = function(i) ggplot(states, aes(x=Population, y = i))+geom_point()+geom_smooth(method="lm")+theme_classic())
```
We can do the same things across all rows. But if you want to plot all the rows as we did the columns above, I suggest you do that with a smaller dataset than the states dataframe.
```{r, echo=T} 
#calculate the sum across each row in states
apply(states, 1, sum)
```
### lapply -- "list" apply
We'll just show a quick example of lapply. It works in the same way as sapply, but returns a list instead of a vector.
```{r, echo=T}
lapply(1:10, function(x)  x^2) # lapply returns list
sapply(1:10, function(x)  x^2, simplify = FALSE) # same as an lapply
sapply(1:10, function(x)  x^2) # default is simplify = TRUE which retuns a vector
```
### tapply - "per Type" apply 
The tapply function is one of my favorites because it is a really great way to sumarize data that has multiple categorical variables that can be 

```{r, echo=T}
# load state data again, you can skip this if you already have it loaded
data(state)
states = as.data.frame(state.x77) # convert data to a familiar format - data frame
str(states) # let's take a look at the dataframe
# example syntax --- tapply(variable of interest, grouping variable, function)
# for each US region in our dataset, finds the mean of Frost for states in that region
tapply(states$Frost, state.region, mean) # state.region contains the region information for each state
# you can nest apply statements! Let's find the region average for all the variables in the states dataset
apply(states,
      2, # apply over columns of my_states
      function(x) tapply(x, state.region, mean)) # each column = variable of interest for tapply
```
## Exercise 3: apply and tapply
Read in the exer_3.R script and fill in the commands as needed. Don't forget to save your work for submission!
