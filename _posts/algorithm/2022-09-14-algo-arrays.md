---
layout: post
title: test
category: algorithm
tags: algorithm
sitemap: false
---
# [Java] Arrays

Chapter: Section 7

```java
public class SingleDimensionArray{
  int arr[] = null;

  public SingleDimensionArray(int sizeOfArray){
    arr = new int[sizeOfArray];
    for(int i = 0; i<arr.length; i++){
      arr[i] = Integer.MIN_VALUE;
    }
  }

//insert
  public void insert(int location, int valueToBeInserted){
    try{
      if (arr[location] == Integer.MIN_VALUE){
        arr[location] = valueToBeInserted;
        System.out.println("Successfully inserted");
      } else{
        System.out.println("This cell is already occupied");
      }
    }catch (ArrayIndexOutOfBoundsException e){
      System.out.println("Invalid index to access array!");
    }
  }

//traverse
  public void traverseArray(){
    try{
      for(int i = 0; i < arr.length; i++){
        System.out.print(arr[i] + " ");
      }
    }catch (Exception e){
      System.out.println("Array no longer exists!");
    }
  }

//search
  public void searchInArray(int valueToSearch){
    for(int i = 0; i<arr.length; i++){
      if(arr[i] == valueToSearch){
        System.out.println("Value is found at the index of " + i);
        return;
      }
    }
    System.out.println(valueToSearch + " is not found");
  }

//delete
	public void deleteValue(int valueToDeleteIndex){
	    try{
	      arr[valueToDeleteIndex] = Integer.MIN_VALUE;
	      System.out.println("The value has been delete successfully");
	    }catch (ArrayIndexOutOfBoundsException e){
	      System.out.println("The delete index is not in the array");
	    }
	  }
}
```