# 1-1-The-R-Programming-Environment
Mastering Software Development in R • Johns Hopkins University

## Welcome
### Swirl Assignments
* install swirl
install.packages("swirl")  
check version  
packageVersion("swirl")  
* load swirl
library(swirl)
* install the R Programming Environment course
install-course("The R Programming Environment")
* Start swirl and complete the lessons
swirl()

## Crash Course on R Syntax
### Lesson Introduction
x <- 1  
print(x)  
[1] 1  
x  
[1] 1  
msg <- "hello"  
"#" indicates a comment  

### Evaluation
x <- 5  ## nothing printed  
x       ## auto-printing occurs  
[1] 5  
print(x)  ## explicit printing  
[1] 5  
x <- 11:30  
x  
 [1] 11 12 13 14 15 16 17 18 19 20 21 22  
[13] 23 24 25 26 27 28 29 30  

### Objects
R has five basic or “atomic” classes of objects:  
character  
numeric (real numbers)  
integer  
complex  
logical (True/False)  
A vector can only contain objects of the same class.  

### Numbers
Numbers in R are generally treated as numeric objects (i.e. double precision real numbers).   
integer: L e.g. 1L  
infinity: Inf e.g. 1/Inf is 0  
undefined value (“not a number”): NaN e.g. 0/0  

### Creating Vectors
x <- c(0.5, 0.6)       ## numeric  
x <- c(TRUE, FALSE)    ## logical  
x <- c(T, F)           ## logical  
x <- c("a", "b", "c")  ## character  
x <- 9:29              ## integer  
x <- c(1+0i, 2+4i)     ## complex  
x <- vector("numeric", length = 10)   
x  
 [1] 0 0 0 0 0 0 0 0 0 0  
 
### Mixing Objects
y <- c(1.7, "a")   ## character  
y <- c(TRUE, 2)    ## numeric  
y <- c("a", TRUE)  ## character  

### Explicit Coercion
x <- 0:6  
class(x)  
[1] "integer"  
as.numeric(x)  
[1] 0 1 2 3 4 5 6  
as.logical(x)  
[1] FALSE  TRUE  TRUE  TRUE  TRUE  TRUE  TRUE  
as.character(x)  
[1] "0" "1" "2" "3" "4" "5" "6"  

x <- c("a", "b", "c")  
as.numeric(x)  
Warning: NAs introduced by coercion  
[1] NA NA NA  
as.logical(x)  
[1] NA NA NA  
as.complex(x)  
Warning: NAs introduced by coercion  
[1] NA NA NA  

### Matrices
m <- matrix(nrow = 2, ncol = 3)  
m  
     [,1] [,2] [,3]  
[1,]   NA   NA   NA  
[2,]   NA   NA   NA  
dim(m)  
[1] 2 3  
attributes(m)  
$dim  
[1] 2 3  
  
m <- matrix(1:6, nrow = 2, ncol = 3)   
m  
     [,1] [,2] [,3]  
[1,]    1    3    5  
[2,]    2    4    6  
  
m <- 1:10   
m  
 [1]  1  2  3  4  5  6  7  8  9  10  
dim(m) <- c(2, 5)  
m  
     [,1] [,2] [,3] [,4] [,5]  
[1,]    1    3    5    7    9  
[2,]    2    4    6    8   10  
   
x <- 1:3  
y <- 10:12  
cbind(x, y)  
     x  y  
[1,] 1 10  
[2,] 2 11  
[3,] 3 12  
rbind(x, y)   
  [,1] [,2] [,3]  
x    1    2    3  
y   10   11   12  

### Lists
x <- list(1, "a", TRUE, 1 + 4i)  
x  
[[1]]  
[1] 1  

[[2]]  
[1] "a"  

[[3]]  
[1] TRUE  

[[4]]  
[1] 1+4i  

x <- vector("list", length = 5)  
x  
[[1]]  
NULL  

[[2]]  
NULL  

[[3]]  
NULL  

[[4]]  
NULL  

[[5]]  
NULL  

### Factors
x <- factor(c("yes", "yes", "no", "yes", "no"))  
x  
[1] yes yes no  yes no  
Levels: no yes  
table(x)  
x  
 no yes   
  2   3  
"## See the underlying representation of factor"  
unclass(x)  
[1] 2 2 1 2 1  
attr(,"levels")  
[1] "no"  "yes"  
  
x <- factor(c("yes", "yes", "no", "yes", "no"))  
x  ## Levels are put in alphabetical order  
[1] yes yes no  yes no  
Levels: no yes  
x <- factor(c("yes", "yes", "no", "yes", "no"),  
            levels = c("yes", "no"))  
x  
[1] yes yes no  yes no  
Levels: yes no  

### Missing Values
"## Create a vector with NAs in it"  
x <- c(1, 2, NA, 10, 3)  
"## Return a logical vector indicating which elements are NA"  
is.na(x)   
[1] FALSE FALSE  TRUE FALSE FALSE  
"## Return a logical vector indicating which elements are NaN"  
is.nan(x)   
[1] FALSE FALSE FALSE FALSE FALSE  
"## Now create a vector with both NA and NaN values"  
x <- c(1, 2, NaN, NA, 4)  
is.na(x)  
[1] FALSE FALSE  TRUE  TRUE FALSE  
is.nan(x)  
[1] FALSE FALSE  TRUE FALSE FALSE  

### Data Frame
x <- data.frame(foo = 1:4, bar = c(T, T, F, F))  
x  
  foo   bar  
1   1  TRUE  
2   2  TRUE  
3   3 FALSE  
4   4 FALSE  
nrow(x)  
[1] 4  
ncol(x)  
[1] 2  
Data frames are usually created by reading in a dataset using the read.table() or read.csv().  
Data frames can be converted to a matrix by calling data.matrix().  

### Names
x <- 1:3  
names(x)  
NULL  
names(x) <- c("New York", "Seattle", "Los Angeles")  
x  
   New York     Seattle Los Angeles  
          1           2           3  
names(x)  
[1] "New York"    "Seattle"     "Los Angeles"  

x <- list("Los Angeles" = 1, Boston = 2, London = 3)  
x  
$`Los Angeles` 
[1] 1    
$Boston  
[1] 2  
$London  
[1] 3  
names(x)  
[1] "Los Angeles" "Boston" "London"     

m <- matrix(1:4, nrow = 2, ncol = 2)  
dimnames(m) <- list(c("a", "b"), c("c", "d"))   
m  
  c d  
a 1 3  
b 2 4  

colnames(m) <- c("h", "f")  
rownames(m) <- c("x", "z")  
m  
  h f  
x 1 3  
z 2 4  

Object;     	  Set column names;     	Set row names  
data frames;  	names();	              row.names()  
matrix;     	  colnames();	           rownames()  

### Attributes
Some examples of R object attributes are:  
names, dimnames  
dimensions (e.g. matrices, arrays)  
class (e.g. integer, numeric)  
length  
other user-defined attributes/metadata  

### Summary
* atomic classes: numeric, logical, character, integer, complex
* vectors, lists
* factors
* missing values
* data frames and matrices
