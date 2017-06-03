Think of Do Files Like Lego
============================

The data crunching part of research tends to go through the following stages, some of which overlap:

#. **Data cleaning**: reading the raw data (possibly a `csv` file), renaming the variables (hopefuly in a way that's easy to understand), creating lables, etc. This can involve different files from different sources.

#. **Merging the data**: at the end of the day you'll work with only one dataset, containing only the variables you need for analysis.

#. **Transforming the data**: creating the variables to include in your econometric model.

#. **Analyzing**

#. **Storing and formatting results**


Even when each stage is performed with different code, many people tend to put all this into one single Do file. This is a bad idea and a main cause of stress.

Consider this: data cleaning can be the longest, most annoying parts of research. You might have heard this famous quote:

	*"I had to spend one month cleaning the data just to estimate this regression in less than an hour"*

	*Every Economics researcher ever*

By putting your data cleaning code in the same Do file that contains your analysis code, you're guaranteeing that you have to look at it every single time you wanna tune your equations.

If you're lazy, you can simply run the whole file, which will risk overwriting your files in probably unexpected ways. This will also take an unnecessary amount of time.

But even if you take the time to search and select the exact piece of code you need to re-run, isn't that wasteful?

Believe me, large Do files are a big source of stress, avoid them by breaking up your code in parts in a logical way.

Separating Concerns
-------------------

Many Computer Scientists share the view that one piece of code should do just one thing, and do it very well. In Stata, you can follow this principle by dividing your code in many Do files that do one thing in specific. Then, create a *Run this.do* file that calls the other Do files in steps, performing all the necessary operations in order.

See the following example of a Do file::

	set more off

	clear
	global parent_directory "C:\Users\Juan\Documents\Research\Project 1"
	cd "$parent_directory"

	*1) Clean the children household survey data files.
	do "1 Clean children data.do" "$parent_directory\children"
	cd "$parent_directory"
	clear

	*2) Clean the parents household survey data files.
	do "2 Clean parents data.do" "$parent_directory\parents"
	cd "$parent_directory"
	clear

	*3) Clean prefectures data.
	do "3 Clean prefectures data.do" "$parent_directory\prefectures"
	cd "$parent_directory"
	clear

	*4) Merge and create panel.
	do "4 Merge and create panel.do" "$parent_directory\workfiles"
	cd "$parent_directory"
	clear

	*5) Create variables for analysis.
	do "5 Create variables for analysis.do" "$parent_directory"
	cd "$parent_directory"

	*6) Analysis and results.
	do "6 Analysis and results.do" "$parent_directory"
	cd "$parent_directory"

Do you see? `Run this.do` aggregates all the other files in steps. The home directory is passed as an argument and is accessible to every Do file through the local variable **`1'**. Now you don't have to worry about being in the right directory, you'd just have to change one line!

This is a **lego** structure, because it allows you to modify individual parts of your workflow without having to see (or risk making unintended changes to) the other files. You can modify, for example, the file `5 Create variables for analysis.do` and you'd just have to run steps 5 and 6.
