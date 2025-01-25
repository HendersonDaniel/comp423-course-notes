# Setting up a dev container for Rust

* Primary author: [Daniel Henderson](https://github.com/HendersonDaniel)
* Reviewer: [Maxim Chadaev](https://github.com/maximdolphin)

## Prerequisites
Before we dive in, make sure you have:

1. A GitHub account: If you don’t have one yet, sign up at [GitHub](https://github.com/).
2. Git installed: Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don’t already have it.
3. Visual Studio Code (VS Code): Download and install it from [here](https://code.visualstudio.com/).
4. Docker installed: Required to run the dev container. Get Docker [here](https://www.docker.com/products/docker-desktop).

## Part 1. Project Setup: Creating the Repository
### Step 1. Create a Local Directory and Initialize Git
1. Open your terminal or command prompt.
2. Create a new directory for your project or navigate to the directory you would like it to be located in. 
```
mkdir <project-name>
cd <project-name>
```
3. Initialize a new git project.
```
git init
```
4. Create a `README.md` file and make your first commit.
```
echo "# My Rust Project" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Step 2. Create a Remote Repository on GitHub
1. Log in to your GitHub account and navigate to the Create a New Repository page.
2. Fill in the details as needed. Make sure to set your repository name to the same name you used for your directory.
3. Click Create Repository.

### Step 3. Link your Local Repository to GitHub
1. Add the GitHub repository as a remote:
```
git remote add origin https://github.com/<your-username>/<project-name>
```
Replace `<your-username>` and `<project-name>` with your GitHub username and project name respectively.
2. Check your default branch name with the subcommand `git branch`. If it's not `main`, rename it to `main` with the following command: `git branch -M main`.
3. Push your local commits to the GitHub repository:
```
git push --set-upstream origin main
```

## Part 2. Setting Up the Development Environment

### Step 1. Add Development Container Configuration
1. In VS Code, open your project's directory. You can do this via: File > Open Folder.
2. Install the [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) extension for VS Code.
3. Create a `.devcontainer` directory in the root of your project with the following file inside of this "hidden" configuration directory:

`.devcontainer/devcontainer.json`

The `devcontainer.json` file defines the configuration for your development environment. Here, we're specifying the following:

* `name`: A descriptive name for your dev container.
* `image`: The Docker image to use, in this case, the latest version of a Rust environment.
* `customizations`: Adds useful configurations to VS Code like installing the [rust-analyzer](https://code.visualstudio.com/docs/languages/rust) extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.

```
{
  "name": "My Rust Project",
  "image": "mcr.microsoft.com/vscode/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  }
}
```

### Step 2. Reopen the Project in a VSCode Dev Container
Reopen the project in the container by pressing `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded.

Once your dev container setup completes, close the current terminal tab, open a new terminal pane within VSCode, and try running `rustc --version` to check if your container is running the latest version.

## Part 3. Setting up the Rust Project

### Step 1: Initialize the Project
We will now go through the steps for creating a new project in Rust. 

1. In your dev container's terminal in your project's directory, run `cargo new <subdirectory-name> --vcs none`. The flag `--vcs none` (Version Control System) prevents a new `git` repository from being created on your behalf. This will create a new directory.
2. Navigate into this directory through the terminal to the subdirectory.
```
cd <subdirectory-name>
```
3. Open `main.rs` and edit the default "Hello World!" program into "Hello COMP423!" as follows:
```
fn main() {
    println!("Hello COMP423!");
}
```
4. Save and then run `cargo run`. This will compile and run the program. You should see the output `Hello COMP423` in your terminal after.

!!! note

    You can also run `cargo build`. This will compile the program into an executible which you can find in the target folder. This is different from `cargo run` because it does not immediately run the program after it compiles it. Use `cargo build` when you want to send the executible file to others and not run it immediately. This executable file can be found in the `target/debug/`directory, and it will be of the same name as `<subdirectory-name>`. You can run this file by running `./target/debug/<subdirectory-name>` in your terminal, provided you are in the `<subdirectory-name>` directory.

    !!! note

        For those who are familiar with the C programming language, `cargo build` is Rust's way of compiling the program into bytecode, just like `gcc main.c -o my_program`. On the other hand `cargo run` does that, as well as running `./my_program` right after.


### Step 2: Push to GitHub
Now you can commit and push these changes to github. First, navigate out of the subdirectory.
```
cd ..
```
Then stage your changes and commit them, with an appropriate message, before pushing to your remote repository.
```
git add .
git commit -m "Created Rust project"
git push origin main
```
Now, you are done!

## References
[Citation 1 -> Kris Jordan's Tutorial](https://comp423-25s.github.io/resources/MkDocs/tutorial/)
