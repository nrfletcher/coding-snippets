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
#deinfe OUT 0

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


  
