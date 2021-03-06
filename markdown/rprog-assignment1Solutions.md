# Programming Assignment 1, "a more elegant solution"

Students in *R Programming* frequently ask to see other students' work once they have completed their versions of the three functions in the assignment, including `pollutantmean()`, `complete()`, and `corr()`. Often the students want to see what a "good" or "elegant" solution looks like, which is a reasonable request.

Unfortunately the Community Mentors are not allowed to post solutions to these assignments due to the Coursera Honor Code, which stipulates that students are not allowed to post solutions to assignments or quizzes unless directed to do so by course instructors. In the Johns Hopkins University Data Science Specialization, a number of assignments are public, such as the *R Programming* lexical scoping assignment.

Community Mentors have published a variety of content that is applicable to well-written solutions for the first programming assignment, such as techniques for subsetting objects illustrated in the article [Forms of the Extract Operator](http://bit.ly/2bzLYTL). That said, beginning students in *R Programming* need to see how concepts are tied together into an elegant solution. Therefore, it's helpful to paint a more holistic picture of a well-formed solution to these assignments, without giving the assignment answers away.

# What does an "elegant" R program look like?

I see two key characteristics of an elegant R program, including:

1. Code that implements core R concepts (i.e. functional programming) in a minimum number of programming statements, and<br><br>
2. Code that runs efficiently.

On the first point, each of the functions required for *Programming Assignment 1* can be completed in a single statement consisting of nested R functions, once one understands how to use the `apply()` family of functions and comprehends the subtleties of the extract operator. For example, without giving the complete solution, here is what my one line version of `pollutantmean()` uses `lapply()` to drive the bulk of the processing while subsetting both the list of files to be read as well as the specific pollutant, so the result of `unlist()` is a vector of numbers that is used as input to `mean()`.

<img src="./images/rprog-assignment1Solutions01.png">

As one can see from the leftmost part of the one line of code above, by nesting functions we can use the output from the inner functions as input to the outer functions. If one connects them in the right order, one can build the function with a single nested set of R functions.

Similarly, one can code the `complete()` function as follows:

     complete <- function(directory,id=1:332) {
         data.frame(id=id,nobs= # magic happens here
                   )
     }

In this solution we simply pass the `id` argument to the output data frame, and then use code similar to what is in my one line version of `pollutantmean()` to read the files from a directory, and use the list of files as input to an apply function that reads the files and calculates the number of complete cases.

The one statement version of `corr()` is most challenging of the three functions because a single statement solution requires a slightly sophisticated anonymous function within an `apply()` function. One also has to cast the result as a numeric vector with `as.vector()` to ensure the case of an empty result is returned as an empty numeric vector.

On the second point, execution speed, my one line version of `pollutantmean()` is much faster than my original that used a `for()` loop and `rbind()`: 41.48 seconds vs. 1.67 seconds.

<img src="./images/rprog-assignment1Solutions02.png">

Note that the one line versions of `pollutantmean()`, `complete()` and `corr()` were definitely not my original versions of these programs. My first attempts used `for()` loops because I had background in other programming languages where `for()` loops weren't as inefficient as they are in R, and I was following the advice I give in [Strategy for the Programming Assignments](http://bit.ly/2ddFh9A), where I share the old programming aphorism "make it work, make it right, make it fast".

My original solution of `pollutantmean()` covered "make it work" and "make it right," because it produced the correct results, a weighted mean of non-missing cases for all sensor files that are specified by the `id` argument passed to the function. As I developed more skill with R, I was able to refactor the code into functions that perform well, use R more as it is intended, and with fewer overall programming statements.
