# Learn command line

Please follow and complete the free online [Command Line Crash Course
tutorial](https://web.archive.org/web/20160708171659/http://cli.learncodethehardway.org/book/) or [Codecademy's Learn the Command Line](https://www.codecademy.com/learn/learn-the-command-line). These are helpful tutorials. Each "chapter" focuses on a command. Type the commands you see in the _Do This_ section, and read the _You Learned This_ section. Move on to the next chapter. You should be able to go through these in a couple of hours.

---

### Q1.  Cheat Sheet of Commands  

Here's a list of items with which you should be familiar:  
* show current working directory path
* creating a directory
* deleting a directory
* creating a file using `touch` command
* deleting a file
* renaming a file
* listing hidden files
* copying a file from one directory to another

Make a cheat sheet for yourself: a list of at least **ten** commands and what they do.  (Use the 8 items above and add a couple of your own.)  

> > pwd - show current working directory path
> > mkdir - creating a directory
> > cd - change directory
> > rm -r directory -  deleting a directory
> > touch filename.txt -  creating a file using `touch` command
> > rm filename.txt - deleting a file
> > mv filename.txt newfilename.txt - renaming a file
> > ls -a - listing hidden files
> > cp directory/filename.txt newdirectory/ - copying a file from one directory to another
> > grep "Text" filename.txt - finds text within the file name; pair with -R to read into all within a directory or -i for case insensitivity
> > cat filename.txt - displays lines in a file
> > sed - searches for a text pattern and modifies it

---

### Q2.  List Files in Unix   

What do the following commands do:  
`ls`  
`ls -a`  
`ls -l`  
`ls -lh`  
`ls -lah`  
`ls -t`  
`ls -Glp`  

> > `ls`  - lists contents
> > `ls -a`  - lists all contents
> > `ls -l`  - lists contents in long form
> > `ls -lh`  - lists contents in long human readable format
> > `ls -lah` - lists all contents in long human readable format 
> > `ls -t`  - lists contents by time last modified
> > `ls -Glp` - lists contents in long (no group) list with slashes for all files that are directories

---

### Q3.  More List Files in Unix  

Explore these other [ls options](http://www.techonthenet.com/unix/basic/ls.php) and pick 5 of your favorites:

> > ls -F
> > ls -d
> > ls -R
> > ls -Fa
> > ls -m
---

### Q4.  Xargs   

What does `xargs` do? Give an example of how to use it.

> > xargs repeats the argument/command multiple times, which is useful when you're doing using some arguments like touch and find. 
find . -name "*.txt" | xargs rm -rf
 

