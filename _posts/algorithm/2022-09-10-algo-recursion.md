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