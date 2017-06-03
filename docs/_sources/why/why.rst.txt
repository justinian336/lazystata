Introduction
=====================


You know I don't lie when I say that spaguetti code can get you in serious trouble. You have been there.

* Remember that time when a journal asked you for revisions, but you had to spend some good time trying to understand your code from six months ago?


* What about that time when you had to work with that other professor, but understanding his code took you more than you'd like to admit?


* Let's not forget that day when you tried to check an earlier version of your code, but you couldn't find it because you overwrote it.


Trying to understand complicated code is not why you entered the PhD program, or became a professor.

You're too busy advising government officials and making great discoveries! And don't forget about your personal life!

In the world of Software Engineering, it is widely known that code gets read more than it gets written, and therefore it has to be clean.

However, most Stata users don't come from such background, and schools often don't give importance to teaching how to write good code when teaching Stata.

Bad code steals your time, makes you angry and frustrates you, and that's bad. This style guide gives you some tips that will make your life as a researcher easier.


What's In This Guide?
----------------------

- Suggestions to make your code more readable and easy to manipulate.

- An example project that shows how to structure your code and your data in a way that's easy to maintain and to understand.


What's NOT In This Guide?
--------------------------

- A Stata tutorial for beginners. This guide won't introduce basic concepts, it will only show how to use them in efficient ways.

- A guide on creating macros. This might be included in the future; for now, this guide concentrates on design patterns for using existing packages.


Who Is It For?
---------------

This guide is aimed at researchers who have already some experience with Stata. 

If you're a graduate student working on your disertation, this guide will give you some tips on managing the code for your papers. Some patterns in this guide might make your life easy when replying to journals.

Professors and researchers can also find valuable design patters to help them process their data more efficiently. Especially if you're working on a team, you might learn one trick or two to make it easy to collaborate with your partners.

If you're a beginner and still need to learn the basics of Stata, you can still read this guide in order to learn some general tips on programming and structuring your project. However, some examples might feel difficult to follow.

Experienced Stata who are used to writing readable, easy to maintain code might find that the advice in this guide is not of great help. Indeed, there's not a perfect way of writing code, and the best style might depend on the project and the person. In that case, you can still find interesting tips. For example, no matter how experienced you are, odds are high that you have never used Git for your research. In that case, the chapter on versioning can help you add a new tool to your stack.


Collaborating
--------------

`Lazy Stata` is an open source project, and is open for Pull Requests. If you have suggestions on how to improve the content of this guide, feel free to create an Issue. Front-end developers can also collaborate on improving the layout and making it more interactive.

The guide is compiled with Sphinx and is currently deployed on Github Pages. For instructions on the compilation process, see the README file.
