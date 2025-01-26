# Setting up a Dev Container for Rust 

* Primary author: [Jacob Gogel](https://github.com/jacobala1)
* Reviewer: [Jonathan Jacob](https://github.com/hashunc)
* Structure of Tutorial Inspired By: ([Starting a Static Website Project with MkDocs by Kris Jordan](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-2-create-a-remote-repository-on-github))


Welcome! In this tutorial you will learn how to create a basic development container for the Rust programming language. Along the way you will gain familiarity with setting up container through VS Code and even be able to wrtie and run a basic Rust program. 

## Why is This Important? 

Setting up a developement container for specific coding languages allows for efficient collaboration by enabling all users to work in the same environment (language version, specific extensions needed, etc...) regardless of their machine. Being able to build, understand, and utilize containers is an important aspect for software developers and further broadens your technical skillset.

## Prerequisites

Before beginning this tutorial, please ensure you have:

 1. **A GitHub account**: If you don't have one, sign up at [GitHub](https://github.com).
 2. **Git installed**: [Install Git](https://git-scm.com) if you don't already have it.
 3. **Visual Studio Code (VS Code): Download and install it [here](https://code.visualstudio.com)
 4 **Docker installed**: Needed to run the dev container. [Get Docker here](https://docker.com/products/docker-desktop/).
 5 **Command Line Basics**: Familiarity with the command line will be beneficial in understanding how to set-up the environment.

## Part 1. Project Setup: Creating the Repository


### Step 1. Setting Up a Local Git Repository 

1. Open your terminal/command prompt.

2. Create a new directory or change into a parent diretory for where you'd like the direcotry to be stored on your machine.

```bash
mkdir rust-dev-container
cd rust-dev-container
```

3. Initialize a new Git repository:
```bash
git init
```

!!! note "What is init?"
    'init' is a subcommand for Git that makes your directory function as a local Git repository for you to use other subcommands to make commits and save and push work to a remote repository on GitHub to share your work with others if you desire

4. Create a README file where you can explain what your project is about. 

```bash
echo "# Creating a Rust Dev Container" > README.md
git add README.md
git commmit -m "Initial commit with README"
```

### Creating a Remote Repository

If you would like to share your dev container with others, set up a remote repository on GitHub and link it with your local repository allowing other users to se changes/updates you make.

(1) Log in to GitHub and go to [Create a New Repository](https://github.com/new)

(2) Fill out the details for your repository:
    - **Name**: Make it the same or something similar to the local repo name
    - **Description**: Provide a description like "Basic dev container for Rust"
    - **Visibility**: Make it public

(3) Do not initialize the repository with a README.md, .gitignore, or license

(4) Click **Create Repository** 

(5) Link your local repo with the remote one. In your terminal do the following:
```bash
git remote add origin https://github.com/<your-username>/<remote-repo-name>.git
```

!!! note "Pushing to remote repo"
    Once your ready to make your changes present on the remote repo you'll need to push your commits to the remote repository. If you are on a branch that is not currently represented in the remote repo, when you push for the first time you'll type `git push --set-upstream origin <branch-name>`, allowing the repo to track it. After that pushes with the same branch don't require the `--set-upstream` flag.

