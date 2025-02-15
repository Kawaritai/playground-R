# `swirldev/swirl_courses`

- URL: https://github.com/swirldev/swirl_courses
- Installation:
  ```R
  # 1. Make sure you have a recent version version of swirl:
  install.packages("swirl")
  # 2. Enter the following from the R console, substituting the name of the course that you wish to install:
  library(swirl)
  install_course("Course Name Here")
  swirl()
  ```


## 1) R Programming

- **Start**: 07/02/2025
- **Command**: 
  ```R
  install_course("R Programming")
  ```

### Notes
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
- [x] 7: Matrices and Data Frames
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

- **Start**: 15/02/2025ß
- **Command**: 
  ```R 
  install_course("Getting and Cleaning Data")
  ```\
- Key packages: `dplyr`, `tidyr`, `lubridate`

### Notes
- [x] 1: Manipulating Data with `dplyr`
  - `dplyr` is for manipulating tabular data from a variety of sources (data frames, data tables, databases, multidim. arrays)
    - Think: Dataframe-pliers
  - In using `dplyr`, the first step is to load the data into a "data frame tbl" or `tbl_df`. You can use the function `tbl_df()`. 
    - Colloquially, we call this a `tibble`: referring to a data frame that has the `tbl_df` class
  - Core philosophy: small functions that each do one thing well.
    - `dplyr` supplies five 'verbs' that cover most fundamental data manipulation tasks: `select()`, `filter()`, `arrange()`, `mutate()`, and `summarize()`
    - E.g. use `select()` rather than `tbl_df()$attr1`, `tbl_df()$attr2`, `tbl_df()$attr3`. Additionally, you can use the `:` operator as logically. 
  - Think: `select()` to choose from columns; `filter()` to choose from rows.
  - `arrange()` orders rows and is ascending by default:
    - Asc: `arrange(tbl_df(), col1)`
    - Desc: `arrange(tbl_df(), desc(col1))`
  - `mutate()` creates new columns that are functions of existing variables. 
    - This, as with all previous functions, doesn't modify the original `tbl_df` -- it returns a new one. 
  - `summarize()` collapses the dataset to a single row. 
    - Akin to aggregate functions in SQL and `GROUP_BY`, sort of.
    - "The idea is that `summarize()` can give you the requested value FOR EACH group in your dataset."
- [x] 2: Grouping and Chaining with `dplyr`
  - In this lesson, we go into the `summarize()` aggregating function. 
  - `group_by(tbl_df, attr)` converts an existing tibble into a **grouped tibble** where operations are performed "by group"
    - `ungroup()` removes the grouping
    - Doesn't look different in the console, except you see `Groups: attr`
    - We can further use `summarize()` on the grouped table to apply aggregate operations by-grouping. 
    - `n()`, `n_distinct(notgroupattr)`, `mean(notgroupattr)` are examples. In particular, `n()` gives the current group size (e.g. you can use it to count instances within a group)
  - `quantile(pack_sum$count, probs = 0.99)` to get the 99% sample quantile based on the `count` value (size of groups, in this case). 
  - `View(tibble)` to open a View of the data. Capitalised.
  - Chaining allows you to string together multiple function calls in a way that is compact and readable. 
    - Advantage: We don't have to store intermediate results. 
  - `%>%` is the chaining operator. You can pronounce it as "then"
    - `?chain` for documentation
    - `left %>% right`: the code on the right operates on the output of the left. 
    - Notably, we don't need to specify the dataset. E.g. `select(cran, ...)` is `cran %>% select(...)`
    - In fact, at the end, you can just write `%>% print()`
    - Start chaining by specifying the dataset or assign by `variable <- tibble %>% chaining....`
