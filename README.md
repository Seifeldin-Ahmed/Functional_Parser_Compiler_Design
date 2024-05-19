# Functional_Parser_Compiler_Design


This project aims to implement a fully functional parser using C++ for a simple programming language. The parser consists of two main phases: lexical analysis (tokenization) and semantic analyzer (parsing). The lexer divides the input code into meaningful tokens and assigns them appropriate types. The parser then uses these tokens to construct a parse tree, which represents the hierarchical structure of the program.

## Project Functions

•   Read data from input.txt file: The program can read input data from a file named 
"input.txt". This file contains the code or input that needs to be processed by the 
program. 
•    Accept multiple data types: The program is capable of handling various data types, 
such as integers, floats, long long, etc. 
•    Parsing if and while statements: The program has specific support for if and while 
statements. The parser is designed to recognize and parse these control flow statements 
according to a given context-free grammar (CFG). 
•    Tokenization: Before parsing, the input code needs to be tokenized. Tokenization 
involves breaking down the code into individual tokens, such as keywords, identifiers, 
operators, numbers, and declaration keywords, punctuation and error.  
•    Generate a parse tree: After tokenization, the program follows a certain CFG to 
generate a parse tree. The parse tree represents the syntactic structure of the input code. 
•    Visualization using graphviz: The program provides a feature to visualize the generated 
parse tree using graphviz. 
•    Remove comments: The program includes a function to remove comments from the 
code. This function identifies and removes both single-line and multi-line comments while 
preserving the functionality of the parser. 

## CFG 
     stmts            ----> stmts stms | E 
     stmt             ----> while_stmt | if_stmt | assign_stmt | declaration_stmt
     declaration_stmt ----> declaration_keyword definition_stmt
     declaration_keyword--> int | char | float | double | short | long long
     definition_stmt  ----> id = expr; |
                            id;
     while_stmt       ----> while(cond){stmts}
     assign_stmt      ----> id = expr;
     if_stmt          ----> if(cond) stmt |
                            if(cond) stmt else_stmt|
                            if(cond) stmt elseif_stmt
     else_stmt        ----> else stmt 
     elseif_stmt      ----> elseif (cond) stmt elseif_stmt | else_stmt | e
     cond             ----> id op factor 
     expr             ----> expr + term | expr - term | term
     term             ----> term * factor | term / factor | factor
     factor           ----> id | digit | (expr)
     id               ----> a-z|A-Z
     digit            ----> 0|..9
     op               ----> >|>=|<|<=|=|==|!=|+|-|*|/

## CFG after left recursion left factoring elimination
     stmts            ----> stmt rest
     rest             ----> stmt rest | E
     stmt             ----> while_stmt | if_stmt | assign_stmt | declaration_stmt
     declaration_stmt ----> declaration_keyword definition_stmt
     declaration_keyword--> int | char | float | double | short | long long
     definition_stmt  ----> id rest4;
     rest4            ----> e | = expr 
     while_stmt       ----> while(cond){stmts}
     assign_stmt      ----> id = expr;
     if_stmt          ----> if(cond)stmt rest3
     rest3            ----> elseif_stmt| else_stmt | E
     else_stmt        ----> else stmt
     elseif_stmt      ----> else if (cond) stmt rest3
     cond             ----> id op factor
     expr             ----> term  Rest1
     Rest1            ----> + term Rest1 | - term Rest1 | E
     term             ----> factor Rest2
     Rest2            ----> * factor Rest2 | / factor Rest2 | E
     factor           ----> id | digit | (expr)
     id               ----> a|..|z|A|..|Z
     digit            ----> 0|..|9
     op               ---->>|>=|<|<=|=|==|!=|+|-|*|/
## Input Code Sample: 
```c++
int x = 1 ;
float y;
double temp;
while(x<3)
{
 y = 10.4;
 // z = 70;
 y = y + 3e1;
 
}
if(x==10)
  temp = 3.33;
else if(x <2)
   temp = 30;
else
   temp = 0;
```
   
## Parse Tree for this sample Code:
![parsetree](https://github.com/Seifeldin-Ahmed/Functional_Parser_Compiler_Design/assets/120275931/2e6c6de5-c2b4-4433-a094-327a06544793)
