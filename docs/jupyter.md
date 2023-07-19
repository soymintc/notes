# Jupyter
Personal cheatsheet

## Launch session on server and port it to local
### On the server
```bash
PORT_SERVER=9988
jupyter lab --no-browser --port=$PORT_SERVER --ip "*"
```
### On local
```bash
PORT_SERVER=9988
PORT_LOCAL=9988 # does not have to be the same
ssh -L $PORT_SERVER:localhost:$PORT_LOCAL <MY_ID>@<SERVER_ADDRESS>
```

## Reload packages without referring to jupyter cache
Run the following magic upstream
```python
%load_ext autoreload
%autoreload 2
```
Another way to do it (not so recommended) is:
```python
from imp import reload 
import wgs_analysis.plots.rearrangement as svplots
reload(svplots)
```

## Using pdb (python debugger)
Documentation: https://docs.python.org/3/library/pdb.html#debugger-commands
```python
%debug  # use this magic
```
Some notable pdb commands 
```
a: list arguments of current function
b: back
u: up
c: continue until breakpoint()
n: next
whatis expression: print type of expression
p expression: print expression
pp expression: same thing as print but pretty-print
display [expression(s)]: print changes of expressions each step

Documented commands (type help <topic>):
========================================
EOF    commands   enable    ll        pp       s                until 
a      condition  exit      longlist  psource  skip_hidden      up    
alias  cont       h         n         q        skip_predicates  w     
args   context    help      next      quit     source           whatis
b      continue   ignore    p         r        step             where 
break  d          interact  pdef      restart  tbreak         
bt     debug      j         pdoc      return   u              
c      disable    jump      pfile     retval   unalias        
cl     display    l         pinfo     run      undisplay      
clear  down       list      pinfo2    rv       unt
```
