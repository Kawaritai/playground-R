# `swirldev/swirl_courses`

- URL: https://github.com/swirldev/swirl_courses

## 1) R Programming

- Start: 07/01/2025

- [x] 1: Basic Building Blocks
  - R does broadcasting or "recycling", so some things just work how we expect them to
  - `c()` to create vectors. Means combine or concatenate
  - `<-` is the assignment operator
- [x] 2: Workspace and Files
  - `getwd()` -- pwd
  - `setwd()` -- cd
  - `ls()` -- objects in your workspace (like variables)
  - `list.files()` or `dir()` for files in wd.
  - `args(func_obj)`
  - Use `file.some_method` for some method related to files
  - Use `dir.some_method` for directories, like creating them
    - Use `recursive = TRUE` for nested folders in one shot: `dir.create(file.path("testdir2", "testdir3"), recursive = TRUE)`
  - Remove files and (if recursive = TRUE) directories, `unlink()`
- [x] 3: Sequences of Numbers
  - For a range, just use a colon. `1:20`
    - To get the documentation, use `` ?`:`  `` with the backticks
  - For more control than that, use `seq()`
  - For repeating, use `rep(val, times = X)`
    - `val` can be a vector created with `c()`
    - When it is a vector, you can use `times` or you can use `each = X` to repeat _each_ element
- [x] 4: Vectors
  - `paste()` has arguments `sep` and `collapse`
    - `> paste(1:3, c("x", "y", "z"), sep = ":", collapse = "|")`
    - `[1] "1:x|2:y|3:z"`
  - In some cases of vector recycling in R, you can basically consider it as tiling
- [x] 5: Missing Values
  - NaN's can creep up - just compare `is.nan()` and `== NaN`
- [x] 6: Subsetting Vectors
  - "**Index vectors** come in four different flavors -- logical vectors, vectors of positive integers, vectors of negative integers, and vectors of character strings"
  - `x[is.na(x)]` returns a vector with all NAs (Why? Because `is.na()` tells you where the NAs are)
  - R does 1-based indexing :|
  - `x[c(-2, -10)]` or `x[-c(2, 10)]` gives all elements EXCEPT at idx 2 and 10
