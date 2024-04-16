Converts the source language into target language
Interpreter - Directly executes the source program with input

Why does Most of the Compilers' target language is Assembly language (compared to object code):
1. Easier to produce as output
2. Easier to debug

Source-to-Source Translator : High Level Language to High Level Language

Advantages of C language being a target language:
1. Portability - Runs on various platforms
2. Low-level control - Direct Hardware Access
3. Efficient - Fast & Memory Efficient (possible to run some low level optimal subroutines)
4. Legacy Compatibility

Difference between Compiler and Interpreter:

| Compiler| Interpreter|
|--------------------------------------------|-----------------------------|
|Source Language$\rightarrow$Target Language|Source Language + Input $\rightarrow$ Output|
|Faster at Mapping Inputs to Outputs|Better Error Diagnostics|

Just In Time Compiler (JIT):
Java first compiles the code into a bytecode which is then interpreted by a Java Virtual Machine (JVM)
Benefit is bytecode can be now shared and read by any JVM

Process for running a code:
1. Preprocessor -
	Collect source code from various files and expand macros
2. Compiler
3. Assembler -
	Assembly language $\rightarrow$ Machine Code
4. Linker -
	Resolves the external memory addresses when the machine code is spread across different places
5. Loader -
	Loads the machine code from machine to execution

![[Pasted image 20240124135013.png]]
<h1>Structure of Compiler</h1>
<h4>1. Front end (Analysis)</h4>
Breaks up the source program into different logical pieces and connects them according to a Grammatical structure (<i>Syntax Tree</i>)
Creates a <i>Symbol Table</i> which stores the details of the variables
Optimises some of the code present
If the source program is ill-syntaxed, then it provides suitable error messages
Creates an intermediate representation of the source program

<h4>2. Synthesis</h4>
The intermediate representation is then fit to the according machine details and target program is created

<h4>Phases of Compilers</h4>
![[Pasted image 20240124135056.png]]

Symbol Table is used by all compiler phases

Suppose we are given the following code to compile:
```
position = initial + rate * 60
```

<h4>Lexical Analysis</h4>
Also known as scanning
It will group the characters into <i>lexemes</i> which are converted into tokens

Token format is as follows: ```<token_name,attribute_value>```
Token name is some arbitrary name (or identifier/keyword) which is used in syntax analysis
Operators need no attribute value
Attribute Value is the index of the token in the symbol table

So to convert the above code:
```<id,1> <=> <id,2> <+> <id,3> <*> <60>```

<h4>Syntax Analysis</h4>
Also known as parsing
Creates a syntax tree using the token names

Structure of the syntax tree:
1. Root - Operator
2. Children - operands/operators
3. Leaves - operands
4. Non-terminal nodes - operators

We can use different types of grammers (like CFG) to optimise the preparation of the tree
![[Pasted image 20240124135139.png]]
<h4>Semantic Analysis</h4>
Checks the semantic consistency using syntax tree and symbol table
Performs Type Checking and Type Casting
If problem, throw error

Here, we assume that the language provides a freedom to multiply int and float, so we have to do a type casting first
![[Pasted image 20240124135200.png]]
<h4>Intermediate Code Generation</h4>
No fixed format
Can be thought of as a pseudocode of the target code (not of the source code!)
Should be easy to produce and easy to translate into the target language

<h5>Three Address Code</h5>
Each line in the intermediate code has atmost three 

# Lexer (Lex Language)

Used to identify tokens from a stream of characters
Creates a C code (<file_name>.yy.c)

Syntax :
```
%{
	/* Definition section (C code) */
	/* Used to define any variables */
	/* Directly added to the final C code */
	/* We can add C code by one space indenting */
}%
%%

/* Rules Section */
/* UNIX RegEx pattern given on the left, Action on the right
Lexer recognizes the pattern and executes the action
yytext is a special array which contains the text that matched the pattern
*/
[\t \n ]+ ;
if   |
else |
for  |
while| { printf("Keyword : %s\n",yytext);}
%%

/* User Subroutines Section */
/* Contains any legal C code which is copied to the final C code
Lexer produced by lex is a C routine called yylex()
Returns only when actions return and after the processing of the entire input
*/
main() {
	yylex();
}
```

##### Symbol Table
We dynamically allocate words into a symbol table where the variable name and its properties are stored.
The Symbol Table is used in the rules section to make any actions

Algorithm:
Parsing and Stack
```
1. set ip to the first symbol of w;
2. set x to the top symbol of the stack
3. while(w!=b) { // stack not empty
	1. if(x is a) {
		1. pop the stack and advance ip
	2. }
	3. else if(x is a terminal) {
		1. error();
	4. }
	5. else if(M[x,a] = X => Y1Y2...Yk) {
		1. output the production X => Y1Y2...Yk
		2. pop the stack
		3. push Y1Y2..Yk onto the stack with Y1 on the top
	6. }
	7. set X to the top symbol of stack
6.}
```

Parsing Table

Sentences - string of terminals derived from a grammer

Sentential Form - string of terminals & non terminals derived from a grammer

Rightmost derivation - sentences derived by opening the rightmost non-terminal first

Right Sentential Form - sentential form that occurs in the rightmost derivation of some sentence

Viable Prefix - Prefixes of right sentential forms that appear in the stack



