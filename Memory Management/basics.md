# Memory Management

## Call Stack

stacking items one top of another.

Insert on top always
Remove from the top always

Last in first out ("LIFO" principle)

how function will behave in call stack

example 1:
![alt text](basicsimg/image.png)
![alt text](basicsimg/image-1.png)

Example 2:
![alt text](basicsimg/image-2.png)

Example 3:
![alt text](basicsimg/image-3.png)
![alt text](basicsimg/image-4.png)

it will be helpfull in recursion

## What is Reference Variable?

a = 10

a (Reference Variable) 
    => row1 col3 (Address)
        => 10 (Valure is stored)

## Types of memory in Java

### Premitive Data Types
    byte , sort, int(0), long, float(0.0), double, char(null), boolean(false), 

### Stack memory:
    All the premitive data types & 
    Refernce variables (a = row1 col2).
    are stored here.

### Heap memory
    Content of the 'Reference Variables' called 'Objects' are stored here.

Example1: ![alt text](basicsimg/image-5.png)

Example2: ![alt text](basicsimg/image-6.png)

Example3: ![alt text](basicsimg/image-7.png)
    Type of Mark and Swipe algo works in Garbage collector
    It Try to mark it if not able to mark, swipe it from memory
    Note: there is no Garbage collecter in C++, we have to remove it form memory (otherwise memory fills it is called 'Memory Leaks')
    
```java
In Java it is always pass by value
premitive data type: copy of value (Can't Modify Original)
Objects: copy of reference location (Can Modify Original)
Pass by Value: sharing same variable accorss different level of stack
```

```python
Imutable: int, str, tuple
Mutable: list, dict 
```

Example3: ![alt text](basicsimg/image-8.png)
Example4: ![alt text](basicsimg/image-9.png)
Example5: ![alt text](basicsimg/image-10.png)

```java
System.out.println(mat.toString());
// Equivalent to: ClassName@HashCode
```
```python
print(mat.__str__())  
# Equivalent to: [ [5, 0, 0], [25, 0, 0] ]

#__str__() called special methods in python
```

Example6: ![alt text](basicsimg/image-11.png)
Example7: ![alt text](basicsimg/image-12.png)

quiz1: ![alt text](basicsimg/image-13.png)
quiz2: ![alt text](basicsimg/image-14.png)
quiz3: ![alt text](basicsimg/image-15.png)
quiz4: ![alt text](basicsimg/image-16.png)
quiz5: ![alt text](basicsimg/image-17.png)
quiz6: ![alt text](basicsimg/image-18.png)
quiz7: ![alt text](basicsimg/image-19.png)

## how arrays are stored
how arrays are stored in heap & stack memory

