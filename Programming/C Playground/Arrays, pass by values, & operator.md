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

The designator must be a non negative number. You don't need to initialize with a set length, if you don't set it, the compiler will grab the largest designator and use that as the length but as n-1. Remember arrays have 0 indexing  

### You can also combine both ways of initializing

```
int c[10] = {5,1,9,[4] = 3, 7, 2}
```

## Pass by values
Functions in C are pass by values, meaning that when you call a function on a variable, you are giving a photocopy of that variable to the function. The function will modify the photocopy and when the runtime is over for the function, the photocopy is not saved. That is why you have to use the *& operator*. This gives the address of the variable to the function so that it can modify the actual value of the variable. 

