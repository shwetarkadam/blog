---
title: "How constructors work in Java"
date: 2021-06-14T15:34:30-04:00
categories:
  - Java
  - Concepts
  - programming
tags:
  - constructors
  - Java
  - Programming
  - concepts
published: true
comments: true
author_profile: true
#header:
  #teaser: "/assets/images/Screenshot_20220118-232720__01__01.jpg"
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"
---

<audio controls>
  <source src="/assets/audio/constructors.mp3" type="audio/mp3">
</audio>
 
Constructors are used every time to initialize instance variables. There are some additional rules associated with constructors that are often asked in interviews.Hence revising those here through a blog post.

#### 1.A constructor is used to initialize instance variables.

#### 2.When an object of an class is created,JVM goes to the class and searches for that matching constructor.
#### If Constructor is NOT PRESENT it gives a compile error.

#### 3.By default every class has a constructor called  default no argument constructor
```
class A{
A(){ //default no arg constructor 
}}
```

#### 4.A programmer can have multiple constructors in a class provided their signatures are different this is called constructor overloading.
```
class A{
A(){
//some code
}

A(int x){
//some code
}

A(float x){
//some code
}

A(float x,int y){
//some code
}
A(int x,float y){
}
A(int z){}//THIS WILL GIVE COMPILE ERROR SInce its already defined on top.

}

A a=new A();
new A();//goes to first matching constructor

```

#### 5.JVM always calls the matching constructor from the class.HOWEVER,a programmer can call other constructors of this class by using the the this() method
```
class A{
A(){
System.out.println("A");    //I 
A(int x){
this();                     //this will go to constructor A();
System.out.println("AA");   //II
}
}
class App{
public static void main(String[]args){
new A(5);
}}

OUTPUT:
A
AA

```

#### 6.If a programmer desires it can call the constructor of the super class as well from its own constructor using the super() method.
```
class A{
A(){
System.out.println("A");    //I 
}
}
class B extends A{
B(){
super();             //this is called implicitly refer next point also 
System.out.println("B");
}}


class HelloWorld {
    public static void main(String[] args) {
        new B();
    }
}
OUTPUT:
A
B
```

#### 7.Whenever a programmer creates a constructor ,JVM writes super() in every constructor implicitly as its first line.

Note:If a class does not extend any class it by default extends the Object class.
Do Try this code in your ide to see it for yourself
```
class A{
A(){
//super will be called implicitly at the first line of this constructor and here since it does not extend any class it will extend the Object class
System.out.println("A");    //I 
}

A(int x){
//super will be called implicitly at the first line of this constructor 
System.out.println("AA");
}}


class HelloWorld {
    public static void main(String[] args) {
        new A(5);
    }
}
OUTPUT:
A
AA
```
That's all for constructors in Java. 

Happy Learning :)


