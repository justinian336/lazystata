Using Git For Versioning (for the adventurous)
================================================

When you work with other people, or in projects that take a very long time, you'll find yourself creating several versions of your code.
This is a tricky thing to do, and can create a large number of files and all sorts of confusions.


Versioning systems in the wild
-------------------------------

Here are some ways people use to version their Stata code, along with their flaws:

#. Create an edited copy of the do file and store it on the same directory.

Usually these files are called something along the lines of `analysis1.do`, followed by `analysis2.do` and so on, until it reaches `analysis FINAL ver3 Feb.do`.
Some researchers will even add a comment at the beginning of each file containing the name of the author and the date of edition.

Ok, that's not really a versioning system.

First, it's wasteful because you're just duplicating content with some changes.

Second, it's risky. Nothing prevents you from mistakenly overwriting your changes on the same old file.

Finally, what's the point of adding the name of the author and the date of edition as a comment on the code? Isn't this information already available in the properties of the file? Besides that, nothing forces you to update it every time you update a file.

#. Adding the date of edition to the name of the file.

Again, you run the risk of overwriting your changes into the wrong file.

#. Creating separate directories

Usually the directories are named after the date of edition, the stage of the revision process by the journal, etc.

This is a better system, because it makes it more difficult to overwrite your changes into the wrong file. It's also easier to maintain, because the directory where the file is stored doesn't depend on your imperfect memory every time you edit the file.

For simple projects, this method is encouraged for versioning simple, individual projects.

However, it suffers some important flaws when it comes to more complicated projects:

- It's still wasteful because you're storing many times the same code, instead of just the changes introduced on each version.
- You can still introduce changes into older versions by mistake.
- There's no easy way of comparing two versions of a Do file and of knowing exactly who introduced a given change.
- In collaborative research, all researchers have to share the same directory structure and the same versioning system. Besides that, it gets complicated when many people need to introduce changes into the same version of the same file.
