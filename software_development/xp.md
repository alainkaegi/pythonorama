# Extreme Programming
## Overview
Extreme Programming (XP) is a process for software development. Like other agile methods, it focuses on tight feedback loops, both between the developers and the code and between the developers and the customer. This is intended to keep everyone's expectations accurate and avoid unpleasant surprises.

XP emphasizes certain values and practices.

### Values
* Communication
* Simplicity
* Feedback
* Respect
* Courage

### Practices
* Testing first
* [Pair programming](pair_programming.md)
* Sustainable pace
* Simple design
* Refactoring
* Small releases
* Continuous integration
* Collective code ownership
* Coding standards
* Customer involvement
* The planning game

## Development Process
### Initial Setup
A couple of things have to happen before the customer and the developers have their first meeting.

#### User Stories
The customer has to write a first draft of a set of *user stories*. (I currently maintain these as [GitHub Issues](https://docs.github.com/en/issues).) Each story describes some desired capability of the software. For example:

| Duck Detonation |
|-|
|When the user clicks on the Detonate button, the duck explodes.|

Stories should be relatively small and testable *by the customer*. They should avoid any technical details about *how* a feature will be implemented.

Stories will be modified, added, and discarded as the project proceeds. Nothing is etched in stone.

#### Setting Up a GitHub Repository
**One developer** should [create a new GitHub repository](setting_up_github.md). The others should then clone it to their local machines. They may need to do some setup (like marking directories as source roots or creating a Python virtual environment) because this developer-specific information is not stored in the repository.

### Iteration
Development proceeds in a series of iterations (known in some other agile methods as sprints). For the main Software Development project, each iteration lasts two weeks.

Each iteration consists of four stages:
1. Customer meeting
1. Planning
1. Coding
1. Delivery

#### Customer Meeting
During the customer meeting, we play the "planning game". Here the developers determine the *cost* of stories and the customer determines the *value* of stories. Specifically:
1. The customer writes stories. They may modify, add, or discard old stories. The developers and the customer should discuss these stories to make sure that everyone understands what is needed. The customer also indicates, very roughly, which stories should be tackled first. These stories are entered at the bottom of the `Backlog` column in the GitHub Project board.
1. The developers estimate how long each story (or at least those stories in the "tackle next" category) will take. Each story is given a rating from 1 to 3 units of difficulty. As a rough approximation, 1 means that a pair of developers could complete the story in under an hour, 3 means that it would take the entire iteration, and 2 is somewhere in between. If a story seems so difficult that it cannot be accomplished in one iteration, it should be broken down into smaller stories. Note that the estimate should be for completing that story *independent of any other stories*; the developers don't yet know in what order stories will be tackled. Modify the title of each story in Trello to show its estimated difficulty, e.g., "Duck Detonation (2)". Existing stories may be re-estimated if the developers feel that work done so far, or new information, justifies doing so.
1. The customer is given a budget to choose stories. For the first iteration, this will be 3 units times the number of developer pairs; for later iterations, it will be based on the average number of units the team has completed in each previous iteration. Given this budget, the customer chooses which stories they want the developers to work on first. This is indicated by moving the stories to the `This Iteration` column.

#### Planning
The developers now meet to do a small amount of planning.
1. Come up with a simple overall design. This is just about the high-level organization of the system; it shouldn't get into details like what data structures are used inside particular classes. This is also a good time to divide each story into tasks (which can be noted by setting up a checklist within the story's Issue).
1. Decide who will pair with whom. (If the team has an odd number of developers, one "pair" will have three people.) The pairs should change each iteration. This serves to propagate knowledge (about programming, our tools, and our system) around the group. It also prevents creating indispensable developers who are the only ones able to work with some part of the system; the project may grind to a halt if such a person calls in sick or is hit by a meteor.
1. Each pair now chooses *one* story, assigns that Issue to themselves, moves it to the `In Progress` column, and starts work on it. If a story involves detailed knowledge (e.g., of some API or part of our system) that some developers gained in a previous iteration, it is best handled by a pair that consists of one knowledgeable person and one new person.

#### Coding
Since we have received extensive training in this highly technical job, many students imagine that coding is the only "real" work and that the other parts of the process are meaningless bureaucratic hoops to jump through. Experienced developers know that planning, communication, coordination, and documentation are just as important. Cranking out a page of code by the seat of one's pants might suffice in an early computer science class, but in a large project with many developers this approach quickly leads to disaster.

There are a number of technical steps for working with git here. A step-by-step process is provided in [a separate document](xp_coding_steps.md).

#### Delivery
When time for the iteration runs out, it is time to deliver. Resist the temptation to squeeze in one more feature that is "almost done". The last hour of each iteration is reserved for this stage.

A working version of the system is presumably in the GitHub repository on the `main` branch. It need only be checked out and put into a format the customer can use (e.g., a standalone executable) along with any necessary instructions and delivered.

The customer now plays with the system. On the project board, each story in the `Merged` column should either be moved to the `Approved` column or back to the `Backlog` column; in the latter case, the customer should include comments in the card explaining why it was rejected. This also gives the customer the opportunity to discover bugs that the developers missed and think about what's important for the next iteration. Crucially, the customer agrees or disagrees with any claims the developers have made about completing stories.

## Resources
- [Extreme Programming: A gentle introduction](http://www.extremeprogramming.org/)
- [The Agile Manifesto](https://agilemanifesto.org/)
- [Extreme Programming: Values, Principles, and Practices](https://www.altexsoft.com/blog/business/extreme-programming-values-principles-and-practices/)
- [GitHub guides](https://guides.github.com/)
- [GitHub Issues Can be Agile if You Do it Right](https://zube.io/blog/agile-project-management-workflow-for-github-issues/)
- Christensen, *Flexible, Reliable Software Using Patterns and Agile Development*, Chapter 1
- Steinberg and Palmer, *Extreme Software Engineering: A Hands-On Approach*

## Questions

## Answers
