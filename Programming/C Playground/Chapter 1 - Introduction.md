[[C Programming]]

# Hello World
your program beings execution at the beginning of main - every program must have a main somewhere

the statement of a function are enclosed in {}

``` C
#include <stdio.h>

  

int main (){

printf("Hello world!\n");

return 0;

}
```

# How to compile
Using linux - using software gcc 

> [!NOTE] What is compile
> Turn your C code into machine code so that your computer can understand it and actually run it. 

# Celsius to Fahrenheit 
Things to consider when working with integers. When doing integer division the result is truncated meaning: any fractional part is discarded. 5/9 would be truncated to zero. 

```C
#include <stdio.h>

// oC=(5/9)(oF-32)

/* print Fahrenheit-Celsius table

for fahr = 0, 20, ..., 300 */

int main (){

int fahr, celsius;

int lower, upper, step;

  

lower = 0;

upper = 300;

step = 20;

  

fahr = lower;

  

while (fahr <= upper){

celsius = 5 * (fahr-32)/9;

printf("%d\t%d\n", fahr, celsius);

fahr = fahr + step;

}
}
```

## How printf() works in C
The first argument is a string of characters to be printed where each % indicates where the second, third, ... arguments will be substituted.

- %d specifies an integer argument 
- \t means tab 

the first % in a printf() is paired with the second argument, then third. They must match the data type or you will get an error.

