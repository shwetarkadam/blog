---
title: "Today I learnt: Interesting Things in Java 11"
date: 2022-11-20T15:34:30-04:00
categories:
  - Java11
  - New Features
tags:
  - primitives
  - java
  - Liquibase
  - Arrays
  - Arrays.asList
  - var in java
  - blog
published: true
comments: true
header:
  teaser: "/assets/images/java-word-cloud.png"
author_profile: true

---
![Test out the code snippets!](/assets/images/java-word-cloud.png)

I came across a fascinating Java talk on youtube by Devoxx 2022 Hanno Embregts. 
This article is about a few java snippets I encountered. The purpose of today's TIL is to have a list of interesting things we could do in Java and not deep dive into each concept.

Today's TIL : **Crazy things to do with Java 11+**

## Initializing Array and var keyword 

Having the ~var~ keyword in a statically typed language such as Java was fascinating in itself(an article on this in the future :). But we never thought we would use it to initialize such as

```
var element =new int[2];       //WORKS
var [] element=new int[2];      // COMPILE ERROR :error: 'var' is not allowed as an element type of an array
```
Since var is a generic element type, giving it array [] provides an error since rather than being generic we are giving it an array type.

## C style Array 
What is a c style array?
Java supports providing [] before and after the variable name in an array 
```
 int []arr=new int[2];
 int arr1[]=new int[2];
```
In C style array, we provide [] after the variable name that is ~int arr1[].
 

So in Java, suppose we have the following code: 
```
       int arr1[],arr2;
       arr1=new int[1];
       arr2=new int[1];        //COMPILE ERROR : error: incompatible types: int[] cannot be converted to int
```
The above code will result in COMPILE ERROR for arr2 since arr2 is not an array but a primitive int variable.
But if we want to want both arr1 and arr12 as array type we need to change the declaration to 
```
       int [] arr1,arr2; //Notice how [] are 
       arr1=new int[1];
       arr2=new int[1];      
```

       
## Arrays.asList and Primitives 

Let's look at the following example :
``` 
String [] strArr={"one","two","three"};
var stringList= Arrays.asList(strArr);

int [] intArray = {1,2,3};
var intList = Arrays.asList(intArray);

System.out.println(stringList.contains("one")+" ");
System.out.print(intList.contains(1));

```
Output: true false

Signature of Arrays.asList is var-args or List of T's.
```
      public static <T> List<T> asList(T... a)
 
```
T is of generic type so that means it needs to reference a Type such as Integer,Float and not reference Array of Ints

But next question is Can they boxed ? (Autoboxing: Converting primitive to Class Type example : int -> Integer)
Answer is no 
Array of ints -> Cannot be boxed -> Array of Integer 
##### Don't use Arrays.asList on primitives


## No structural changes allowed in Array 

```
String [] ints ={"a","b","c",null};
List<String> strings= Arrays.asList(ints);
strings.removeIf(Objects :: isNull);
System.out.println(strings.size());
```
 
Output:
Exception in thread "main" java.lang.UnsupportedOperationException: remove
at java.base/java.util.Iterator.remove(Iterator.java:102)


 Because the array does not allow any structural changes to it 

## A Unique way to remove null values from Map

```
 
Map<Integer,String> map=new HashMap();
map.put(4,null); //currently map has key:4 value: null
System.out.println(map.getOrDefault(4,"four"));
map.putIfAbsent(4,"four");     //key key:4 value:four
System.out.println(map.get(4));

```

Output: null,four

## 
```
var numbers = List.of(-1,0,1);
Map<Integer,List<Integer>> map=new HashMap<>();
numbers.forEach(number-> map.putIfAbsent(number,new ArrayList<>())
               .add(number));
System.out.println(map.get(0));

```

Output:
NullPointerException: Exception in thread "main" java.lang.NullPointerException
at HelloWorld.lambda$main$0(HelloWorld.java:33)

Because map.putIfAbsent returns null if no value is present 


