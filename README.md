# WDGPH Developer Guide <!-- omit from toc -->

## Introduction
Welcome to our Developer Guide. This guide serves as a reference for contributors to Wellington-Dufferin-Guelph Public Health's open-source projects. With this guide we seek to support coding and project management practices that create reliable, and high-quality tools that can be developed collaboratively. This guide is not a strict set of rules, but a collection of best practices that we've found to work well for us in our day-to-day coding and project management.

This guide is a living document. The field of software development is always evolving, with new tools and practices continually emerging. As such, **contributions and improvements to this guide are highly welcomed**. If you come across a tool, technique, or practice that you believe could benefit the team, we encourage you to open a pull request to this document to suggest its addition. Your perspective can help us keep this guide accessible, useful, and forward-looking.

- [Introduction](#introduction)
- [Git Version Control](#git-version-control)
  - [Understanding Git and GitHub](#understanding-git-and-github)
  - [Core Concepts](#core-concepts)
  - [Initializing a Repository](#initializing-a-repository)
  - [Staging Changes](#staging-changes)
  - [Committing Changes](#committing-changes)
  - [Working with Branches](#working-with-branches)
  - [Merging and Pull Requests](#merging-and-pull-requests)
  - [Other Git Concepts and GitHub Features](#other-git-concepts-and-github-features)
    - [Stashing](#stashing)
    - [Rebasing](#rebasing)
    - [Squashing Commits](#squashing-commits)
    - [Tagging](#tagging)
    - [Releases](#releases)
    - [Main Branch Protections](#main-branch-protections)
    - [GitHub Actions](#github-actions)
- [Project Documentation](#project-documentation)
  - [Structure](#structure)
  - [Usage Instructions](#usage-instructions)
  - [Welcoming Contributions](#welcoming-contributions)
- [Licenses](#licenses)
- [Privacy](#privacy)
- [Code Readability and Style](#code-readability-and-style)
  - [Comments](#comments)
  - [Style](#style)
  - [Succinctness](#succinctness)
- [Code Functionality](#code-functionality)
  - [Correctness](#correctness)
  - [Robustness](#robustness)
  - [Efficiency](#efficiency)
  - [Testing](#testing)
- [Reproducibility](#reproducibility)
  - [Randomness](#randomness)
  - [Dependencies](#dependencies)
  - [Packaging](#packaging)
  - [Containerization](#containerization)
- [Security](#security)
  - [Code and Git History](#code-and-git-history)
  - [Dependencies](#dependencies-1)
- [Project Maintenance](#project-maintenance)
  - [Regular Updates](#regular-updates)
  - [Bug Fixes](#bug-fixes)
  - [Dependency Management](#dependency-management)
  - [User Feedback](#user-feedback)
  - [Documentation Updates](#documentation-updates)
  - [Refactoring](#refactoring)
  - [End-of-life](#end-of-life)


## Git Version Control
Git is a distributed version control system that provides mechanisms for multiple developers to work on a single project simultaneously without overwriting each other's changes. It maintains a complete history of a project's changes, facilitating the tracking of progress, the investigation of issues, and the potential to revert changes if necessary.

### Understanding Git and GitHub
Git and GitHub are distinct but complementary tools used in code development. Git is a version control system that allows you to track changes, create branches, and more, all from your local development environment. It's a command-line tool that is installed and used on your local machine.

On the other hand, GitHub is a web-based hosting service for Git repositories. It provides a graphical interface to interact with your Git repositories, and adds features such as access control, collaborative features (like pull requests and code reviews), issue tracking, and more. While you can use Git without GitHub, using them together provides a more robust, collaborative version control environment.

In short, Git is the tool, and GitHub is the place where you store your projects and collaborate with others using that tool.

### Core Concepts
- **Repository:** This is a project's home where all files and revision history are stored.

- **Forks:** A fork is a copy of a repository that allows you to experiment freely without affecting the original project. After making modifications in a forked repository, you can propose changes to the original (upstream) repository by creating a pull request.

- **Commit:** A commit is a snapshot of a repository at a given time. Each commit is associated with a unique SHA-1 hash (a string of characters that identifies the specific commit) and a message describing the changes made in that commit.

- **Branches:** Git uses branches to isolate changes for specific features or tasks. The `main` branch is the default branch where the source code reflects a production-ready state. New branches, created off of the `main` branch, can be used to develop new features or to experiment without disturbing the main line of development. Once the feature is ready, it's merged back into the `main` branch.

- **Merging:** Git operation in which changes from one branch are incorporated into another branch. 

- **Pull Request:** Proposal to merge changes from one branch into another on GitHub platform. A pull request (PR) allows for code review and discussion about the proposed changes.

### Initializing a Repository
To start using Git, you first need to initialize a Git repository in your project's directory. This creates a new subdirectory named `.git` that contains all of your necessary repository files — a Git repository skeleton. None of your project files are touched when you initialize the repository, but the directory becomes Git-aware and ready for version tracking.

In the terminal, you would navigate to your project directory and use the `git init` command.

```bash
git init
```

When initializing a new repository, it's common and beneficial to include a few specific files:

- **`README.md`:** This is often the first thing people will see when they access your repository. It should contain information about your project, how to use it, and any other relevant details. For smaller projects, an entire project's documentation might be contained in the README.

- **`LICENSE.md`:** This is crucial for open-source projects. The license dictates how others can use, modify, and distribute your project. 

- **`.gitignore`:** This file tells Git which files or directories to ignore in your project. This is particularly useful for excluding files with sensitive information, logs, or machine-specific configuration files from your commits.


### Staging Changes
In Git, the term "staging" refers to the process of preparing changes in your working directory for a commit. When you make changes to your files, Git recognizes that the files have been modified, but won't include these changes in a commit until you've "staged" them.

Staging changes allows you to selectively add changes to a commit, even if there have been many changes in your working directory. This allows for more granular commits and more precise version control. For example, if you have made changes to three files but only want to commit changes to two of those files, you would stage the changes for those two files and then proceed to commit. The changes to the third file remain in your working directory and can be included in a future commit.

You can stage changes in VS Code by clicking on the '+' symbol next to the file in the Source Control view. Alternatively, in the terminal, you can use the `git add` command followed by the file name to stage changes.

```bash
git add file-name
```

### Committing Changes
Once you've staged changes, you can then commit those changes to your project's history. A commit is like a snapshot of your project at a point in time, which you can refer back to or even revert to if needed.

You can commit staged changes in VS Code by providing a commit message and clicking the check mark in the Source Control view. Alternatively, in the terminal, you can use the `git commit -m` command followed by your commit message in quotes.

```bash
git commit -m "Your descriptive commit message"
```

Commit messages are vital. They provide a log of changes made over time, which helps you and your team understand the history and rationale behind certain changes. A good commit message is clear, concise, and explains the "why" behind the commit. It's also common practice to write commit messages in the present tense.

The size of commits is a matter of preference, but it's generally best to keep commits relatively small and focused on a single task or feature. Large commits with many changes across many files can be difficult to understand and troubleshoot if issues arise. By keeping commits small and specific, it's easier to identify and manage changes across the project.

Committing changes regularly and with good commit messages is a hallmark of effective version control and team collaboration.

### Working with Branches
Branches in Git separate different lines of development. You might create a new branch for adding a feature, fixing a bug, or even experimenting, while the main branch of your project (often called "main") remains stable and deployable.

Using branches effectively allows you and your team to work on multiple features concurrently, experiment without affecting the main codebase, and propose changes that can be reviewed before integration. This leads to safer, more collaborative development.

You can create a new branch in VS Code by clicking on the branch icon in the Status Bar at the bottom of the window and typing the name of your new branch. VS Code automatically switches you to the new branch after creation. Alternatively, in the terminal, you can create a new branch with the `git branch` command and switch to it with the `git checkout` command.

```bash
git branch new-branch-name
git checkout new-branch-name
```

The two commands above can also be combined into a single command:

```bash
git checkout -b new-branch-name
```

### Merging and Pull Requests
Merging is a process in Git where the changes from one branch are integrated into another branch. This is often done after you've finished working on a feature or bug fix on a separate branch and you're ready to integrate those changes into the main line of development. 

In the terminal, you would typically switch to the branch you want to merge into (usually the main branch) and then use the `git merge` command.

```bash
git checkout main
git merge your-branch-name
```

A related concept is the pull request. While merging is a Git operation, a pull request is a functionality provided by hosting services like GitHub. Pull requests are a way to propose changes from a branch and request that someone review and merge your changes. 

Pull requests are not a part of the Git technology itself, but they are a core part of the collaborative workflow that Git enables. They are central to code review, as they allow you to share your changes with others before they're merged into the main branch. This lets teams collaborate on the changes, discuss potential modifications, and approve the final version before it's integrated.

To create a pull request, you would typically push your branch to the remote repository and then use the GitHub interface to open a new pull request. This provides an interface for reviewing the changes, having discussions, and ultimately merging the changes into the target branch.

Thus, merging and pull requests together provide a powerful mechanism for collaborative development, enabling developers to work on separate tasks, propose changes, review code, and integrate features in a controlled and iterative manner.

### Other Git Concepts and GitHub Features

#### Stashing
`Stash` is a command that takes your modified tracked files, stages changes, and saves them on a stack of unfinished changes that you can reapply at any time. This is useful when you want to switch branches, but you don't want to commit your changes yet.

To stash changes:

```bash
git stash
```

#### Rebasing
Rebasing 'replays' your branch's commits onto the tip of the specified branch, creating new commits in the process. Rebasing is particularly useful when preparing to make a pull request. It allows you to make your feature branch up to date with the latest code on the main branch. If the main branch has moved on since you branched off, rebasing can help by putting your changes on top of what everyone else has already done.

In the terminal, you would typically switch to the branch you want to rebase and then use the `git rebase` command.

```bash
git checkout your-branch-name
git rebase main
```

Rebasing rewrites history, which can be a source of confusion or even data loss for you or others if mishandled. It's generally recommended to use it only for cleaning up your own local commit history before sharing with others.

#### Squashing Commits
Squashing in Git is the act of compressing multiple commits into a single commit. This is typically done to clean up a messy commit history or to make the changes in a feature branch more digestible for the reviewer.

Squashing commits can be achieved using an interactive rebase with the `git rebase -i` command, followed by the commit you want to squash back to. This will open a text editor where you can decide what to do with each commit.

```bash
git rebase -i HEAD~n
```

In the above command, `n` should be replaced with the number of commits from the `HEAD` you want to consider to be squashed. This will provide you with a list of the last `n` commits, each prefixed with the word `pick`.

To squash the commits, you would replace `pick` with `squash` or `s` for each commit you want to squash into the previous commit. Once you've marked the commits to squash, you save and close the editor. Git then combines all the changes and opens a new editor for you to write a new commit message for the squashed commit.

Squashing allows you to create a more streamlined and understandable commit history, which can greatly facilitate code review and project comprehension. Remember to use this carefully, though, as it alters commit history.

#### Tagging
Tagging in Git is a way to mark specific points in your repository's history as being important, usually to denote project milestones or versions. Tags are refs that point to specific points in Git history, and unlike branches, they can't move or change once they're set on a specific commit.

Creating a tag in Git is straightforward. Here's an example of how to create a lightweight tag:

```bash
git tag v1.0.0
```

#### Releases
Releases are a feature of GitHub that allows you to present significant versions of your code in a more polished way. When you create a release, GitHub takes a snapshot of the repository at the point of the tag you specify. You can also attach binary files (like compiled executables, minified scripts, documentation) to a release. Moreover, releases are accompanied by release notes that you can use to describe what's new in the specific version.

#### Main Branch Protections
To ensure stability of a projects, the main branch can be protected from direct commits. This means that developers cannot directly push their changes to the main branch. Instead, changes are introduced via pull requests. This setting can be enabled in the repository settings under the "Branches" section.

Before a pull request is merged into the main branch, you can also require a review by at least one other team member. This ensures a second set of eyes on the changes, making it less likely that bugs or other issues slip into the main codebase. This setting is also found in the repository settings, under the "Branches" section.

#### GitHub Actions

GitHub Actions is a powerful feature that automates certain tasks within your GitHub repository. Actions are event-driven, meaning they can be configured to execute or "trigger" when specific events occur in your repository, such as a push to a particular branch, the creation of a pull request, or the opening of an issue. One of the key strengths of GitHub Actions is its flexibility. It can be used to automate a wide range of tasks relevant to software development, and it supports multiple languages and platforms. They may be used for tasks such as building documentation, running tests and test coverage reports, or code style checks.

## Project Documentation

### Structure
Sectioning your documentation can greatly improve its readability and navigability. Organize your information logically and use subheadings to break up text into digestible chunks. This approach can make the code usage apparent to others and make it easier to find and understand specific parts of your project. For larger documentation consider adding a table of contents or a framework that generates a structured website for your documentation.

### Usage Instructions
Documentation should provide enough information to enable users to understand how to use your code without additional external resources. Include explanations of all the main features, functions, data structures, and any assumptions or prerequisites. The aim is to make the code as user-friendly as possible.

Providing examples or tutorial of how to use your code can be an extremely helpful addition to your documentation. Examples demonstrate usage in a concrete way, help to clarify complex concepts.

### Welcoming Contributions
In your `README.md` or a separate `CONTRIBUTING.md` document, clearly specify the types of contributions that are welcome. This could include code contributions, documentation improvements, bug reports, feature requests, etc.

## Licenses
Include a license in your project, typically in the form of a `LICENSE.md` file in the top level directory. This clarifies the terms under which others can use, modify, or distribute your code.

There are many licenses available for open-source projects, two commonly used ones are the MIT License, the GNU General Public License (GPL)0.

- **[MIT License](https://opensource.org/licenses/MIT):** permissive license that is short and easy to understand. It allows people to do anything with your code with proper attribution and without warranty.

- **[GNU General Public License (GPL)](https://www.gnu.org/licenses/gpl-3.0.en.html):** is a copyleft license that requires anyone who distributes your code or a derivative work to make the source available under the same terms.

Ensure that your project adheres to the license requirements of any projects it derives from or redistributes, e.g. attribution requirements.

## Privacy
The code, as well as the entire Git history, must be free of sensitive data. Make sure to review your code and Git history thoroughly before publishing or sharing it, and never include sensitive data in your code. If your project involves disclosure of any data, first consult with our *Privacy Analyst*. This should be discussed as early as possible, typically in the project proposal stage.

## Code Readability and Style

### Comments
Comments can be highly valuable in explaining why certain decisions were made during coding. They can help future developers or yourself to understand the code. All non-trivial code blocks should be properly commented, but avoid redundant comments that just describe what the code is doing.

### Style
Consistency is key in writing maintainable and readable code. This includes consistent line length, use of whitespace, commenting style, naming conventions, and operator use. You might want to follow a style guide or set of coding conventions for your chosen language. There are code formatting tools which can help adhere to standards, including:
- **R:** [styler](https://styler.r-lib.org/), 
- **Python:** [black](https://github.com/psf/black), [autopep8](https://github.com/hhatto/autopep8)
- **Julia:** [JuliaFormatter](https://github.com/domluna/JuliaFormatter.jl)

### Succinctness 
Code should be as succinct as possible. This doesn't mean it should be densely packed and hard to read, but rather that it avoids unnecessary complexity. This makes the code more readable and maintainable.

## Code Functionality

### Correctness
Aim to write code that doesn't produce errors or warnings when loading are when in use.

Ensure your code functions as intended and produces correct results. Testing and peer review are important activities for this.

You may also consider using a linter, which is a static code analyzer which looks for potential errors and deviations from style guidelines. Common linters include:
- **R:** [lintr](https://lintr.r-lib.org/)
- **Python:** [pylint](https://pylint.readthedocs.io)
- **Julia:** [JET](https://github.com/aviatesk/JET.jl)

### Robustness
Robust code is code that can handle unexpected inputs or conditions gracefully. It doesn't break or produce incorrect results when faced with edge cases, and it has safeguards to prevent misuse.

Your code should fail gracefully in the event of an error. This means providing meaningful error messages that explain what went wrong and, if possible, how to fix the issue.

Typing of functions can ensure they are utilized as intended. Python supports *type hints* as of version 3.5. Julia supports typing as key part of its *multiple dispatch* functionality. R does not support this natively. In addition to fault-handling benefits, typing may positive impact to performance, readability, and usability.

### Efficiency
Use efficient algorithms, appropriate libraries, and data structures in your code to ensure it runs quickly, doesn't consume unnecessary resources, and scales well.

### Testing
Testing helps to ensure your code works as expected under a variety of conditions. This can be especially important as you add new features or update dependencies, ensuring there is not impact to tests. You can use of testing libraries to create and manage your tests:
- **R:** [testthat](https://testthat.r-lib.org/)
- **Python:** [pytest](https://docs.pytest.org/)
- **Julia:** [Test](https://docs.julialang.org/en/v1/stdlib/Test/)

## Reproducibility

### Randomness
Any process in your project that relies on randomization should have a mechanism for setting the random seed. The seed should be set explicitly in any analyses, examples and tests to ensure reproducibility.

### Dependencies
Utilize a framework that allows you to specify version or bounds for all project dependencies. This ensures that your project remains compatible even when dependencies update. Be aware that different programming communities adhere to semantic versioning to varying degrees, so it is recommended to verify compatibility whenever updates to dependencies are available. Consider the following frameworks for managing dependencies:

- **R:** [renv](https://rstudio.github.io/renv/index.html)
- **Python:** [poetry](https://python-poetry.org/), [pip](https://pip.pypa.io/en/stable/)
- **Julia:** [Pkg](https://pkgdocs.julialang.org/v1/)

### Packaging
Packaging your project makes it easier to distribute, share, and install. It may also help your project reach a wider audience if you list it on an official package repository. The dependency management tools listed in the previous section can assist with packaging your project.

### Containerization
Containerization is a method of packaging your code along with its dependencies so it can run uniformly across different systems, enhancing its portability. Container technologies like Docker allow you to define a container in a text file, which can then be built into a container image. This image can be distributed and run on any system that has the container runtime installed, ensuring your code runs the same way regardless of where it's being executed. Containerization is particularly useful for projects with complex dependencies, as it allows you to control the environment in which your code runs. Containerization is central to cloud native computing, microservice architectures.

## Security

Security is important for ensuring the integrity of our tools. Any disclosure of infrastructure details in a project requires consultation and sign-off from our IT Architect. Ideally this is done as part of a well thought out project proposal. Many of the steps we take to maintain security have the added benefit of making our tools more generalizable and useful to others.

### Code and Git History
Our first line of defense is the code and the Git history itself. Both should be free of sensitive data like:

- **Usernames, passwords, tokens, or secrets:** Consider using environment variables, configuration files not tracked by Git (i.e. excluded using `.gitignore`) or secure secret storage solutions.
- **Internal URLs, network names or IP addresses:** This can unnecessarily disclose internal network structure.
- **Full directories:** Relative paths should be generally used.

### Dependencies
Managing dependencies is another crucial aspect of maintaining security:

- **Minimal:** Limit your dependencies to what's necessary. Each additional dependency is another potential security vulnerability.
- **Trustworthy:** Be cautious when adding new dependencies. Ensure they are from a reliable source, and have a good reputation within the community.
- **Maintained:** A well-maintained and supported package is likely to have fewer security issues, and if any are found, they're likely to be fixed quickly.
- **Up to date:** Regularly update your dependencies. Updates often include security fixes alongside new features and bug fixes.

## Project Maintenance
Maintaining a project is just as important as its initial development. This involves regular updates, bug fixes, dependency management, and ensuring the project stays relevant and useful over time.

### Regular Updates
Even after the project's initial development phase, it's important to continue making regular updates. These updates could involve adding new features, improving performance, or updating the UI/UX based on user feedback. Regular updates show that the project is active and well-maintained.

### Bug Fixes
Despite our best efforts, bugs can and will occur in your projects. Having a robust and efficient process for tracking, addressing, and resolving these bugs is essential to maintaining the quality of your project. Utilize issue tracking systems and provide clear instructions to users on how to report bugs.

### Dependency Management
Your project's dependencies should be updated regularly. This not only allows you to take advantage of the latest features and performance improvements, but also helps to protect your project from vulnerabilities that may have been found in older versions of dependencies. However, remember to test your project thoroughly after updating dependencies to ensure nothing breaks.

### User Feedback
Users are the heart of your project. Regularly seeking and addressing user feedback helps you keep your project relevant, useful, and user-friendly. Feedback can come in many forms, including bug reports, feature requests, or direct user surveys. Be open to feedback and consider it an opportunity to improve and grow your project.

### Documentation Updates
As your project grows and changes, so should your documentation. Keeping documentation up-to-date is crucial for helping users understand how to use your project and for aiding new contributors who wish to add to your project. Treat your documentation as a living document that evolves with your project.

### Refactoring
Over time, as more features are added and bugs are fixed, your codebase can become complex and difficult to understand. Regular refactoring can help manage this complexity. Refactoring involves restructuring your code without changing its external behavior to improve code readability, reduce complexity, or improve performance. Be mindful to ensure that you have a good suite of tests in place before embarking on significant refactoring, to ensure that the behavior of your code has not inadvertently changed.

### End-of-life
Finally, there might come a time when your project has served its purpose or has been replaced by better alternatives, and you decide to stop maintaining it. In such cases, it's good practice to clearly mark the project as no longer maintained, and if possible, direct users towards other alternatives. This helps set clear expectations for users and contributors.