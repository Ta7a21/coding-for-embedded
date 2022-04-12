# Chapter 1: Language Structure Traps
## Presentation traps
1. Use typedef instead of macros for defining new types
```c
#define PTR_CHAR char * /* Not compliant */

typedef char * pchar; /* Compliant */
```
2. Initialize all or none elements in arrays (By default, other non-initialized elements gets zero value)
```c
int arr[3] = {1}; /* Not compliant */

int arr[3] = {1 ,2, 3}; /* Compliant */
```
3. Specify data types while using static keyword (By default, static variables are integers)
```c
static x; /* Not compliant */

static int x; /* Compliant */
```
4. Initialize variables before using it
```c
int x;
fun(x); /* Not compliant */

int x = 0; /* Compliant */
fun(x);
```
5. Initialize all variables if they are on the same line
```c
int x, y = 0; /* Not compliant */

int x = 0, y = 0; /* Compliant */
```
6. Seperate each variable in a new line
```c
int x = 2, y = 0; /* Not compliant */

int x = 2;
int y = 0; /* Compliant */
```
7. Limit the usage of post/pre increment/decrement specially within lines
```c
int x = y++; /* Not compliant */

int x = y;
y = y + 1; /* Compliant */
```
8. Use curly braces to specify scopes
```c
if(x == 1)
    if(y == 0)
else /* Not compliant */

if(x == 1)
{
    if(y == 0)
    {

    }
}
else
{

} /* Compliant */
```
9. Take care of indentation
```c
if(x == 1)
    x++;
    y = 0; /* Not compliant */

if(x == 1){
    x++;
}
y = 0; /* Compliant */
```
10. Standardize naming rules
```c
int mx; /* Not compliant */

int maximumValue; /* Compliant */
```
11. Don't depend on C implicit types and defaults(By default, functions' return-type is an integer)
```c
fun(x, y){

} /* Not compliant */

int fun(x, y){

} /* Compliant */
```
12. Limit the usage of macros and comma operators

## Lexical traps
1. Specify logical operands for logical operators
```c
if(x || y) /* Not compliant */

if (x == 1 || y == 1) /* Compliant */
```
2. Use brackets and spaces in operations
```c
x=y/a+b; /* Not compliant */

x = y / (a + b) /* Compliant */
```
3. Don't rely on C default types (Real numbers are double by default and integer numbers are signed int)
```c
float x = 0.7
if(x == 0.7) /* Not compliant */

if(x == (float)0.7) /* Compliant */
```
4. Limit the usage of assignment operators
```c
x+=1; /* Not compliant */

x = x + 1; /* Compliant */
```
5. Don't rely on precedence rules
```c
x=y*a/b+z /* Not compliant */

x = (y * a) / (b + z); /* Compliant */
```

## Syntactic traps
1. Avoid multiple affectation
```c
Q[i] = C = getchar(); /* Not compliant */

C = getchar();
Q[i] = C; /* Compliant */ 
``` 
2. Don't rely on precedence rules
3. Limit the usage of post/pre increment/decrement specially within lines
4. Avoid abusive syntax
```c
for(;i--; x[i] = 0) /* Not compliant */

for(i = 50;i == 0;--i){
    x[i] = 0;
} /* Compliant */
```
5. Avoid declaring variables inside the switch-case scope
```c
switch(a)
{
    int var = 1; /* Not compliant */
    case 1: x = var;
}

int var = 1; /* Compliant */
switch(a)
{
    case 1: x = var;
}
```
6. Take care of semicolon usage
```c
/* Extra semicolon */
if(x == 1); /* Not compliant */

/* Missing semicolon */
if(x == 0)
    return /* Not compliant */
x = 1;
```
7. Use the break keyword for each case in switch-case
```c
switch(a)
{
    case 'a':
    case 'e':
    case 'i':
    case 'o':
    case 'u':
        printf("Voel");
        break;
    default:
        printf("Not voel");
} /* Not compliant */

switch(a)
{
    case 'a':
        printf("Voel");
        break;
    case 'e':
        printf("Voel");
        break;
    case 'i':
        printf("Voel");
        break;
    case 'o':
        printf("Voel");
        break;
    case 'u':
        printf("Voel");
        break;
    default:
        printf("Not voel");
} /* Compliant */
```
8. Use curly braces to specify scopes
9. Use empty braces instead of empty null statements
```c
if(x == 1){

}
else; /* Not compliant */

if(x == 1){

}
else{} /* Compliant */
```

## Semantic traps
1. Use array notation with arrays, and poiner notation with pointers
2. Use casting to avoid overflow and modulo effects (Overflow affects sign, while modulo affects maximum size)
3. Take care of missing return statements
```c
fun(x){
    if(x == 1)
        return 1;
} /* Not compliant */

fun(x){
    if(x == 1)
        return 1;
    else return -1;
} /* Compliant */
```
4. Don't return an address of a local variable
```c
int *fun(){
    int x = 0;
    return &x;
} /* Not compliant */
```
5. Don't use operations within lines
```c
if(i++ < 10) /* Not compliant */
```
6. Differentiate between names in scopes
```c
int x;
int main(){
    int x = 1;
} /* Not compliant */
```
7. Don't use arithmetic operations on enums (Use enum values)
```c
enum week{Mon, Tue, Wed, Thur, Fri, Sat, Sun};
week day = 0; /* Not compliant */

week day = Mon; /* Compliant */
```

## Preprocessor traps
1. Take care of spaces in macros definition (e.g. #define f (x) ((x)-1) )
```c
#define f (x) ((x)-1) /* Not compliant */
```
2. Use brackets on macros arguments
```c
#define min(a, b) a < b ? a : b /* Not compliant */

#define min(a, b) (a) < (b) ? (a) : (b) /* Compliant */
```
3. Take care of macros' multiple evaluation of arguments
```c
#define min(a, b) a < b? a : b
min(x++,y); /* Not compliant */
```
4. Don't use macros to define new types
```c
#define PTR_CHAR char * /* Not compliant */
```
5. Use multi-lines macros in a do{ }while(0) to avoid confusion
```c
#define assert(e) if(e) printf("error") /* Not compliant */

#define assert(e) do{ if(e) printf("error") } while(0) /* Compliant */
```
6. Use brackets with macros constants
```c
#define MAX 10 + 2 /* Not compliant */

#define MAX (10 + 2) /* Compliant */
```

## Conversions
1. Operations with long double convert smaller types to long double
2. Operations with double convert smaller types to double
3. Integer promotion takes place on arithmetic operations between smaller types (int or unsigned int depends on the value size)
4. In arithmetic operations:
    * If types are different but signs are equal? convert the smaller types to bigger ones
    * if signs are different? 
        * if types are equal? convert the unsigned to signed
        * if the bigger type is unsigned? convert the smaller to unsigned and expand its size
        * if the bigger type is signed? convert the smaller to signed and expand its size
