
# For Statement

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

## Symbolic Constants
In the program mentioned above, we have constants like 300 and 200. These are buried inside the for loop. In a larger program these numbers could be hard to troubleshoot. 

In this case it is better to store them inside variables or inside a #define line.

```
#include <stdio.h>

#define LOWER 0 /* lower limit of table */
#define UPPER 300 /* upper limit */
#define STEP 20 /* step size */


int main() {

  

int fahr;

  

for (fahr = LOWER; fahr <= UPPER; fahr = fahr + STEP)

printf("%3d %6.2f\n", fahr, (5.0/9.0)*(fahr-32));
  
}
```

Symbolic constants are not variables. When defined, they are declared in CAPS to be distinguished between that and real variables. 

Symbolic constants do not appear in declaration. This is just a text replacement. When the compiler sees STEP, it will turn it into 20 
- Declaration -> tells the compiler the name and type of something, so the compiler can know how to use it. 
- Definition -> The actual creation of the 'something'

Symbolic constants = replacements 

# Input and Output
input -> getchar()
ouput -> putchar()

*Text stream* -> A|B|C|D|E each line consists of a character 

`char` is used to store character data 

```
#include <stdio.h>

/* copy input to output; 1st version */

main()

{

int c;

c = getchar();

while (c != EOF) {

putchar(c);

c = getchar();

}

}
```

EOF -> signifies the end of the file. getchar() returns this when there is no more input. 

Important note, c must be declared as a big enough variable to hold anything that getchar() might return. We don't use char, but instead int because the variable needs to be big enough to hold EOF in addition to any possible char. 


The above script can also be written as:
```
#include <stdio.h>

/* copy input to output; 2nd version */

main()

{

int c;

while ((c = getchar()) != EOF)

putchar(c);

}
```

Here the getchar() is being performed inside the while loop and then evaulated to see if it != EOF. If this is false, it continues and sends the c value to putchar(c) to output the character

Another note, the precedence of != is higher than =, so parentheses are necessary for the c = getchar() to happen first. 

c = getchar() != EOF is equivalent to c = (getchar() != EOF)

Exercsise 1-6. Verify that the expression getchar() != EOF is 0 or 1.

