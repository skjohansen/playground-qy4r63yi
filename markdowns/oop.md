# Object Oriented Programming and C#

C# is a [multi paradigm](https://en.wikipedia.org/wiki/Comparison_of_multi-paradigm_programming_languages) programming language, which is used in the Microsoft .NET framework, currently (March 2020) in [version 8.0](https://docs.microsoft.com/da-dk/dotnet/csharp/language-reference/proposals/csharp-8.0/nullable-reference-types).

Object Oriented Programming (OOP) is a [programming paradigm](https://en.wikipedia.org/wiki/Programming_paradigm) which is highly used in C#.

## OOP Concepts

OOP introduces four important concepts : Encapsulation, Inheritance, Polymorphism and Abstraction.

Please read the following articles:

- [What are four basic principles of Object Oriented Programming?](https://medium.com/@cancerian0684/what-are-four-basic-principles-of-object-oriented-programming-645af8b43727)

- [How to explain object-oriented programming concepts to a 6-year-old](https://www.freecodecamp.org/news/object-oriented-programming-concepts-21bb035f7260/)

### Encapsulation

?[What is the goal of encapsulation within OOP?]
-[ ] To put your code in a capsule
-[ ] To put a special focus on a specific feature in the code
-[x] To prevent access to implementation details

Detailed optional reading on [Encapsulation in C#](https://www.tutorialspoint.com/csharp/csharp_encapsulation.htm)

Example of encapsulation

```C# runnable
using System;

namespace RectangleApplication {
   class Rectangle {
      private double length;
      private double width;
      
      public Rectangle(double length, double width){
      	this.length = length;
        this.width = width;
      }
       
      private double GetArea() {
         return length * width;
      }
       
      public void Display() {
         Console.WriteLine("Length: {0}", length);
         Console.WriteLine("Width: {0}", width);
         Console.WriteLine("Area: {0}", GetArea());
      }
   }
   
   class ExecuteRectangle {
      static void Main(string[] args) {
         Rectangle r = new Rectangle(4.5, 2);
          // You are unable to access the vaiables length and width as they are private
          // You are unable to access GetArea() as it's private
         r.Display();
      }
   }
}


```

### Inheritance

?[What is the goal of inheritance within OOP?]
-[ ] To use code without breaking the copyright
-[x] To reuse code functionality 
-[] To make sure code never dies

Detailed optional reading on [Inheritance in C#](https://www.tutorialspoint.com/csharp/csharp_inheritance.htm) https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/inheritance and [How To Do Object Oriented Programming The Right Way](https://codeburst.io/how-to-do-object-oriented-programming-the-right-way-1339c1a25286) (optional)



Example of inheritance 
```C# runnable
using System;

namespace RectangleApplication {
   class Triangle : Rectangle {     
      public Triangle(double length, double width): base(length, width){
      	type = "Triangle";
      }
       
      public override double GetArea() {
         return 0.5 * Length * Width;
      }
       
   }
   
   class Rectangle {
      double Length {protected get; private set;}
      double Width {protected get; private set;}
      protected string type = "Rectangle";
      
      public Rectangle(double length, double width){
      	Length = length;
        Width = width;
      }
       
      public virtual double GetArea() {
         return length * width;
      }
       
      public void Display() {
         Console.WriteLine($"Length {type}: {0}", length);
         Console.WriteLine($"Width {type}: {0}", width);
         Console.WriteLine($"Area {type}: {0}", GetArea());
      }
   }
   
   class ExecuteRectangle {
      static void Main(string[] args) {
         var r = new Rectangle(4.5, 2);
         r.Display();
         
         var t = new Triangle(4.5, 2);
         t.Display();
      }
   }
}


```

### Polymorphism

?[What is the goal of polymorphism within OOP?]
-[ ] Putting your code in a capsule
-[ ] Putting a special focus on a specific feature in the code
-[x] Prevents access to implementation details
-[ ] Peace & Love

Detailed reading on [Polymorphism in C#](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/polymorphism) (optional)

Example of polymorphism 

### Abstraction

?[What is the goal of abstraction within OOP?]
-[ ] Putting your code in a capsule
-[ ] Putting a special focus on a specific feature in the code
-[x] Prevents access to implementation details
-[ ] Peace & Love

Detailed reading on [Abstration in C#](https://www.geeksforgeeks.org/c-sharp-abstraction/) (optional)

Example of encapsulation

## OOP Elements

**A class is a template or blueprint from which objects will be instantiated**. It’s like the mould from which objects can be created/instantiated from. A class represents a **real life concept** such as a person, an animal, a car, a house or a football.



A class consists of a collection of states (a.k.a. **attributes** or **properties**) and **behaviours** (a.k.a. **methods**). 

An **object** is an **instance** of a **class**. The attributes of an object as stored using variables for storing data  and the behaviour/methods of an object are implemented as functions or  procedures and can be used to perform operations on the data.

https://codeburst.io/how-to-do-object-oriented-programming-the-right-way-1339c1a25286

https://brilliant.org/wiki/classes-oop/

Class

https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes

Objects

https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/objects

## Design principles

Coupling and Cohesion

https://sanaulla.info/2008/06/26/cohesion-and-coupling-two-oo-design-principles/

## 

## 