java c
Assignment 2
EMATM0061: Statistical Computing and Empirical Methods, TB1, 2024
Introduction
Create an R Markdown for assignment
First, it is recommended that you create a single R Markdown document to include   your solutions, with headings created by heading codes such as “## 1.1 (Q1)”, “## 3 (Q1)”, etc.
It is a good practice to use R Markdown to organise your code and results. You can start with the template called Assignment02_TEMPLATE.Rmd which can be downloaded via Blackboard.
In Section 1, you will need to use R programming to complete the tasks. In section 2 and 3, it is not required to write R code.
You can optionally hand in this assignment by 13:00 Tuesday 1 October. This will   help us understand your work but will not count towards your final grade. If you    want to hand in the assignment, please submit a PDF file containing your answers  (click on the “Assignment 02” under the assignment tab at Blackboards to upload the file). There is no requirement on how the PDF file is generated. One example is to choose the output of R-markdown as PDF (which may require LaTex to be installed in your computer). Another example is to choose a html output at R-markdown and convert the html file into a PDF file. If you have multiple PDF files, please combine them into a single PDF file before the submission.
Load packages
Then we need to load two packages, namely Stat2Data and tidyverse, before
answering the questions. If they haven’t been installed in your computer, please use install.packages() to install them first.
1.      Load the tidyverse package:
library(tidyverse)
2.      Load the Stat2Data package and then the dataset Hawks:
library(Stat2Data)
data("Hawks")
1. Data Wrangling
This part is mainly about data wrangling. Basic concepts of data wrangling can be found in lecture 4.
1.1 Select and filter
(Q1). Use acombination of the select() and filter() functions to generate a data
frame. called “hSF” which is a sub-table of the original Hawks data frame, such that
1.     Your data frame. should include the columns:
a)     “Wing”
b)     “Weight”
c)     “Tail”
2.     Your data frame. should contain a row for every hawk such that:
a)     They belong to the species of Red-Tailed hawks
b)     They have weight at least 1kg.
3.     Use the pipe operator “%>%” to simplify your code. The data frame. should look like this:
## Wing Weight Tail
## 1 412 1090 230
## 2 412 1210 210
## 3 405 1120 238
## 4 393 1010 222
## 5 371 1010 217
(Q2) How many variables does the data frame. hSF have? What would you say to communicate this information to a Machine Learning practitioner?
How many examples does the data frame. hSF have? How many observations? How many cases?
1.2 The arrange function
(Q1) Use the arrange() function to sort the hSF data frame. created in the previous section so that the rows appear in order of increasing wingspan.
Then use the head command to printout the top five rows of your sorted data frame. Your results should look something like this:
## Wing Weight Tail
## 1 37.2 1180 210
## 2 111.0 1340 226
## 3 199.0 1290 222
## 4 241.0 1320 235
## 5 262.0 1020 200
1.3 Join and rename functions
The species of Hawks within the data frame. “Hawks” have been indicated via a two- letter code (e.g., RT, CH, SS). The correspondence between these codes and the full names is given by the following data frame.
##   species_code species_name_full
## 1           CH          Cooper's
## 2           RT        Red-tailed
## 3           SS     Sharp-shinned
(Q1). Use data.frame() to create a data frame. that is called
hawkSpeciesNameCodes and is the same as the above data frame. (i.e., containing the correspondence between codes and the full species names).
(Q2). Use a combination of the functions left_join(), therename() and the select() functions to create a new data frame. called “hawksFullName” which is the same as   the “Hawks” data frame. except that the Species column contains the full names rather than the two-letter codes.
(Q3). Use acombination of the head() and select() functions to printout the top seven rows of the columns “Species”, “Wing” and “Weight” of the data frame. called “hawksFullName”. Do this without modifying the data frame. you just created. Your result should something like this:
##
Species
WingWeight
## 1
Red-tailed
385920
## 2
Red-tailed
376930
## 3
Red-tailed
381990
## 4
Cooper's
265470
## 5
Sharp-shinned
205170
## 6
Red-tailed
4121090
## 7
Red-tailed
370960
Does it matter what type of join function you use here? In what situations would it make a difference?
1.4 The mutate function
Suppose that the fictitious “Healthy Hawks Society”has proposed a new measure called the “bird BMI” which attempts to measure the mass of a hawk standardized by their wingspan. The “bird BMI” is equal to the weight of the hawk (in grams) divided by their wingspan (in millimeters) squared. That is,
Bird-BMI : = 1000 × Weight/Wing-pan2 .
(Q1). Use the mutate(), select() and arrange() functions to create a new data frame. called “hawksWithBMI” which has the same number of rows as the original Hawks data frame. but only two columns - one with their Species and one with their   “bird BMI”. Also, arrange the rows in descending order of “bird BMI”. The top 8 rows of your data frame. should look something like this:
## Species bird_BMI
## 1 RT 852.69973
## 2 RT 108.75741
## 3 RT 32.57493
## 4 RT 22.72688
## 5 CH 22.40818
## 6 RT 19.54932
## 7 CH 15.21998
## 8 RT 14.85927


