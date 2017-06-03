The DRY Principle
=================

**DRY** stands for *Don't Repeat Yourself*. It's the principle that says that you should simplyfy your code by eliminating repetitions.


Global Variables
----------------

One important source of repetitions in Stata Do files are directory names. Often, you perform many saving and opening operations over files located under the same directory. 

This can be annoying when doing collaborative research, because directory names are usually not the same for all researchers. What ends up happening, is that each researcher will have to change the directory name to accomodate their file system, which is a waste of time.


You can make it easy for other researchers to follow, by defining the directory name into a global variable::

	global var main_dir = "C:\Users\MyUser\Research\Project\"
	global var parents_data = "parents"
	global var children_data = "children"
	global var family_data = "family_data"

Then, you'd use it across your project as::

	save "$main_dir\$children_data\children_survey.dta", replace

	sort family_ID
	merge family_ID using "$main_dir\$parents_data\parents_survey.dta"
	save "$main_dir\family_data\family.dta"

As you can see, the path in `main_dir` is present three times in this file. Changing the text one by one would be a real trouble. By defining the path through a global variable, this task has been reduced to changing just one line of code!


Loops
---------

Do files often contain blocks that repeat a single logic once and once again. Look at this example::
	
	gen total_primary = rowtotal(boys_primary, girls_primary)
	gen total_secondary = rowtotal(boys_secondary, girls_secondary)
	gen total_university = rowtotal(boys_university, girls_university)

Obviously there's some repetition here, which could easily be refactored into::
	
	foreach i in "primary" "secondary" "university" {
		gen total_`i' = rowtotal(boys_`i', girls_`i')
	}

Much cleaner! Maybe you'll tell me that we haven't achieved much, since we're still using three lines of code. Well, look at the following block::

	gen total_grade_1 = rowtotal(boys_grade_1, girls_grade_1)
	gen total_grade_2 = rowtotal(boys_grade_2, girls_grade_2)
	gen total_grade_3 = rowtotal(boys_grade_3, girls_grade_3)
	gen total_grade_4 = rowtotal(boys_grade_4, girls_grade_4)
	gen total_grade_5 = rowtotal(boys_grade_5, girls_grade_5)
	gen total_grade_6 = rowtotal(boys_grade_1, girls_grade_6)
	gen total_grade_7 = rowtotal(boys_grade_7, girls_grade_7)
	gen total_grade_8 = rowtotal(boys_grade_8, girls_grade_8)
	gen total_grade_9 = rowtotal(boys_grade_9, girls_grade_9)

This is wrong on several levels: 

* First, the person who wrote this most certainly copied the first line nine times, and then changed the numbers. This is error prone! In this case, there's an error on line 6, because the person did not substitute the `boys_grade_1` variable inside the `rowtotal` function. 

* Second, large blocks of repetitive code make it difficult to notice such errors, which is scary. If you submitted your paper to an academic journal, a referee would have noted that the summary statistics for grade 6 don't match. You'd then have to reply that it was a copy-paste error... how awkward is that!?

Believe or not, researchers are humans too, they shouldn't put their attention span to test in blocks like that one. A cleaner solution would be::

	foreach g of numlist 1/9{
		gen total_grade_`g' = rowtotal(boys_grade_`g', girls_grade_`g')
	}

This is a much simpler piece of code that explains itself and is less error-prone. 

If you wanted to make it even more descriptive, you could throw in some **display** statements to help you know where the loop is running, and add a comment line before the loop explaining what it does::

	// Generate total number of students by grade:
	foreach g of numlist 1/9{
		display "Generating total_grade_"`g'
		gen total_grade_`g' = rowtotal(boys_grade_`g', girls_grade_`g')
	}

.. warning:: Don't over-simplify your code to the point where it becomes hard to understand. The purpose here is to make your code readable to other humans, including you in the future. Therefore, readability has the biggest priority.



