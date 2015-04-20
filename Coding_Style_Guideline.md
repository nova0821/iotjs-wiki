# Coding Style Guideline for C/C++

This coding standard follows google c++ coding standard(https://google-styleguide.googlecode.com/svn/trunk/cppguide.html) with few exceptions.

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

### Funtion names
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