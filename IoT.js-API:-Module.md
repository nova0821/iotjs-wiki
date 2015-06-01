## Module 
``` module ``` implements ``` require ``` function. 
Since ``` require ``` function is implicitly passed to user code, user do not need to import it explicitly.

### Methods
#### require(id)
* ``` id : String ``` - module name to be loaded

load the module named 'id'

### Module Loading by ``` require ``` function
``` require('foo') ``` works as follows:

0. If native module named 'foo' exists, load it and return.
1. If foo.js file exists, load it and return.
2. If a directory foo exists, load it as an package and return.