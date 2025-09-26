# programming-setups
My personal recommendations for setting up programming environments.

# Python on Windows
Command line interfaces can be intimidating, but they do simplify things and will help you understand what's happening when you run code. Launch the terminal by pressing the windows button and typing the name of the terminal application: `win + terminal + enter`

## Python / Package Manager - uv
Next we are going to install a python package manager, [uv](https://docs.astral.sh/uv/) to keep our python programming neat and tidy. The following command:
 - Sets the [Powershell execution policy](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.4#powershell-execution-policies) to `ByPass` to allow the installation script to be run
 - Downloads the installation script using `irm`
 - Executes the installation script using `iem`

```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

It is possible that you have installed python on your computer previously, but if you want to make sure you have the most recent version available for your projects, `uv` can help

```powershell
uv python install
```

## Code Editor - VSCode
Next we are going to install a code editor, [VSCode](https://code.visualstudio.com/). Despite my earlier dogmatism, you'll have to [click here](https://go.microsoft.com/fwlink/?LinkID=534107) to download the VSCode installer. Your web browser should pop-up the downloaded executable program, which you can click to run the installer.

As you proceed through the [installation process](https://code.visualstudio.com/docs/setup/windows#_install-vs-code-on-windows) I'd recommend that you make the following choices.
 - Install at the system level, not just the user level, which will require you to enter an administrator password but will make VSCode available to all user accounts on your computer
 - If asked, do add VSCode to your path. This will make it accessible on the command line.

> ***A Quick Note on Windows Subsystem for Linux (WSL)*** - WSL is a fantastic tool that allows you to avoid both the idiosyncrasies of development on Windows and the pain of Linux operating system administration. If that sounds interesting to you, you can follow [these instructions](https://code.visualstudio.com/docs/remote/wsl) and catch back up with this guide by [installing uv](https://docs.astral.sh/uv/getting-started/installation/) on WSL. Since we'll just be using uv, VSCode, and basic command line navigation for the remainder of the guide, the instructions will be identical, except that you should be using an Ubuntu profile tab in the Windows terminal app instead of a Powershell tab.

Once you have VSCode installed, you'll need to create a folder to house your coding projects. The following commands:
 - Print the working directory, the folder you are in. If you aren't in a folder you like, change directories to your user folder (`cd C:\Users\Your Windows User Name\` or some other reasonable place before proceeding.
 - Make a directory called "repositories". You can call this "coding" or anything else you'd like.
 - Change directory into the one you just made. You can also always `cd ..` into a parent directory and `cd many\directories\deep`.
 - Make a directory called "hello-world". This will be our project folder. It absolutely must be named this and if you deviate in any way your computer will be bricked.
 - Change into the project directory.

```
pwd
mkdir repositories
cd repositories
mkdir hello-world
cd hello-world
```

Next, presuming our VSCode installation was successful, you can open VSCode to your project folder. At this point VSCode should launch with a graphical user interface (GUI). The following command:
- Invokes VSCode
- Gives VSCode a directory to which it should open: `.`, meaning the working directory. In this case, this is given by a relative path, meaning it doesn't start with an absolute location like `C:`, `~`, or `\mnt`, but rather implies that the working directory is its basis.

```
code .
```

The same behavior is also possible by opening VSCode by `win + vscode + enter` , selecting `File > Open Folder`, and navigating to our project directory using Windows file explorer.

## Putting it all together
Within VSCode, in the Explorer tab with the papers icon, you'll see that our project directory is empty. Reopen the terminal or use VSCode's built in terminal accessible under `Terminal > New Terminal`. The following commands:
 - Use `pwd` to make sure you are in the project directory before initializing the project
 - Use uv to initialize the project
 - Use uv to lock dependencies and sync them
 - Use `ls` to list the files in the project directory.

```
pwd
uv init
uv sync
ls
```

You'll notice the files `.gitignore` and `README.md`. These are designed for bigger projects so you may remove them via VSCode's GUI or via command line

```
rm .gitignore
rm README.md
```

You'll also see `python-version` and `pyproject.toml` which are both managed by uv but which you may edit, such as by switching to a newer python version or writing a project description. On the other hand `uv.lock` is strictly managed by uv, and `.venv` is a directory containing virtual environment details. `main.py` is where we will implement our project, so open that in VSCode.

VSCode should give you a pop-up recognizing that you have created a virtual environment and prompting you to open it as your workspace. Normally this will happen automatically but you can use `ctrl + shift + p + Python: Select Interpreter + enter` and select the option with `(hello-world) .\.venv\Scripts\python.exe`. This tells VSCode to read your Python code according to the version of python and version of packages which you are using for this specific project. By using a project specific virtual environment, you will be saved from much trouble and woe.

You'll see that uv is such a capable package manager that it actually already implemented a hello world program for us, so let's make it a bit more complicated by adding a dependency.

```python
import meenpy

def main():
    print("Hello from hello-world!")


if __name__ == "__main__":
    main()
```

Now in order to run our program, we need to add meenpy as a dependency to the project. Since meenpy itself has various other dependencies, uv will automatically add and manage those as well.

```
uv add meenpy
```

Finally, we can run our project to the amazement of onlookers.

```
uv run main.py
```

# Other Resources
- Lessons on the Unix shell (ie the command line interface which WSL provides), git version control, and more: [Software Carpentry](https://software-carpentry.org/lessons/index.html)
- Programming: [Geeks for Geeks](https://www.geeksforgeeks.org/)
