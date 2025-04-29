# Ex-4-LETTER-FOLLOWED-BY-ANY-NUMBER-OF-LETTERS-OR-DIGITS-USING-YACC

## RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC

## Name: V Mythili
## Reg no: 212223040123
## Date: 29-04-25

# Aim:
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.
# PROGRAM:

## variable_test.l file:
```
%{
#include "y.tab.h"
#include <stdio.h>
%}

%%

"int"           { return INT; }
"float"         { return FLOAT; }
"double"        { return DOUBLE; }

[a-zA-Z_][a-zA-Z0-9_]* {
    printf("Identifier is: %s\n", yytext);
    return ID;
}

[ \t]           { /* ignore whitespace */ }

\n              { return '\n'; }

.               { return yytext[0]; }

%%

int yywrap() {
    return 1;
}
```

## variable_test.y file:

```
%{
#include <stdio.h>

/* This YACC program is for recognizing variable declarations */
void yyerror(const char *s);
int yylex(void);
%}

%token ID INT FLOAT DOUBLE

%%

D: T L '\n'         { printf("Valid declaration.\n"); }
 ;

L: L ',' ID         { /* multiple identifiers */ }
 | ID               { /* single identifier */ }
 ;

T: INT              { printf("Type: int\n"); }
 | FLOAT            { printf("Type: float\n"); }
 | DOUBLE           { printf("Type: double\n"); }
 ;

%%

extern FILE *yyin;

int main() {
    printf("Enter a declaration:\n");
    yyparse();
    return 0;
}

void yyerror(const char *s) {
    fprintf(stderr, "Error: %s\n", s);
}

```


# Output:

![image](https://github.com/user-attachments/assets/6bb68461-f9d0-4b07-b031-83a74ed814a2)


# Result
A YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.
