# Setting up a dev container for Go 
* Primary author: [rithwik-mishra](https://github.com/rithwik-mishra)
* Reviewer: [arshm06](https://github.com/arshm06)

## Prerequisites
- **Go Installation:** If you don't already have Go installed, follow the download and install steps [here](https://go.dev/doc/install)
???+ note
    Check which version of Go you have installed using ```#!go go version``` command. This tutorial uses Go 1.23.X
- **A GitHub account:** Make sure you have an existing GitHub account or sign up [here](https://github.com/)
- **Git Installation:** Install Git [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you do not have a preexisting installation.
- **A coding IDE:** VS Code is a great option for all platforms and is the one used by this tutorial.
- **Docker:** Docker is required to run the dev container that we create in this tutorial. [Get Docker here](https://www.docker.com/products/docker-desktop)
- **A command terminal:** Go works well using terminal in Linux or Mac and on powershell or cmd in Windows.

## Part 1: Setting up your directory with Git
### Step 1. Initialize Git and Create a Local Repository
- [ ] 1. Open terminal or your command prompt.
- [ ] 2. Create a new directory to store your project files:
``` bash
mkdir hello-go
cd hello-go
```

- [ ] 3. Turn this directory into a new GitHub repository:
``` bash
git init
```

- [ ] 4. Create a README file for your project and make your initial git commit:
``` bash 
echo "# Hello Go" > README.md
git add README.md
git commit -m "Initial commit with README"
```
### Step 2: Create a remote repository on GitHub 
- [ ] 1. Log into GitHub and go to the [Create a new repository](https://github.com/new) page.
- [ ] 2. Use the same repository name as your directory that you created, in this case we would set **Repository Name** as *hello-go*. 
- [ ] 3. Click **Create Repository**.
???+ warning
    Do not initialize the repository with a README, .gitignore, or license. We already created a README in the last step!

### Step 3: Link your local repository to GitHub
- [ ] 1. Assign the repository to the remote server with the following line:
``` bash
git remote add origin https://github.com/your-username/hello-go.git 
```
???+ note 
    Make sure you replace "your-username" with your GitHub username!

- [ ] 2. Make sure your default branch is named main by using the `#!bash git branch` command. If its not called main, you can use the command `#!bash git branch -M main`.
- [ ] 3. Push your local commits to the remote repository on GitHub:
``` bash
git push --set-upstream origin main
```
???+ note
    You can check if this command worked by refreshing your GitHub repository in your browser and seeing if the local files you created and committed were pushed to the remote repository in the cloud! You can also use ```#!bash git log``` in your local terminal to see if the commit ID and message matches the commit ID of the most recent commit in your remote repository.

## Part 2: Setting up a Dev Container in VS Code
Setting up a dev container is an important part of every programming project. Dev container ensures efficient and seamless collaboration between team members by creating a pre configured environment that is standardized across machines. This way, there wont be any problems stemming from individual machine setups since all team members have an identical environment with the exact same programming language, libraries, and dependency versions. We can create this dev container in VS Code by making a devcontainer.json file.

### Step 1: Add Development Container Configuration in VS Code
- [ ] 1. Open your ```hello-go``` directory in VS Code by clicking File > Open Folder and locating your local directory.
- [ ] 2. Install the **Dev Containers** extension in VS Code if you don't have it already by clicking on the Extensions button in the sidebar and searching for the one made by **Microsoft**.
- [ ] 3. Create a ```.devcontainer``` directory in the root of your project, and then create a ```devcontainer.json``` file inside that directory. 
- [ ] 4. In the dev container file, we will specify the following environment variables:
    * **Name**: A descriptive name for your dev container
    * **Image**: The docker image to use in the environment, in this case we will use the latest Go environment from Microsoft
    * **Customizations**: This variable specifies useful customizations to VS Code, which in our case is installing the Go extension when the environment is built.
    * **postCreateCommand**: This variable specifies what command the environment should run after its been created.

Copy the following code inside your ```devcontainer.json``` file:   
``` json
    {
        "name": "Go Dev Container",
        "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
        "customizations": {
            "vscode": {
                "settings": {
                    "extensions": ["golang.go"]
                }
            }
        },
        "postCreateCommand": "go version"
    }
```

### Step 2: Reopen the project with your VS Code dev container
Re open your VS Code workspace inside your dev container by pressing ```Ctrl + Shift + P``` on Windows or ```Cmd + Shift + P``` on Mac followed by typing and selecting "Dev Containers: Reopen in Container". Once your dev container finishes setting up, you can close the terminal and should see the current version of Go being used in the container since we specified ```go version``` to be our post create command.

## Part 3: Creating your Go module and file
- [ ] Enable dependency tracking for your Go project using the following command:
``` bash
go mod init example/hello
```
???+ note
    Usually we would link the dependency tracking module to an actual github repository location, such as github.com/mymodule, but for the purposes of this example we can just use example/hello

- [ ] Create a file called ```hello.go```, paste the following code, and then save the file:
``` go
package main

import "fmt"

func main() {
    fmt.Println("Hello, COMP 423")
}
```

- [ ] Run the ```#!bash go run .``` command to see the output of the code! It should print the string "Hello, COMP 423" to the terminal.
- [ ] Alternatively, we can create a Windows executable using the ```#!bash go build```, very similar to how we used the GCC command in COMP 211 when compiling C programs as runnables. This command, unlike ```#!bash go run .```, only compiles our program instead of running it. 
- [ ] Run the executable using ```#!bash ./hello-go``` on Macbook or ```#!bash hello-go.exe```. It should have the same output as the ```go run . ``` command above.

