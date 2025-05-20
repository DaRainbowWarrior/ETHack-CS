[Back to Main page](README.md)

# Python library Hijacking

It's basically just making a usual python library file (eg. `random.py`) and modifying the `$PATH` variable to search and find ours faster than the original one, executing it and any code in it

### Making a fake python library
- In the same directory make a python file named like an included library in the executable code
- Usually it's good to include code running a bash instance `import pty; pty.spawn('/bin/bash')`
    - It's really only useful if the python executable can be run in another, probably more privileged user's name

### Modifying the PATH variable
- With one command we can add the current directory, or any to the PATH
    - Firstly `echo $PATH` and copy the current variables
    - `export PATH = <path with the fake library>:<the rest of the path copied the step before>` 
- It is adviced to add the directory which the executable and our fake library is located, otherwise it might not work