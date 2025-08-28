
for loop statement

code used here:

```c
#include <stdio.h>

/* print Fahrenheit-Celsius table */

  
  

main() {

int fahr;

for (fahr = 0; fahr <= 300; fahr = fahr + 20)

printf("%3d %6.1f\n", fahr, (5.0/9.0) * (fahr-32));

}
```

One difference between this script and the previous converter [/Programming/C Playground/Chapter 1 - Introduction.md] is that we are doing the operation in the printf command. Since we declared a decimal (%6.1f) we can place here any operation that yields the decimal result 


the for has 3 parts:
1) the initialization where we declare fahr varible = 0 
2) fahr <= controls the loop, if it's true it will continue the loop. 
3) the incremental step is then performed 

## for vs while
It depends on context, but the for is used then the inizialisation and step functions are related and single statements 