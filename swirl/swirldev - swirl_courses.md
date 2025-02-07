# `swirldev/swirl_courses`
* URL: https://github.com/swirldev/swirl_courses

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
- [ ] 3: Sequences of Numbers
- [ ] 4: Vectors
- [ ] 5: Missing Values
- [ ] 6: Subsetting Vectors
- [ ] 7: Matrices and Data Frames
- [ ] 8: Logic
- [ ] 9: Functions
- [ ] 10: `lapply` and `sapply`
- [ ] 11: `vapply` and `tapply`
- [ ] 12: Looking at Data
- [ ] 13: Simulation
- [ ] 14: Dates and Times
- [ ] 15: Base Graphics