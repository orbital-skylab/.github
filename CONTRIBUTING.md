# Contributing to Skylab V2

Thank you to all who wish to contribute to the development of Skylab V2 :smiley:

## For New Contributors

Do read our [Getting Started](https://github.com/orbital-skylab#getting-started) guide to set up your development environment and get familiar with our coding conventions as well as Git and issue tracking workflows. 
You can also contact our developers to be added to our Jira project.

## Picking Up and Creating Tickets

Our [Jira kanban board](https://orbital-skylab.atlassian.net/jira/software/c/projects/OS/boards/1) tracks all open issues in the form of tickets.

You can look through the tickets in the `Backlog` column to see if there are any tickets you would be able to work on.
To pick it up, simply click on the ticket and assign it to yourself, then move the ticket into the `In Progress` column.

If you managed to find an untracked bug or there is a new feature that you would like to work on, you can create a ticket for this new task.

Categorize this newly created ticket under the most appropriate `Epic`. If there is no fitting `Epic` currently in the project, feel free to add a new one.

Do remember to provide the necessary details about the task in the description section of the ticket. 

## Writing Code

Begin by creating a new branch as specified in our [Git Workflow](https://github.com/orbital-skylab/skylab-frontend/wiki/Git-Workflow).

During the process of writing your code to implement a new feature or bugfix, ensure to commit frequently using the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) framework as specified in our Git Workflow.

Do also ensure to abide by our coding conventions and best practices as specified in our [Style Guide](https://github.com/orbital-skylab/skylab-frontend/wiki/Style-Guide)

## Testing Code

Make use of **Jest** to write unit tests for any new helper function(s) that you have defined and **Cypress** to automate end-to-end testing for any new feature(s) that you have implemented. You can find more information in our [Systems Testing](https://github.com/orbital-skylab/skylab-frontend/wiki/System-Testing) documentation.

Do not expect others to test your code for you! While reviewers will be testing your code before approving the changes, the onus is on you to ensure that your code is working as intended before making a pull request. Having test cases prepared will also help with validating that your code continues to work throughout future changes to the codebase.

## Creating a Pull Request

Once you have completed writing and testing your code, you can create a pull request and request a review from another contributor for your branch to be merged.

In the description of the pull request, it would be very helpful to reviewers if you are able to detail the key changes that you are introducing(point form will do) and also provide screenshots or screen recordings of the changes that you have implemented(if applicable).

Reviewers will assess your code using our [Code Review Rubrics](https://github.com/orbital-skylab/skylab-frontend/wiki/Code-Review-Rubrics), so do give this a read to ensure that your commits fulfil all the highlighted criteria
Reviewers may comment and/or request changes before approving your pull request. Feel free to reach out to reviewers to seek further clarification if necessary, and work with them to resolve all requested changes.

Once your pull request is approved, it will be merged by the reviewer.


