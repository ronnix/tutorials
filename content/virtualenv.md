Title: Working with Python virtualenvs
Date: 2015-01-02
Category: Python

## Prerequisites

In order to follow this tutorial, you should have:

* a Unix-like (such as OS X or Linux)
* Python

## What is a Python virtual environment?

A *virtualenv* (or *venv*) is an isolated Python environment where we can install packages locally, in isolation from the global Python packages.

When you're working on multiple projects, it also allows different projects to use different versions of the same framework or library.

## The tools

The traditional way to create *virtualenvs* is using the aptly-named [virtualenv](https://pypi.python.org/pypi/virtualenv) tool by Ian Bicking.

A popular enhancement is [virtualenvwrapper](https://pypi.python.org/pypi/virtualenvwrapper) by Doug Hellmann, that makes it more convenient to use and adds some powerful features.

In this tutorial, we'll first see how to use *virtualenv* directly, then we'll see how to use *virtualenvwrapper*.

Note that starting with version 3.3, Python comes with some basic support for virtualenvs, including the new `pyvenv` command: https://docs.python.org/3/library/venv.html

## Option 1: virtualenv

In this section, we'll see how to create and manage *virtualenvs* using the [virtualenv](https://pypi.python.org/pypi/virtualenv) tool.

### Installing virtualenv

We’ll start by installing `virtualenv` using the pip package manager:

```
$ pip install virtualenv
```

Note that you may need to use `sudo` to run the command with administrative privileges:

```
$ sudo pip install virtualenv
```

### Creating a virtualenv

To create a virtualenv, we must provide the name of the directory that will contain the virtualenv files. If the directory does not exist, it will be created:

```
$ virtualenv VENV
New python executable in VENV/bin/python2.7
Also creating executable in VENV/bin/python
Installing setuptools, pip...done.
```

Note that if you don't want to use the default Python interpreter, you can choose to use a specific one in this virtualenv using the `--python` flag. For example:

```
$ virtualenv VENV --python=/usr/local/bin/python3.4
```

We can see that the `virtualenv` command has created a `VENV` directory, and that this directory contains several subdirectories:

```
$ ls VENV
bin     include lib
```

### Working with a virtualenv

The `bin` subdirectory contains a `python` executable that is bound to this virtualenv. This is an isolated Python interpreter, that only has access to the packages installed within the virtualenv:

```
$ VENV/bin/python --version
```

The `bin` subdirectory also contains a `pip` executable that can be used to install packages inside the virtualenv:

```
$ VENV/bin/pip install somepackage
```

The Python files from installed packages will typically be found in `VENV/lib/pythonX.X/site-packages/` (the exact path depends on the Python version), and any included scripts will be in `VENV/bin/`.

### Activating a virtualenv

Each virtualenv comes with a convenient shell script that can modify the shell's `PATH` viariable so that commands from the virtualenv (that is those in the `VENV/bin` directory) are the first to be found.

This script also changes your prompt to remind you that you're working with this specific virtualenv.

```
$ source VENV/bin/activate
(VENV)$ which python
(VENV)$ which pip
(VENV)$ echo $PATH
(VENV)$ echo $VIRTUAL_ENV
```

Note that you need to use `source` in order to run the script in the context of the current shell (otherwise the script would be run in a sub-process, and could not change the environment of its parent shell).

When you're done, you can revert those changes by using the `deactivate` alias:

```
(VENV)$ deactivate
```

## Option 2: virtualenvwrapper

The most convenient and most powerful way to create and manage virtualenvs is to use [virtualenvwrapper](https://pypi.python.org/pypi/virtualenvwrapper). As its name suggests, it is built on top of the *virtualenv* tool.

### Installing virtualenvwrapper

We’ll start by installing `virtualenvwrapper` using pip:

```
$ pip install virtualenvwrapper
```

You may need to use `sudo` to run the command with administrative privileges:

```
$ sudo pip install virtualenvwrapper
```

Then you must add the following lines to your shell startup script (typically `$HOME/.bashrc`):

```
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/Devel
source /usr/local/bin/virtualenvwrapper.sh
```

Note that you have to source this file in order to apply the changes to the current shell:

```
$ source $HOME/.bashrc
```

## Creating a virtualenv

Now we’ll use the `mkvirtualenv` command to create a *virtualenv*:

```
$ mkvirtualenv myproject
```

Note that the virtualenv directory is not created in the current directory, but in the `$WORKON_HOME` directory.

A nice benefit of this is that files from the virtualenv are not mixed with your project files, so there is no need to add configuration to your text editor or version control system to ignore them.

Also note that the prompt has changed to tell you that the *virtualenv* has automatically been activated (no need to manually source the `activate` script).

## Activating a virtualenv

To activate an existing virtualenv, *virtualenvwrapper* provides a command called `workon`, that supports autocompletion:

```
$ workon myproject
```

When you are done working with a virtualenv, you can deactivate it:

```
$ deactivate
```

### Setting up a project directory

Let’s say we want a directory where we can put our project source code:

```
$ mkdir myproject
$ cd myproject
```

The `setvirtualenvproject` allows us to associate this working directory with our virtualenv:

```
$ setvirtualenvproject
```

Now, each time we will use the `workon myproject` command, the virtualenv will be activated and the current directory will be changed to the project’s working directory.

We can also use the `cdproject` command to go back to this directory at any time.
