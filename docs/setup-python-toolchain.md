# Setup python toolchain

Python has a lot of tools that make it flexible to work with, but starting out can feel a bit tricky, especially for beginners. In this article, we’ll talk about one important concept in the Python world and focus on a tool called `uv`. We’ll also mention some other helpful tools you can use when you're just getting started.

Before we begin, it’s worth noting that you can write and run Python programs without using extra tools like [uv](https://docs.astral.sh/uv/), [poetry](https://python-poetry.org/) or [pyenv](https://github.com/pyenv/pyenv),. However, managing your Python setup and dependencies can get complicated. Without these tools, you might spend more time fixing problems like version conflicts or broken environments than actually writing code.

> We'll also be using a system command shell interface, like the native [Terminal](https://support.apple.com/en-ge/guide/terminal/welcome/mac), [Alacritty](https://alacritty.org/index.html), [iTerm](https://iterm2.com/), or any other preferred shell.

## Packages management 

Let’s start from the very beginning — setting up Python and the essential tools. We'll be using a system package manager [^1] for this. On macOS, the most common package manager is `brew`, so let's install it first:

```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

> `brew` works similarly to [apt](https://ubuntu.com/server/docs/package-management), [pacman](https://wiki.archlinux.org/title/Pacman), or [yay](https://github.com/Jguer/yay) for Linux distributions, and [Chocolatey](https://chocolatey.org) for Windows.

Once installed, let’s verify that `brew` is ready:

```shell
brew -v
```

You should see output similar to this:

```shell
Homebrew 4.4.0
```

Now we’re ready to proceed with installing the Python toolchain. You can also use `brew` to install other essential tools like [Git](https://git-scm.com/), [Neovim](https://neovim.io/), [Docker](https://www.docker.com/), and more.

## Project management

Now, let's install `uv`, the Python package and project manager : [^1][^2]

```shell
brew install uv
```

Once the installation is complete, verify that `uv` is ready to work:

```shell
uv -V
```

The output should look like this:

```shell
uv 0.4.18 (Homebrew 2024-10-01)
```

Now we’re ready to create our first Python project and run our first Python program. But before we do that, it’s a good idea to create a folder for your future projects rather than keeping everything in the root directory. Let’s create one and navigate into it:

```shell
mkdir Projects; cd Projects/
```

Next, let's initialize the project using `uv`:

```shell
uv init how-to-python
```

The output should look something like this:

```shell
Initialized project `how-to-python` at `/Users/user/Projects/how-to-python`
```

> Here, `user` is the name of your current user in macOS, and `how-to-python` is the name of the project as well as the directory.

The command creates a few files inside the project directory. Let’s take a closer look:

```shell
how-to-python
├── .git               # Git repository directory
├── .gitignore         # Files ignored by Git
├── .python-version    # Python version used by the project
├── README.md          # Project’s title and description
├── hello.py           # Python program file
└── pyproject.toml     # Project configuration file
```

Now, let's run the program created by `uv`:

```shell
uv run hello.py
```

And the output might be a bit surprising:

```shell
Using CPython 3.12.3 interpreter at: /Users/user/.pyenv/versions/3.12.3/bin/python
Creating virtual environment at: .venv
Hello from how-to-python!
```

> In this example, `uv` is using a Python interpreter installed via `pyenv`. If you haven’t installed a Python version using version managers, it will use the default Python version installed on your system.

This is a simple "Hello, World!" script. However, besides running the script, `uv` also creates a virtual environment [^3] and locks the project dependencies [^5]. This happens because `uv` didn't find an existing virtual environment or a lock file.

```shell
how-to-python
├── .git
├── .gitignore
├── .python-version
├── .venv              # Virtual environment directory
├── README.md
├── hello.py
├── pyproject.toml
└── uv.lock            # Lock file for project dependencies
```

## Discussion

Let’s pause for a moment and think about all the files we now have. Do we really need all of them to run a simple one-line Python script?

As I mentioned earlier, the Python interpreter doesn’t require any third-party tools to run Python code. However, Python programs are usually more complex, and many of them rely on packages outside the Python Standard Library [^6].

 Some of these packages may conflict with each other or require a specific version of Python. To manage this complexity across multiple projects, Python developers typically use project managers and Python version managers.

`uv` serves as both a project manager and a Python version manager. It offers a handy interface that makes it easier to get started compared to other tools like [poetry](https://python-poetry.org/), [pyenv](https://github.com/pyenv/pyenv), and [pipfile](https://github.com/pypa/pipfile). However, behind the scenes, `uv` still follows common concepts like virtual environments [^3] and dependency management.

## Conclusion

We’ve taken a step-by-step approach to setting up Python with `brew` and `uv`. By following these instructions, you’ve successfully installed the tools and created your first Python project.

While it’s possible to run Python without extra tools, we saw how `uv` simplifies project management by organizing everything in one place. It creates the necessary project files and manages dependencies automatically.

`uv` acts as both a project manager and a Python version manager, making it a convenient choice for handling everything in one tool. It follows common practices like virtual environments and dependency management, but it’s designed to be easy to use.

## Footnotes

[^1]: **Package Manager**: A tool that automates the installation, upgrading, configuration, and removal of software programs in a consistent manner.

[^2]: **Project Manager**: A tool or script that provides a standard interface to manage a project’s environment, dependencies, and configuration settings, streamlining the development process.
   
[^3]: **Virtual Environment**: An isolated Python environment that keeps a project’s dependencies separate from the system’s global Python installation, avoiding conflicts between different projects.

[^4]: **Git repository**: A system that stores and tracks changes to project files, enabling collaboration, version control, and easy reversion to previous versions.

[^5]: **Dependencies locking**: A process that captures exact versions of project dependencies, ensuring consistency across different environments and preventing version conflicts.

[^6]: **Python Standard Library**: A collection of built-in modules and packages that come with Python, providing tools for common tasks like file handling, math operations, and network communication without needing external libraries.

## References

1. [Homebrew (brew.sh)](https://brew.sh/)
2. [uv (astral.sh)](https://docs.astral.sh/uv/)
3. [Package management (ubuntu.com)](https://ubuntu.com/server/docs/package-management)
4. [git (git-scm.com)](https://git-scm.com/)
5. [poetry (python-poetry.org)](https://python-poetry.org/docs/)
6. [pyenv (github.com)](https://github.com/pyenv/pyenv)
7. [The Python Standard Library (python.org)](https://docs.python.org/3/library/index.html)
