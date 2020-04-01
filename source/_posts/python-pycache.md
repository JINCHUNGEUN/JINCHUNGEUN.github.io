---
title: Abount python's __pycache__
date: 2020-03-30 09:21:43
tags: python
categories: python
---

<em>Python Version2.x will have .pyc when interpreter compiles the code. </em>
<em>Python Version3.2 and later will have __pycache__ when interpreter compiles the code</em>

## So:

- What is __pycache__
- When it is created
- What it is for
- How to ignore it in python project

I will explain about these questions from what i understand. 


### 1. What is __pycache__
When you run run a program in python, the interpreter compiles it to bytecode first and stores it in the __pycache__ directory. If you look in there you will find a bunch of files sharing the names of the .py files in your project's folder.only their extensions will by .pyc or .pyo. These are bytecode-compiled and optimized bytecode-compiled versions of your program's files. 
When the project executed again, If the interpreter identifies that the *.py script has not been modifed, it skips the compile step and runs the previously generated *.pyc file stored in the __pycached folder


### 2. When it is created
When a module is imported for the first time(or when the source file has changed since then current compiled file was created). a .pyc file containing the compiled the code should be created in a `__pycache__` subdirectory of the directory containing .py file.   
The `.pyc` file will have a filename that starts with the same name as the `.py`, and ends with `.pyc`, with a middle component depends on the particular python binary that created it: `module.version.pyc`


```
import module
```

### 3. Waht it is for
All it does is just make your program  start a little faster. When your program change, they will be recompiled, and if you delete the files or the whole folder and run your program again, they will reappear.
I don't recommend deleting these files or suppressing creation during development as it may hurt performance.

### 4. How to ignore
Just add  code below to .gitignore. It will ignore all files under __pycache__ folder recursivly
```
**/__pycache/
```

Ohterwise If you need to ignore a file already under version control. update the the index to ignore changes to files already under version control 
```
git update-index --assume-unchanged {files}
# or
git rm -r --cached {folder}
```


Note: from python3.8 you can use an environment variable to change to location for the annoying cache directories