1.5 Summarize and group-by functions
Using the data frame. “hawksFullName”, from Section 1.3 above, to do the following tasks:
(Q1). In combination with the summarize() and the group_by functions, create a summary table, broken down by Hawk species, which contains the following summary quantities:
1.     The number of rows (num_rows);
2.     The average wingspan in centimeters (mn_wing)代 写EMATM0061: Statistical Computing and Empirical Methods, TB1, 2024 Assignment 2R
代做程序编程语言;
3.     The median wingspan in centimeters (nd_wing);
4.     The trimmed average wingspan in centimeters with trim=0.1, i.e., the mean of the numbers after the 10% largest and the 10% smallest values being
removed (t_mn_wing);
5.     The biggest ratio between wingspan and tail length (b_wt_ratio).Hint: type?summarize to see a list of useful functions (mean, sum, etc) that can be used to compute the summary quantities. Your final result should look something  like this:## # A tibble: 3 × 6##   Species       num_rows mn_wing md_wing t_mn_wing b_wt_ratio##                                ## 1 Cooper's            70    244.     240      243.       1.67## 2 Red-tailed         577    383.     384      385.       3.16## 3 Sharp-shinned      261    185.     191      184.       1.67
(Q2). Next create a summary table of the following form. Your summary table will    show the number of missing values, broken down by species, for the columns Wing, Weight, Culmen, Hallux, Tail, StandardTail, Tarsus, and Crop. You can complete this task by combining the select(), group_by(), summarize(), across(), everything(), sum() and is.na() functions. You should end with a summary table of the following  form.:
## # A tibble: 3 × 9
##   Species        Wing Weight Culmen Hallux  Tail StandardTail Tarsus
Crop
##                             
## 1 Cooper's          1      0      0      0     0           19     62
21
## 2 Red-tailed        0      5      4      3     0          250    538
254
## 3 Sharp-shinned     0      5      3      3     0           68    233
68


