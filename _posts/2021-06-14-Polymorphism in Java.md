---
title: "Understanding Polymorphism in Java"
date: 2021-06-14T15:34:30-04:00
categories:
  - Java
  - Concepts
  - programming
tags:
  - polymorphism
  - polymorphic object
  - Java
  - Programming
published: true
comments: true
author_profile: true
header:
  teaser: "/assets/images/Screenshot_20220118-232720__01__01.jpg"
---

![polymorphism](/assets/images/Screenshot_20220118-232720__01__01.jpg)


Just revisiting and explaining myself Polymorphism concept here through a blog post. The words Polymorphism means multiple forms. 

In Java ,Polymorphism means ***multiple forms of an object***.
We shall divide this article into 3 sections.

1.Syntax

2.Calling a variable polymorphically.

3.Calling a method polymorphically.

### 1.Syntax

Now in polymorphism in Java, the thumb key rule to remember is 

#### super = sub

Meaning the variable reference (LHS) must always be a super class reference and the object initialization(RHS) must a sub class.

For Example:
class A{

}
class B extends A{
}              
class C extends B{
}              
class D extends A{
}              

So valid and invalid syntax according to the thumb rule will be

```
A a =new B();           //VALID
B b=new D();            //NOT VALID 
C c=new A();           //VALID
A a1=new D();           //VALID
```

### 2.Calling a variable polymorphically.
If a variable is called from a polymorphic object,we follow the *reference* i.e. the **super** class.
And if the variable is not present in the super class ,it results in a COMPILE ERROR.
EG:
```
class A{
int x=5;
}
class B extends A{
int x=10;
}
class App{
public static void main(String[]args){
A a=new B();
System.out.println(a.x); 
//What do u think is the output class A x value (5)or class B x value(10)?Follow the rule.

}
}
OUTPUT:
5
```

### Calling a method polymorphically.
 
If a method is called from a polymorphic object ,we follow a 2 step procedure:
1.We got to the super class and check whther the method is present or not.
```
if(present)
 Goto to step 2 
else
 COMPILE ERROR
```
2.Come to the sub class and check wther the method is overrided or not.
```
if(overrided)
 Call the sub-class version
else
 Call the super -class version.
```

Eg:
```
class A{
void m1(){
System.out.println("A");
}}
class B extends A{
void m1(){
System.out.println("B");
}}
class App{
public static void main(String[]args){
A a=new B();
a.m1();          //Follow the rule
B=new B();
b.m1();          //Normal sub class object method call
}}
OUTPUT:
B
B
```

So that's all for polymorphism in java.

Happy Learning :)

Image source :- me.me.com
