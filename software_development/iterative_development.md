# Iterative Development
## Overview
If you are asked to write a *very* simple program, perhaps a few lines long, there is a chance that you will be able to formulate a plan in your head and then write correct code on the first try. For nontrivial programs, this is, in practice, *impossible*. It is unreasonable to imagine that you will perfectly understand the problem specification and make no syntax or logic errors. Beyond that, the process of developing software inevitably reveals unforeseen complications.

The accepted solution to this conundrum (across many fields of design, not just software development) is the process of *iterative development*.

Start by writing down a list of tasks that you will need to accomplish to solve the problem. Don't worry about making this list perfect; you'll be able to change it later.

Now write a ridiculously simple program and get it to work. Even getting the classic "Hello, world!" program to run can help you resolve issues with installing and using your editor, compiler, debugger, libraries, and other tools.

Once you have something running, make a series of passes (iterations) through the following steps:

1. Plan out what improvement you want to make next. You may find an appropriate task on your list, or you may find that one of those tasks must be divided into smaller tasks. Aim for the smallest possible improvement that you could make that would take you from your currently running program to a slightly better running program.
1. Make the change. Avoid the dangerous temptation to change more than one thing. If you see other things that could be improved, add them to your task list for future iterations.
1. Evaluate your change. Did it work? How do you know? If this improvement is complete, make any needed changes to the task list and go back to step 1. Otherwise, go back to step 2 to correct or finish this change.

Maintaining the task list on paper (or electronically) and performing many short iterations reduces the number of things you need to keep in your head. This in turn makes your work faster, more accurate, and less stressful.

## Resource
- [John Green on iterative development of novels](https://www.youtube.com/watch?v=PCTO91aBFXk)

## Questions
1. :star: What is the first step in iterative development?
1. :star: Can the task list be changed after the first iteration?
1. :star: Is it better to have many short iterations or a few long ones?
1. :star::star: You are about to end a four-hour programming session. In which step of an iteration would you *not* like to be?

## Answers
1. Write down a task list.
1. Yes; indeed, it is expected.
1. Many short iterations.
1. Step 2 (making a change). Stopping here would be like a surgeon leaving the operating room with the patient open on the table. Performing many short iterations will give you the freedom to stop at an appropriate point when you need to attend another meeting, eat, sleep, etc.
