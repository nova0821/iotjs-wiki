# Coding Style Guideline for C/C++

This coding standard is based on google c++ coding standard(https://google-styleguide.googlecode.com/svn/trunk/cppguide.html)


## Header Files

### #define guard
Use #define guard in all header files. `<PROJECT>_<PATH>_<FILE>_H_` format is recommended.

	#ifndef PROJECT_PATH_FILE_H_
	#define PROJECT_PATH_FILE_H_
		...
	#endif // PROJECT_PATH_FILE_H_

### Inline functions
Inline function is allowed only if it is less than 10 lines. 
	
### Parameter order
Input parameters should precede output pamameters.

## Formatting

### Line length 
maximum 80 characters in a line.
  
### Indentation
2 space indent at a time. Do not use a tab for indentation.

### Function call
Write a function call all in a line if it fits. If not, break it into multiple lines aligned with the first argument.
Do not insert spaces after open paren and before close paren.

	int value = foo(arg1, arg2, arg3);

	int value = foo(arg1,
	                arg2,
					arg3);

### Function Declaration and Definition
Use named parameters in funtion declaration.

	ReturnType FunctionName(int, char); // not allowed
	ReturnType FunctionName(int arg1, char arg2); // Use this
	
Return type should be on the same line as funtion name and parameters if it fits. If not, break between them aligned with the first argument.

	ReturnType FunctionName(int arg1,
	                        char arg2);

If even first argument does not fit in a line, write it in a new line with 4 space indent.

	ReturnType FunctionName(
		int arg1,
		char arg2);
	

The open curly brace should be at the same line. The close curly brace should be either at the same line as its open curly brace or at new line.

	ReturnType FunctionName(int arg1, char arg2){  };
	ReturnType FunctionName(int arg1, char arg2){
		...
	}
	ReturnType FunctionName(int arg1, char arg2)
	{  // not allowed
		...
	}

### Conditionals
Use a space between the if and open brace. Open brace on the same line as the if.

	if (condition) {
		...
	}

Short conditional statements may be written in a line unless it has no else part.

	if (condition) DoSomething(); // ok
	if (condition)
		DoSomething();  // ok

### Loops and Switches
Use a space between the switch and loops(for,while,do-while) and open brace. Open brace on the same line as the switch and loops.

	while (condition) {
		...
	}

Single loop body statement may be written without braces.

	while (condition) DoSomething(); // ok
	for (condition)
		DoSomething();  // ok


### Class formatting
The open curly brace should be at the same line.
Declare public, protect, and private sections in order with 1 space indent.

	class MyClass : public ParentClass {
	 public:
	  MyClass();
	  ~MyClass();

	 private:
	  void DoTheings();
	  int my_variable;
	};


## Naming

### Type names
Use UpperCamelCase for class names. No underscore.
Type names include classes, structs, typedefs, and enums. 

	Class MyClassName {
		...
	}

	typedef MyTypeName {
		...
	}
	

### Variable names
Use lower cases and underscore for variable names.

	int lower_case_variable; 

### Constant names
Use a 'k' followed by UpperCamelCase.

	#define kConstantUse

### Function names
Use UpperCamelCase for regular function names. No underscore.

### Namespace names
Use lower cases. 

### Enumerator names
Use constant style(a 'k' followed by UpperCamelCase.)

	enum MyEnum {
	  kOK = 0,                  // OK
	  kNotOK,
	  kError,
	};
	
	enum MyEnum {
	  OK = 0,                  // not allowed
	  NOT_OK,
	  ERROR,
	};




## Comments

### Comment style
Use either // or /* */ style comments. However, // style is much prefered.



# Coding Style Guideline for Javarscript

This coding standard is based on google javarscript coding standard(https://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml)
# Javarscript Language Rules

## var
Declare variable before use.

## Semicolons
Always use semicolons.

## Function Declaration in blocks
Do not declare functions within a block.

## Wrapper objects of primitive types
Do not use wrapper objects for primitive types.

## with
Do not use `with` statement.

## Modifying prototypes of builtin objects
Do not modify prototypes of builtin objects

# Javarscript Style Rules

## Naming
Use lowerCamelCase for varible names.
Use UpperCamelCase for function names.

	var myFirstVariable;
	function MyFirstFunction {
		...
	}

## Formatting
Follow C/C++ formatting above.