- [x] 3: Tidying Data with `tidyr`
  - "This paper should be required reading for anyone who works with data, but it's not required in order to complete this lesson": [http://vita.had.co.nz/papers/tidy-data.pdf](http://vita.had.co.nz/papers/tidy-data.pdf)
    - Okay but it's 24 pages
    - [ ] TODO: Read.
  - Tidy data is formatted in a standard way that facilitates exploration and analysis and works seamlessly with other tidy data tools. Specifically, tidy data satisfies three conditions:
    1. Each variable forms a column
    2. Each observation forms a row
    3. Each type of observational unit forms a table
  - "Messy" data doesn't satisfy these conditions. 
  - `gather(data, key="", value="", ...,)` makes wide data longer.
    - `key` is the new column that the previous column names (as selected) inhabit
    - `value` is the new column that the previous column values (as selected) inhabit
    - `...` represents the column selection (e.g. `2:3`, `attr`, `-attr`, `attr1:attr2`)
    - Aside: `key` and `value` support quasiquotation -- so they could be strings, or not! Life is meaningless. 
  - `spread()` separates one column into multiple columns on a separator.
    - In the tutorial, `separate(res, sex_class, into=c("sex", "class"))` works because the `sep` argument splits on non-alphanumeric values by default (e.g. originally `class_1` and `class_2`)
  - The last two problems covered in this tutorial are 1) multiple observational units in the same table, and 2) a single observational unit stored in multiple tables.
    - For 1), we simply use `select` to make multiple tables. We may use `unique()` call when applicable.
    - For 2), we used mutate per table to add a specific column (same name in both tables, but different constant value). Then use `bind_rows()` to bind any number of data frames by row, making a longer result (useful to just read its docs)
  - **Summary** (from online)
    - `gather()` makes “wide” data longer
    - `spread()` makes “long” data wider
    - `separate()` splits a single column into multiple columns
    - `unite()` combines multiple columns into a single column
- [x] 4: Dates and Times with `lubridate`
  - Fortunately, lubridate offers a variety of functions for **parsing date-times**. These functions take the form of `ymd()`, `dmy()`, `hms()`, `ymd_hms()`, etc., where each letter in the name of the function stands for the location of years (`y`), months (`m`), days (`d`), hours (`h`), minutes (`m`), and/or seconds (`s`) in the date-time being read in.
    - Which function do you use? --> What format is the original string in, in order?
    - It's pretty dynamic! See `dmy(25081985)`
    - E.g.: `ymd_hms("2014-08-23 17:23:02")`
  - `update()` to update one or more components of a date-time
    - `update(this_moment, hours = 8, minutes = 34, seconds = 55)` does not actually alter `this_moment` unless assigned.
    - For a complete list of valid time zones for use with lubridate, check out the following Wikipedia page: [http://en.wikipedia.org/wiki/List_of_tz_database_time_zones](http://en.wikipedia.org/wiki/List_of_tz_database_time_zones)
  - Logical arithmetic operations. To add two days, use `my_date + days(2)`
  - `with_tz()` to change the time zone view. The function returns a date-time as it would appear in a different time zone.
    - `with_tz(tz)` where `tz = "America/New_York", "Asia/Hong_Kong", ...` etc. See the Wikipedia link!
  - `interval(start, end, tzone = tz(start))`: creates an `Interval` object with the specified start and end dates.
    - `as.period(Interval)` to express the time period between start and end. 
  - In general, complexities with time periods arise due to leap years, leap seconds, daylight savings, etc. Hence, in `lubridate`, we have four classes of time-related objects: `instants`, `intervals`, `durations`, and `periods`
    - you can find a complete discussion in the 2011 Journal of Statistical Software paper titled 'Dates and Times Made Easy with lubridate'

## 3) Exploratory Data Analysis

- **Start**: N/A
- **Command**: 
  ```R 
  install_course("Exploratory Data Analysis")
  ```

### Notes
- N/A


## 4) Statistical Inference

- **Start**: N/A
- **Command**: 
  ```R 
  install_course("Statistical Inference")
  ```

### Notes
- N/A


## 5) Regression Models

- **Start**: N/A
- **Command**: 
  ```R 
  install_course("Regression Models")
  ```

### Notes
- N/A
