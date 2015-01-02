Title: Pyramid tutorial
Date: 2015-01-02
Category: Python
Status: draft

## Prerequisites

In order to follow this tutorial, you should have:

* a Unix-like (such as OS X or Linux)
* Python
* Git

## Setting up a Python virtualenv

A *virtualenv* (or *venv*) is an isolated Python environment where we’ll be able to install packages locally, in isolation from the global Python packages.

### Installing virtualenvwrapper

In this tutorial, we’ll use [virtualenvwrapper](https://pypi.python.org/pypi/virtualenvwrapper) to create and manage virtualenvs. To learn how to install and use it, you may want to read this companion tutorial first: ["Working with Python virtualenvs"]({filename}/virtualenv.md)

### Creating a virtualenv

We’ll use the `mkvirtualenv` command from *virtualenvwrapper* to create a *virtualenv*:

```
$ mkvirtualenv pyramid-tutorial
```

### Setting up a working directory

Let’s create a directory where we can put our files:

```
$ mkdir pyramid-tutorial
$ cd pyramid-tutorial
```

Using *virtualenvwrapper*, we can associate this working directory with our virtualenv:

```
$ setvirtualenvproject
```

Now, each time we will use the `workon pyramid-tutorial` command, the virtualenv will be activated and the current directory will be changed to the project’s working directory.

We can also use the `cdproject` command to go back to this directory at any time.

## Starting a pyramid project

First, we’ll make sure that the virtualenv is activated:

```
$ workon pyramid-tutorial
```

Then we’ll install the `pyramid` package from the Python Package Index (PyPI):

```
$ pip install pyramid
```

## Using version control

We initialize a git repository:

```
$ git init
```
