# Setting up a Dev Container for Rust 

* Primary author: [Jacob Gogel](https://github.com/jacobala1)
* Reviewer: [Jonathan Jacob](https://github.com/hashunc)



Welcome! In this tutorial you will learn how to create a basic development container for the Rust programming language. Along the way you will gain familiarity with setting up container through VS Code and even be able to wrtie and run a basic Rust program. 

## Why is This Important? 

Setting up a developement container for specific coding languages allows for efficient collaboration by enabling all users to work in the same environment (language version, specific extensions needed, etc...) regardless of their machine and without the need of manually installing them on your machine. Being able to build, understand, and utilize containers is an important aspect for software developers and further broadens your technical skillset.

## Prerequisites

Before beginning this tutorial, please ensure you have [^1]:

 1. **A GitHub account**: If you don't have one, sign up at [GitHub](https://github.com).
 2. **Git installed**: [Install Git](https://git-scm.com) if you don't already have it.
 3. **Visual Studio Code (VS Code)**: Download and install it [here](https://code.visualstudio.com)
 4. **Docker installed**: Needed to run the dev container. [Get Docker here](https://docker.com/products/docker-desktop/).
 5. **Command Line Basics**: Familiarity with the command line will be beneficial in understanding how to set-up the environment.

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

4. Create a README file where you can explain what your project is about [^1]. 

    ```bash
    echo "# Creating a Rust Dev Container" > README.md
    git add README.md
    git commmit -m "Initial commit with README"
    ```


### Step 2. Creating a Remote Repository

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
    Once your ready to make your changes present on the remote repo you'll need to push your commits to the remote repository. If you are on a branch that is not currently represented in the remote repo, when you push for the first time you'll type `git push --set-upstream origin <branch-name>`, allowing the repo to track it. After that, pushes with the same branch don't require the `--set-upstream` flag.


## Part 2. Creating the Dev Container

Now that your repository is set up, open up VS Code and open the folder containing your repo. Then, follow these steps to set up the dev container:

1. In the root directory of your project, create a folder named `.devcontainer`. This directory will contain the the files that VS Code will read to configure and run the dev container.

2. Install the **Dev Containers** extension for VS Code

3. Create a file within `.devcontainer` called `devcontainer.json`. This file holds the contents to be configured for the container.

4. Fill the contents of the `.json` file with the following:

    * `name`: Name of the dev container
    * `image`: The base image for the container. Specifies what language the environment will run for all users. In this case we are using a basic image provided by Microsoft to run the latest version of Rust.
    * `customizations`: In this part of the file you specify useful extensions in VS Code for the container to configure. In this case we are added the Rust Analyzer extension which adds additional features for developers to edit, format, and error check Rust programs. 
    * `postCreateCommand`: This runs commands post the creation of the dev container. In our case we run will run a commnad that shows us the version of Rust being used to confirm the container is working correctly.    

    ```json
    {
        "name": "Rust Dev Container",
        "image": "mcr.microsoft.com/vscode/devcontainers/rust:latest",
        "customizations": {
            "vscode": {
                "settings": {},
                "extensions": ["rust-lang.rust-analyzer"]
            }
        },
        "postCreateCommand": "rustc --version"
    }
    ```
!!! note "Image vs Container"
    As mentioned above the image provides the details on the programming language the container will configure and install in the environment. The container is simply the running environment after everything in the `.json` file has been configured. 

At this point you should be able to open your project repository in the container. To do so, open up Docker Desktop and then go back into VS Code, press `Ctrl + Shift + P` which opens up the command palette for VS Code and then search and click on `Dev Containers: Reopen in Container`. 

## Part 3. Creating a Basic Rust Program

Now that your project is running in the dev container, let's create a simply hello program in Rust.

### What is Rust?

Rust is a systems programming language that runs swiftly, prevents segfaults, and guarantees thread safety. It is dessigned to be a safem concurrent, and practical language. Rust has a rich type system and ownership model guranteeing memory safety, enabling you to eliminate a variety of bugs at complie-time. For more information, visit the [official Rust documentation](https://www.rust-lang.org/learn).


### Step 1. Create a new Rust project:

Using the terminal in VS Code, type the following to create a new Rust project:

    ```bash
    cargo new hello_comp423 --vcs none
    ```

#### What is Cargo?

Cargo is the Rust package manager and build system. Cargo handles tasks such as building your code, downloading the libraries your code depends on, and building those libraries. When you create a new Rust project using `cargo new`, Cargo will generate a project structure with a `Cargo.toml` file, which is used to specify the project's dependencies and metadata. For more infomation, visit the [official Cargo documentation](https://doc.rust-lang.org/cargo/index.html). In our project it will look like:

    ```
    hello_comp423
    |--- Cargo.toml
    |___ src
            |__ main.rs
    ```

!!! note "--vcs none"
    When using `cargo new` it will try to create a new Git repository for your project so we add `--vcs none` to the end of the command to tell the Version Control to not create one since we already have.

### Write the program

1. Open up the `main.rs` and replace its contents with:

    ```rust
    fn main() {
        println!("Hello COMP423");
    }
    ```

2. Complie and run the program:

    To compile, run:

    ```bash
    cargo build
    ```
    This command is similar to the `gcc` command you may be familiar with, in that, it complies your code. The compiled binary will be located in a directory labeled `target/debug`.

    Then, to run the compiled binary, type this on the command line:

    ```bash
    ./target/debug/hello_comp423
    ```

    Alternatively, you can just use the command `cargo run`, complies and runs the program in one go.



You've now successfully created a Rust dev container and run a program on it. Congradulations!!!


## Sources

[^1]: [Starting a Static Website Project with MkDocs by Kris Jordan](https://comp423-25s.github.io/resources/MkDocs/tutorial/#step-2-create-a-remote-repository-on-github)
[^2]: [Rust Development Container Images](https://hub.docker.com/r/microsoft/devcontainers-rust)