2. Random experiments, events and sample spaces, and the set theory
In this exercise, we will learn about random experiments, events and sample spaces and set theory that were introduced in Lecture 5.
In this section, you are not required to compute your results using R codes. If you want to write math formulas in R-markdown, the document called “Assignment_R    MarkdownMathformulasandSymbolsExamples.rmd” (available under the “resource list” tab at Blackboard course webpage) provides a list of examples for your reference.
2.1 Random experiments, events and sample spaces(Q1) Firstly, write down the definition of a random experiment, event and sample space. This question aims to help you recall the basic concepts before completing   the subsequent tasks.
(Q2) Consider a random experiment of rolling a dice twice. Give an example of what  is an event in this random experiment. Also, can you write down the sample space as a set? What is the total number of different events in this experiment? Is the empty    set considered as an event?
2.2 Set theory
Remember that a set is just a collection of objects. All that matters for the identity of a set is the objects it contains. In particular, the elements within the set are unordered, so for example the set {1, 2, 3} is exactly the same as the set {3, 2, 1}. In addition, since sets are just collections of objects, each object can only be either included or excluded and multiplicities do not change the nature of the set. In particular, the set {1, 2, 2, 2, 3, 3} is exactly the same as the set A = {1, 2, 3}. In   general there is no concept of “position” within a set, unlike a vector or matrix.
(Q1) Set operations:
Let the sets A, B, C be defined by A := {1, 2, 3}, B := {2, 4, 6}, C := {4, 5, 6}.
1.     What are the unions A ∪ B and A ∪ C?
2.     What are the intersections A ∩ B and A ∩ C?
3.     What are the complements A ∖ B and A ∖ C?
4.     AreA and B disjoint? AreA and C disjoint?
5.     Are B and A ∖ B disjoint?
6.     Write down an arbitrary partition of {1,2,3,4,5,6} consisting of two sets. Also, write down another partition of {1,2,3,4,5,6} consisting of three sets.
(Q2) Complements, subsets and De Morgan’s laws
Let Ω be a sample space. Recall that for an event A  ⊆ Ω the complement Ac  : = Ω ∖ A : = {w  ∈ Ω:w ∉ A}. Take a pair of events A  ⊆ Ω and B  ⊆ Ω .
1.      Can you give an expression for (Ac )c  without using the notion of a complement?
2.     What is Ωc?
3.      (Subsets) Show that if A ⊆ B, then Bc   ⊆ Ac.
4.      (De Morgan’s laws) Show that (A ∩ B)c   = Ac  ∪ Bc. Let’s suppose we have a sequence of events A1, A2, ⋯ , Ak   ⊆ Ω . Can you write out an expression for (∩k(k)= 1 Ak )c?
5.      (De Morgan’s laws) Show that (A ∪ B)c   = Ac  ∩ Bc.
6.     Let’s suppose we have a sequence of events A1, A2, ⋯ , Ak   ⊆ Ω . Can you write out an expression for (∪k(k)= 1 Ak )c?
(Q3) Cardinality and the set of all subsets:
Suppose that Ω = {w1, w2, ⋯ , wk } contains K elements for some natural number K. Here Ω has cardinality K.
Let E be aset of all subsets of Ω, i.e., E : = {A|A ⊂ Ω}. Note that here E is a set. Give a formula for the cardinality of E in terms of K.
(Q4) Disjointness and partitions.
Suppose we have a sample space Ω, and events A1, A2, A3, A4  are subsets of Ω .
1.      Can you think of a set which is disjoint from every other set? That is, find a set A ⊆ Ω such that A ∩ B  = ∅ for all B ⊆ Ω .
2.      Define events S1  : = A1, S2   = A2  ∖ A1, S3   = A3  ∖ (A1  ∪ A2), S4   = A4  ∖
(A1  ∪ A2 ∪ A3). Show that S1, S2, S3, S4  form. a partition of A1  ∪ A2  ∪ A3  ∪ A4 . (Q5) Indicator function.
Suppose we have a sample space Ω, and the event A is a subset of Ω. Let 1A  be the indicator function of A.
1.     Write down the indicator function 1Acof Ac  (use 1A in your formula).
2.      Can you find a set B whose indicator function is 1Ac   + 1A?
3.      Recall that 1A∩B   = 1A  ⋅ 1B  and 1A∪B   = max(1A, 1B ) = 1A  + 1B  − 1A  ⋅ 1B  forany A ⊆ Ω and B ⊆ Ω . Combining this with the conclusion from Question  (Q5) 1, use indicator functions to prove (A ∩ B)c   = Ac  ∪ Bc  (De Morgan’s laws).
(Q6) Uncountable infinities (this is an optional extra).
This is a challenging optional extra. You may want to return to this question once you have completed all other questions.
Show that the set of numbers Ω : = [0, 1] is uncountably infinite.





         
加QQ：99515681  WX：codinghelp