- [ ] 7: Matrices and Data Frames
  - "**Matrices** can only contain a single class of data, while **data frames** can consist of many different classes of data."
  - A vector has NULL dimensions.
  - `dim()` can check dimensions or be used to assign
    - When we changed the `dim` on the vector, it's effectively a `reshape` like in Python
  - For rows and cols "labels":
    - Rows: `my-data <- data.frame(patients, my_matrix)`. Using cbind keeps the matrix, but the numbers become **character vectors** (implicit coercion)
    - Cols: `colnames(my_data) <- cnames`
      `names()` and `colnames()
- [x] 8: Logic
  - You can use the `&` operator to evaluate AND across a vector. The `&&` version of AND only evaluates the first member of a vector.
  - The `|` version of OR evaluates OR across an entire vector, while the `||` version of OR only evaluates the first member of a vector.
  - For `isTRUE()`, it is checking for exactly the value TRUE (not just true-ey)
  - The `which()` function takes a logical vector as an argument and returns the indices of the vector that are TRUE.
  - The `any()` function will return TRUE if one or more of the elements in the logical vector is TRUE.
  - The `all()` function will return TRUE if every element in the logical vector is TRUE.
  ```R
  > ints > 7
  [1] FALSE FALSE  TRUE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE
  > ints[ints > 7]
  [1]  9  8 10
  ```
- [x] 9: Functions
  - To understand computations in R, two slogans are helpful: 1. Everything that exists is an object. 2. Everything that happens is a function call.
  ```R
    function_name <- function(arg1, arg2) {
      # Manipulate arguments in some way
      arg1 # Last expression returned
    }
  ```
  - If you specify argument names during the function call, order doesn't matter
  - `args()` exists, remember?
  - Anonymous functions: not named
    - `function(x){x+1}`, for example
  - Just as in `?paste`, the ellipsis, `...` means any number of arguments to be passed
- [x] 10: `lapply` and `sapply`
  - `lapply` and `sapply` are the two most important members of R's \*apply family of functions, also known as loop functions.
  - Used for **Split-Apply-Combine strategy** for data analysis
    - EACH (!) of the \*apply functions will **SPLIT** up some data into smaller pieces,
    - **APPLY** a function to each piece,
    - then **COMBINE** the results.
    - (A more detailed discussion of this strategy is found in Hadley Wickham's Journal of Statistical Software paper titled 'The Split-Apply-Combine Strategy for Data Analysis'.)
  - `lapply`: list apply a (data, func). Returns list of same length (with dim = 0 and same length
    - It _is_ a list, doesn't it kind of act like a vector? (nah. in this case, the return object is a list with keys assigned to single character vectors)
  - You can think of:
    - [] as "give me a sublist containing these elements"
    - [[]] as "follow this name/index to its destination and give me what's there"
  - `sapply`: simplify list. It can be used similarly to `lapply`, but will try simplify the result for you, if the result plays nice. 
  - If `cls_list` is a list of character vectors,
- [x] 11: `vapply` and `tapply`
  - `vapply`: similar to `sapply`, but has a pre-defined type of return value. For safety and speed. Think `v` for helicopter-parenting the return Value.
    - Okay, so in R, it's characters not strings
  - `tapply`: Apply a function to each cell of a ragged array. Think, table-apply because we can break down the X and INDEX using `table` to see what we're working with.
    - "The function factor is used to encode a vector as a factor (the terms ‘category’ and ‘enumerated type’ are also used for factors)."
    - use tapply() to split your data into groups based on the value of some variable, then apply a function to each group
- [x] 12: Looking at Data
  - Aaaand `str()` is not string but "structure"! It concisely combines many features of other functions, like `summary()` and `head/last` and `class` and `dim`...
- [x] 13: Simulation
  - `sample(x)` is shorthand for permuting the elements (when you exclude size and default replace = FALSE)
  - use `replicate(n, distribution)` to repeat an operation `n` times, like taking multiple group samples
  - use `colMeans` to take the mean over each column of, for instance, a matrix of arrays. For a matrix of dim `5 100`, taking `colMeans` returns a numeric vector
- [x] 14: Dates and Times
  - Dates are represented by the 'Date' class and times are represented by the 'POSIXct' and 'POSIXlt' classes. 
    - Internally, dates are stored as the number of days since 1970-01-01 and times are stored as either the number of seconds since 1970-01-01 (for 'POSIXct') or a list of seconds, minutes, hours, etc. (for 'POSIXlt').
  - If something is wrapped in a class, like a "Date", use `unclass()` to view internals
     - For instance, R **internally** stores dates by number of days since 1970-01-01. Also stores negative numbers
  - `Sys.Date()` and `Sys.time()` and `as.Date("formatted character")`
    - The `Sys.time()` is by default `POSIXct` (Calendar Time) class -- stored by seconds since the reference
    - `POSIXlt` (Local Time) is more detailed, with names
  - `weekdays()`, `months()`, `quarters()`...
    - _"What month is it?", "You mean... what quarter?"_
  - `strptime()` converts character vectors to POSIXlt. Kind of a more lenient `as.POSIXlt()`
  - Use arithmetic operators as expected
    - `Sys.time() > t1`
    - `difftime(Sys.time(), t1, units = 'days')`
    
- [x] 15: Base Graphics
  - `plot` is short for scatterplot.. huh.
  - Introduced `par()` and `points` but... with no other exercises _for_ them?
  - If you want to explore other elements of base graphics, then this web page (http://www.ling.upenn.edu/~joseff/rstudy/week4.html) provides a useful overview.

## 2) Getting and Cleaning Data

N/A

## 3) Exploratory Data Analysis

N/A

## 4) Statistical Inference

N/A

## 5) Regression Models

N/A
