# C Snippets from the K&R C Book

## 1.x Introduction

### 1.1 The Beginning

Hello, World in C
```c
#include <stdio.h>

main() 
{
  printf("hello, world\n");
}
```
### 1.2 Arithmetic

Doing some simple arithmetic, also note % arguments (such as %d for integer)
```c
#include <stdio.h>

// Prints Fahrenheit-Celcius table
main()
{
  int fahr, celsius;
  int lower, upper, step;
  
  lower = 0;
  upper = 300;
  step = 20;
  
  fahr = lower;
  while (fahr <= upper) {
    celsius = 5 * (fahr-32) / 9;
    printf("%d\t%d\n", fahr, celsius);
    fahr = fahr + step;
  }
}
```
With floating point values instead
```c
#include <stdio.h>

main()
{
  float fahr, celsius;
  int lower, upper, step;
  
  lower = 0;
  upper = 300;
  step = 20;
  
  fahr = lower;
  while (fahr <= upper) {
    celsius = (5.0/9.0) * (fahr-32.0);
    printf("%3.0f %6.1f\n", fahr, celsius);
    fahr = fahr + step;
  }
}
```
### 1.3 For statement

We can use for loops to repeat tasks
```c
#include <stdioh.>

main()
{
  int fahr;
  
  for(fahr = 0; fahr <= 300; fahr = fahr + 30) {
    printf("%3d %6.1f\n", fahr, (5.0/9.0) * (fahr-32));
  }
}
```
### 1.4 Symbolic constants

Symbolic constants help us get rid of magic numbers
```c
#include <stdio.h>

#define LOWER 0
#define UPPER 0
#define STEP  20

main()
{
  int fahr;
  
  for(fahr = LOWER; fahr <= UPPER; fahr = fahr + STEP) {
    printf("%3d %6.1f\n", fahr, (5.0/9.0) * (fahr-32));
  }
}
```
### 1.5 Character IO

We can get basic user input and output with functions such as getchar() and putchar()
```c
#include <stdio.h>

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
This code counts the number of characters a user inputs
```c
#include <stdio.h>

main()
{
  long nc;
  
  nc = 0;
  while (getchar() != EOF) {
    ++nc;
  printf("%ld\n", nc);
}
```
We can use a double precision float for more space as well as a for loop to do the same logic
We also have an empty for loop known as a null statement because all the work is done in the loop itself
```c
#include <stdio.h>

main()
{
  double nc;
  
  for (nc = 0; getchar() != EOF; ++nc)
    ;
  printf("%.0f\n", nc);
}
```
This code counts the number of lines input
```c
#include <stdio.h>

main()
{
  int c, nl;
  
  nl = 0;
  while ((c = getchar()) != EOF) {
    if (c == '\n') {
      ++nl;
    }
  printf("%d\n", nl);
}
```
This code will count words, lines, and characters all at once
Also introduces the || and && logic operators as well as an else if statement
```c
#include <stdio.h>

#define IN  0
#define OUT 0

main()
{
  int c, nl, nw, nc, state;
  
  state = OUT;
  nl = nw = nc = 0;
  while ((c = getchar()) != EOF) {
    ++nc;
    if (c == '\n')
      ++nl;
    if (c == ' ' || c == '\n' || c == '\t')
      state = OUT;
    else if (state == OUT) {
      state = IN;
      ++nw;
    }
  }
  printf("%d %d %d\n", nl, nw, nc);
}
```
### 1.6 Arrays

Instead of using individual variables to count occurences of values, using an array to hold
values can be much more efficient and logical
```c
#include <stdio.h>

main()
{
    int c, i, nwhite, nother;
    int ndigit[10];

    nwhite = nother = 0;
    for (i = 0; i < 10; i++)
        ndigit[i] = 0;

    while ((c = getchar()) != EOF)
        if (c >= '0' && c <= '9')
        ++ndigit[c-'0'];
        else if (c == ' ' || c == '\n' || c == '\t')
            ++nwhite;
        else
            ++nother;

        printf("digits = ");
        for (i = 0; i < 10; i++)
            printf(" %d", ndigit[i]);
        printf(", white space = %d, other = %d", nwhite, nother);
}
```
This program prints out a histogram representation of the length of words input
```c
#include <stdio.h>

main()
{
    int c;
    int words = 1;
    int newWord = 0;
    int len = 0;

    while ((c = getchar()) != EOF)
    {
        if (c == '\n')
        {
            printf(" ");
            for (int i = 0; i < len; i++)
                printf("|");
            len = 0;
        }
        if (c != ' ')
            ++len;
        putchar(c);
        if (c == ' ')
        {
            ++words;
            newWord = 1;
            for (int i = 0; i < len; i++)
                printf("|");
            printf("\n");
            len = 0;
        }
    }
}
```
This program takes input and prints a frequency histogram of all characters
```c
#include <stdio.h>

main()
{
    int characters[127];
    int c;

    for (int i = 0; i < 127; i++)
    {
        characters[i] = 0;
    }

    while ((c = getchar()) != EOF)
    {
        ++characters[c];
    }
    for (int i = 0; i < 127; i++)
    {
        printf("%c ", i);
        for (int j = 0; j < characters[i]; j++)
        {
            printf("|");
        }
        printf("\n");
    }
}
```
### 1.7 Functions

A function can be thought of as a subroutine. It is an encapsulation of work to be done
someplace else, and helps to provide cleaner code and makes larger programs easier to manage

Here is an example of a custom made power() function which raises a number m to the nth power
```c
#include <stdio.h>

int power(int m, int n); // This is a function prototype

main()
{
    int i;

    for (i = 0; i < 10; ++i)
        printf("%d %d %d\n", i, power(2, i), power(-3, i));
    return 0; // Returning 0 in main implies a normal end of execution
}

int power(int base, int n)
{
    int i, p;

    p = 1;
    for (i = 1; i <= n; ++i)
        p = p * base;
    return p;
}
```

Here is the 1.2 section now using a function instead
```c
#include <stdio.h>

int converter(int lower, int upper, int step);

main()
{
    converter(0, 300, 20);
    return 0;
}

int converter(int lower, int upper, int step)
{
    float fahr, celsius;
    fahr = lower;
    while (fahr <= upper)
    {
        celsius = (5.0/9.0) * (fahr-32.0);
        printf("%3.0f %6.1f\n", fahr, celsius);
        fahr = fahr + step;
    }
    return 0;
}
```
### 1.8 Call by value

All function arguments are passed by value, not reference unless using a pointer.
This means that when passing a value to a function the value passed is actually a copy of the original
value; the original value will not actually change when interacted with inside the function - only the temporary copy.

This is not the case for arrays, however
```c
int power(int base, int n)
{
  int p;
  
  for (p = 1; n > 0; --n)
    p = p * base;
   return p;
}
```
### 1.9 Character arrays
