## Module 
``` module ``` implements ``` require ``` function. 
Since ``` require ``` function is implicitly passed to user code, user do not need to import it explicitly.

### Methods
#### require(id)
* ``` id : String ``` - module name to be loaded

load the module named 'id'

### Module Loading by ``` require ``` function
#### ``` require ``` search paths
``` require ``` function finds id module in the order of 
1. working directory
2. node_modules under the working directory
3. $HOME/node_modules



#### ``` require('id') ``` works as follows:
For each directory in search paths above,

0. If native module named 'id' exists, load it and return.
1. If id.js file exists, load it and return.
2. If a directory id exists, load it as an package and return.