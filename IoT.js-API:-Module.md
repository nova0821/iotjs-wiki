## Module 
``` module ``` implements ``` require ``` function. 
Since ``` require ``` function is implicitly passed to user code, user do not need to import it explicitly.

### Methods
#### require(modulename)
* ``` modulename : string ``` - module name to be loaded

load the module named 'modulename'

### Module Loading by ``` require ``` function
``` require('foo') ``` works as follows:

0. If native module named 'foo' exists, load it.
1. If foo.js file exists in candidate directory, load it.
2. If node_module/foo.js exists under candidate dir, load it.