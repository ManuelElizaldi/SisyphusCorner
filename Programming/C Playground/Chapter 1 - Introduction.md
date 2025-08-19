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

# Working with floats
Improvements could have been made to the previous script. Integers are not as accurate when dealing with temperatures, so we have to use floats. 

Same as before we declare the variables before using them, but now we declare them as floats.

here's the script

```c
#include <stdio.h>
/* print Fahrenheit-Celsius table
for fahr = 0, 20, ..., 300; floating-point version */
main()
{
float fahr, celsius;
float lower, upper, step;
lower = 0;
upper = 300;
step = 20;
}
/* lower limit of temperatuire scale */
/* upper limit */
/* step size */
fahr = lower;
while (fahr <= upper) {
celsius = (5.0/9.0) * (fahr-32.0);
printf("%3.0f %6.1f\n", fahr, celsius);
fahr = fahr + step;
}
```

Since now we are working with floats and they wont get truncated, we can create a better formula that uses 5/9, note that they are defined as 5.0 (decimal). If the operation has ONLY integer operands, the result will be an integer, but if it has an integer and a float, the integer will be converted into a float. 

Nevertheless it is recommended to write floats if you are working with floats for the benefit of other readers. - best practice

Here's the specifications on how to print floats and integers 
![[Pasted image 20250811171513.png]]

## Celsius to Fahrenheit 
```c
#include <stdio.h>

  

int main(){

float fahr, celsius;

float lower, upper, step;

  

lower = 0;

upper = 300;

step = 20;

  

celsius = lower;

  

printf("Celsius Fahrenheit\n");

  

while (celsius <= upper) {

fahr = (celsius * 1.8) + 32;

printf("%6.2f\t %6.2f\n", celsius, fahr);

celsius = celsius + step;

}

}
```
