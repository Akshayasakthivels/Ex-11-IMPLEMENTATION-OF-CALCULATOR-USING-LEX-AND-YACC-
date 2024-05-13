# Ex-11-IMPLEMENTATION-OF-CALCULATOR-USING-LEX-AND-YACC-
IMPLEMENTATION OF CALCULATOR USING LEX AND YACC 
# Date :
# Aim :
To implement a calculator using LEX and YACC.
# ALGORITHM
1. Start the program.
2. Write a program in the vi editor and save it with .l extension.
3. In the lex program, write the translation rules for the various mathematical functions.
4. Write a program in the vi editor and save it with .y extension.
5. Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6. Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7. Compile these with the C compiler as gcc lex.yy.c y.tab.c
8. Enter an expression as input and it is evaluated and the answer is displayed as output.
# PROGRAM
ex11.l
```
%{
#include"y.tab.h" #include<math.h>
%}
%%
([0-9]+|([0-9]*\.[0-9]+)([eE][-+]?[0-9]+)?) {yylval.dval=atof(yytext);return NUMBER;}
log |
LOG {return LOG;} In {return nLOG;} sin |
SIN {return SINE;} cos |
COS {return COS;} tan |
TAN {return TAN;} mem {return MEM;} [\t];
\$ return 0;
\n|. return yytext[0];
%%
```
ex11.y
```
%{
double memvar;
%}

%union { double dval;
}

%token <dval> NUMBER
%token <dval> MEM
%token LOG SINE nLOG COS TAN
%left '-' '+'
%left '*' '/'
%right '^'
%left LOG SINE nLOG COS TAN
 
%nonassoc UMINUS
%type <dval> expression

%%

start: statement '\n'
| start statement '\n'
;

statement: MEM '=' expression { memvar = $3; }
| expression { printf("Answer=%g\n", $1); }
;

expression: expression '+' expression {$$ = $1 + $3; }
| expression '-' expression {$$ = $1 - $3; }
| expression '*' expression {$$ = $1 * $3; }
| expression '/' expression { if ($3 == 0)
yyerror("divide by zero"); else
$$ = $1 / $3;
}
| expression '^' expression {$$ = pow($1, $3); }
;

expression: '-' expression %prec UMINUS {$$ = -$2; }
| '(' expression ')' {$$ = $2; }
| LOG expression {$$ = log($2) / log(10); }
| nLOG expression {$$ = log($2); }
| SINE expression {$$ = sin($2 * 3.14 / 180); }
| COS expression {$$ = cos($2 * 3.14 / 180); }
| TAN expression {$$ = tan($2 * 3.14 / 180); }
| NUMBER {$$ = $1; }
| MEM {$$ = memvar; }
;

%%

int main() {
printf("Enter the expression: "); yyparse();
return 0;
}
 
int yyerror(char *error) { printf("%s\n", error); return 0;
}
```
# OUTPUT
![image](https://github.com/Akshayasakthivels/Ex-11-IMPLEMENTATION-OF-CALCULATOR-USING-LEX-AND-YACC-/assets/144870561/9a154790-eda3-4c1c-b816-a673ee909a04)

# RESULT
The calculator is implemented using LEX and YACC and the output is verified.
The calculator is implemented using LEX and YACC and the output is verified.

