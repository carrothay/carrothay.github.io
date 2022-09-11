---
layout: post
title: test
category: algorithm
tags: algorithm
sitemap: false
---
# [Java] Recursion

Chapter: Section 2

## Recursion

a way of solving a prroblem by having a function calling itself

- everytime recursive method calls itself the system stores in the static memory for coming back cause there are execution statements left after calling itself(LIFO.)

### Recursion vs Iteration

- Space efficient → Iteration
    - No stack memory required
- Time efficient → Iteration
    - In case of recursion system needs more time for pop and push elements to stack memory
- Easy to code → Recursion

```java
//Recursive
static int powerOfTwo(int n){
	if(n == 0){
		return 1;
	} else {
		var power = 2 * powerOfTwo(n-1);
		return power;
	}
}
//powerOfTwo(4)
//2 4 8 16
```

```java
//Iterative
static int powerOfTwoIT(int n){
	var i = 0;
	var power = 1;
	while (i < n){
		power = power * 2;
		i = i + 1;
	}
	return power;
}
//powerOfTwoIT(4)
//2 4 8 16
```

### Recursion - Factorial

```java
class Main {
  public static void main(String[] args) {
    Main recursion = new Main();
    var rec = recursion.factorial(10);
    System.out.println(rec);
  }

  public int factorial(int n) {
    if(n < 0){ //the constraint
        return -1;
    }
    if (n==0 || n== 1){ //the stopping criterion
       return  1;
    } 
    System.out.println(n);
    return n * factorial(n-1); //the flow: n! = n * (n-1)!
  }
}

//10
//9
//8
//7
//6
//5
//4
//3
//2
//3628800
```

### Recursion - Fibonacci

- Fibonacci sequence is a sequence of numbers in which each number is the sum of the two
preceding ones and the sequence starts from 0 and 1
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89…

```java
class Main {
  public static void main(String[] args) {
    Main recursion = new Main();
    var rec = recursion.fibonacci(5);
    System.out.println(rec);
  }

  public int fibonacci(int n) {
    if(n<0){ //the constraint
      return -1;
    }
    if(n==0 || n==1){ //the stopping criterion
      return n;
    }
    return fibonacci(n-1) + fibonacci(n-2);
	//the flow: f(n) = f(n-1) f(n-2)
	//ex: 5 = 3 + 2
  }
}
//return 5
```