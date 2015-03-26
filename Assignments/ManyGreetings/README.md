## Week 1: Many greetings!

### Goals

* learn basic keyboard input and output to screen
* learn basis about variables and assignment
* practice basics of version control (`push`/`pull`, `add`/`commit`, `branch`/`merge`)

### Read

* [Think Python](http://www.greenteapress.com/thinkpython/) ch. 1, 2, 5, 

### Assignment

Write a program that asks your name and prints 'Hello \<your name\> !' on the screen. Its output should look like

	Name ? Tristan
	Hello, Tristan !
	
Commit all the changes and create a new branch called 'extension1'. In this branch, add ask for extra input: 'How many greetings?' and make sure that the greeting is repeated a number of times. Its output should look like

	Name ? Tristan
	How many greetings ? 3
	3 x Hello, Tristan !
	
While working on the extension, try switching back to the master branch. You'll see that you can still run the old version of the code, even if the extension isn't ready yet. You can only switch branches, however, once you've committed the changes!

While still in the master branch, change the first question to read 'What is your name ?'.

	What is your name ? Tristan
	Hello, Tristan !
	
Now try to merge the 'extension' branch back into the master branch. Obviously, there is a conflict between the two branches. Resolve the conflict in such a way that the final program in the master branch should respond as follows

	What is your name ? Tristan
	How many greetings ? 2
	2 x Hello, Tristan !
