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
-[ ] Putting your code in a capsule
-[ ] Putting a special focus on a specific feature in the code
-[x] Prevents access to implementation details

Detailed reading on [Encapsulation in C#](https://www.tutorialspoint.com/csharp/csharp_encapsulation.htm) (optional)

Example of encapsulation

``` c# runnable
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
          // You are unable to access GetArea() as it's private
         r.Display();
      }
   }
}

```

### Inheritance

?[What is the goal of inheritance within OOP?]
-[ ] Putting your code in a capsule
-[ ] Putting a special focus on a specific feature in the code
-[x] Prevents access to implementation details
-[ ] Peace & Love

Detailed reading on [Inheritance in C#](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/inheritance) (optional)

https://codeburst.io/how-to-do-object-oriented-programming-the-right-way-1339c1a25286

Example of inheritance 

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

https://codeburst.io/how-to-do-object-oriented-programming-the-right-way-1339c1a25286

Class

Objects

## Design principles

Coupling and Cohesion

https://sanaulla.info/2008/06/26/cohesion-and-coupling-two-oo-design-principles/

## 

## 