[[C]]
# Initiating an Array

The difference between arrays in C and python is that C is storing in memory each element of the array. Each value of the array is a piece of memory you are accessing. You have to be careful when using arrays not to exceed the length it was initialized with because it could return junk values from memory. 


```
int a[10] = {0,0,0,0,0,0,0,0,0,0};
```

The data type of each element needs to be the same. If you set an initialize as length 10, it needs to have 10 elements. 

You don't need to set a specific length 

```
int a[] = {1,2,3,4,5,6,7,8,9,10};
```

You can also determine specific values inside an array like so:

```
int a[15] = {0, 0, 29,0,0,0,7,0,0,29};
```

position 2 is = 29
position 6 is = 7
position 9 = 29

To make this easier to write, in case the array is large, you can do this:

```
int a[15] = {[15] = 48, [9] = 7, [2] = 29};
```

The *designator* must be a non negative number. You don't need to initialize with a set length, if you don't set it, the compiler will grab the largest designator and use that as the length but as n-1. Remember arrays have 0 indexing.

Example of not setting a specific length:

```C
int a[] = {[5] = 10, [23] = 11};
```

### You can also combine both ways of initializing

```
int c[10] = {5,1,9,[4] = 3, 7, 2}
```

## Pass by values
Functions in C are pass by values, meaning that when you call a function on a variable, you are giving a photocopy of that variable to the function. The function will modify the photocopy and when the runtime is over for the function, the photocopy is not saved. That is why you have to use the *& operator*. This gives the address of the variable to the function so that it can modify the actual value of the variable. 

# Repeat Digits Script


# Using 'sizeof' operator with arrays
This function gives you the size of an array in bytes. If a is an array has 5 integers/elements, the size of a is 20 bytes (5 * 4). 

so by doing sizeof(a)/sizeof(a[0]) you get the actual size of the array.

For this you need to understand how each data type is stored in memory. 

## Cleaning an array
You can use this same function/division to clear an array by creating a for loop that iterates over each element in the array. 


# Computing Interest
```c
#include <stdio.h>
#define NUM_RATES ((int) sizeof(value)/sizeof(value[0]))
#define INITIAL_BALANCE 100.0

int main(){
int i, low_rate, num_years, year;
double value[5];

  

printf("Enter interest rate:");

scanf("%d", &low_rate);

printf("Enter number of years");

scanf("%d", &num_years);

  

printf("\nYears");

  

for (i = 0; i < NUM_RATES; i++){

printf("%6d%%", low_rate + i);

value[i] = INITIAL_BALANCE;

}

printf("\n");

  

for (year = 1; year <= num_years; year++){

printf("%3d ", year);

for (i = 0; i < NUM_RATES; i++){

value[i] += (low_rate + i)/100.0 * value[i];

printf("%7.2f", value[i]);

}

printf("\n");

}

return 0;

}
```

### Notes on this script

we define a macro preprocessor macro/symbolic constant, that stores the size of an array:
`#define NUM_RATES ((int) sizeof(value)/sizeof(value[0]))`

- A preprocessor macro/symbolic constant deletes 'NUM_RATES' anywhere in the script and replaces it with the sizeof formula. 

The way this works is that `sizeof()` returns the size of an element in bytes. So you can get the size of 1 element and then the size of the entire array, by dividing these 2 you get the length. 

value[5]; is declared, this will create the array with 5 0s available for us to insert any value we want. 

We use `scanf("%d", &low_rate);` as `input()` in python to store the low_rate and num_years variables.
- Remember, if we don't place the &, we don't access the value in memory 

Then we have our first for loop. Here we store the interest rates inside the array. Adding 1 to each iteration of the interest rate. Depending on the size of the arrays is that amount of interest rates that will be calculated. 

```c
// storing values in array

for (i = 0; i < NUM_RATES; i++){

printf("%6d%%", low_rate + i);

value[i] = INITIAL_BALANCE;

}

printf("\n");
```


The next for loop - a nested for loop, generates the number of years depending on the value entered in the variable num_years and then on the second - inside loop we calculate the interest rate for each year. Each iteration of the outer loop is 1 year. Then we calculate the interest rate with:

```C
for (i = 0; i < NUM_RATES; i++){
	value[i] += (low_rate + i)/100.0 * value[i];
	printf("%7.2f", value[i]);
}
```


# Multidimensional Arrays

`int m[i][j];`

order of initialization -> `int m[rows][cols]`

How the computer stores a multidimensional array in memory -> 'Row major order'
![[Pasted image 20260210190238.png]]

you can initialize a multidimensional array by declaring a nested array:

```c
int m[5][9] = {{1,1,1,....},
				{1,1,1,0,.....}}
```


There's fast ways of declaring arrays, you can skip the outer braces, but this can be risky. Similar to 1 dimension arrays you can declare some elements in the array, like so:

`double ident[2][2] = {[0][0] = 1.0, [1][1] = 2.0}`

Anything that is not declared will be defined as 0 

if you start the declaration of an array with the word 'const' you make it constant:

`const char hex_chars[] = {}`


# VLA - Variable Length Array 


# C versions 
While I was reading my book, it kept mentioning C99, I searched the web about this and discovered that C upgrades around each decade, compared to python that gets a new version each year. The version that is used does not depend on what you install but the 