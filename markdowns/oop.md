# Object Oriented Programming and C#

C# is a [multi paradigm](https://en.wikipedia.org/wiki/Comparison_of_multi-paradigm_programming_languages) programming language, which is used in the Microsoft .NET framework, currently (March 2020) in [version 8.0](https://docs.microsoft.com/da-dk/dotnet/csharp/language-reference/proposals/csharp-8.0/nullable-reference-types).

[Object Oriented Programming](https://en.wikipedia.org/wiki/Object-oriented_programming) (OOP) is a [programming paradigm](https://en.wikipedia.org/wiki/Programming_paradigm) which is highly used in C#.

For those interesed in the history behind OOP it worth looking at these sites [Alan Kays Definition Of Object Oriented](https://wiki.c2.com/?AlanKaysDefinitionOfObjectOriented) and 
[Alan Kay and OO Programming](https://ovid.github.io/articles/alan-kay-and-oo-programming.html)

## Programming concepts in OOP

Especially four programming concepts are important to understand when programming using OOP : Encapsulation, Inheritance, Polymorphism and Abstraction. These concepts often goes hand in hand, and can be hard to seperate.

Please read the following articles:

- [What are four basic principles of Object Oriented Programming?](https://medium.com/@cancerian0684/what-are-four-basic-principles-of-object-oriented-programming-645af8b43727)

- [How to explain object-oriented programming concepts to a 6-year-old](https://www.freecodecamp.org/news/object-oriented-programming-concepts-21bb035f7260/)

### Encapsulation

?[What is the goal of encapsulation within OOP?]
-[ ] To put your code in a "capsule", to make it secure
-[ ] To put a special focus on a specific feature in the code
-[x] To bind together data and functions that manipulate the data
-[x] To keep the internal state of the object within the object 

Detailed optional reading on [OOP Concept for Beginners: What is Encapsulation](https://stackify.com/oop-concept-for-beginners-what-is-encapsulation/)

Example of encapsulation written in C#. The class Counter, have the inner state counterValue which is hidden for the outside and can only be modified by the methods CountUp and CountDown.

```C# runnable
using System;

public class Counter
{
	private int counterValue = 0;

	public void CountUp()
	{
		counterValue++;
	}

	public void CountDown()
	{
		counterValue--;
	}

	public int GetCounterValue()
	{
		return counterValue;
	}
}
   
class ExecuteEncapsulation {
	static void Main(string[] args) {
        var c = new Counter();
        Console.WriteLine(c.GetCounterValue()); //Expected 0
        c.CountUp(); // value should now be 1
        c.CountUp(); // value should now be 2
        Console.WriteLine(c.GetCounterValue()); //Expected 2
        c.CountDown(); // value should now be 1
        Console.WriteLine(c.GetCounterValue()); //Expected 1
   }
}


```

### Inheritance

?[What is the goal of inheritance within OOP?]
-[ ] To use code without breaking the copyright
-[x] To reuse code functionality 
-[] To make sure code never dies

Detailed optional reading on [Inheritance in C#](https://www.tutorialspoint.com/csharp/csharp_inheritance.htm), [Inheritance (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/inheritance) and [How To Do Object Oriented Programming The Right Way](https://codeburst.io/how-to-do-object-oriented-programming-the-right-way-1339c1a25286) (optional)

Example of inheritance, the species dog and human is inharitancing the functionality of the mammel, and modifies the two parameters legs and specie.

```C# runnable
using System;

public class Mammel
{
	private int numberOfLegs = 0;
	private string specie = string.Empty;

	public Mammel(string specie, int numberOfLegs)
	{
		this.numberOfLegs = numberOfLegs;
		this.specie = specie;
	}

	public int NumberOfLegs
	{
		get
		{
			return numberOfLegs;
		}
	}

	public string Specie
	{
		get
		{
			return specie;
		}
	}
}

public class Dog : Mammel
{
	public Dog() : base("Dogs", 4)
	{
	}
}

public class Human : Mammel
{
	public Human() : base("Humans", 2)
	{
	}
}

class ExecuteInheritance {
	static void Main(string[] args) {
        var d = new Dog();
        Console.WriteLine($"{d.Specie} has {d.NumberOfLegs} legs");

        var h = new Human();
        Console.WriteLine($"{h.Specie} has {h.NumberOfLegs} legs");
   }
}

```

### Polymorphism

?[What can you do with polymorphism within OOP?]
-[x] Function overloading
-[ ] Class overloading
-[x] Operator overloading

Detailed optional reading on [Polymorphism in C#](https://www.tutorialspoint.com/csharp/csharp_polymorphism.htm), [Polymorphism (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/polymorphism) 

Example of polymorphism, the class Polymorph implents three different (polymorph) versions of the method Print. Type of input decides which of the implementaions is excecuted.

```C# runnable
using System;

class Polymorph
{
    public void Print(int i)
    {
    	Console.WriteLine($"Printing int: {i}");
    }

    public void Print(double d)
    {
    	Console.WriteLine($"Printing double: {d}");
    }

    public void Print(string s)
    {
    	Console.WriteLine($"Printing string: {s}");
    }
}
   
class RunPolymorph {
   static void Main(string[] args) {
      var p = new Polymorph();
      p.Print(42);
      p.Print(3.14159265359);
      p.Print("I'm Polymorph");
   }
}


```


### Abstraction

?[What is the goal of abstraction within OOP?]
-[x] To only show  the essentials functionality of a class
-[ ] To make the code hard to read and understand
-[x] To hide away implementation details

Detailed optional reading on [Abstration in C#](https://www.geeksforgeeks.org/c-sharp-abstraction/), [Abstract modifier](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/abstract)

Example of abstraction, the class mammel can't be instanciated since it have the modifier *abstract*, only the class Dog and Human can be instanciated, all functionality data which is generic for mammels are hidden in the Mammel class.

```C# runnable
using System;

public abstract class Mammel
{
	private int numberOfLegs = 0;
	private string specie = string.Empty;

	public Mammel(string specie, int numberOfLegs)
	{
		this.numberOfLegs = numberOfLegs;
		this.specie = specie;
	}

	public int NumberOfLegs
	{
		get
		{
			return numberOfLegs;
		}
	}

	public string Specie
	{
		get
		{
			return specie;
		}
	}

	public abstract void MakeASound();
}

public class Dog : Mammel
{
	public Dog() : base("Dogs", 4)
	{
	}

	public override void MakeASound()
	{
		Console.WriteLine("Wuf");
	}
}

public class Human : Mammel
{
	public Human() : base("Humans", 2)
	{
	}

	public override void MakeASound()
	{
		Console.WriteLine("Hello World");
	}
}

class ExecuteAbstraction{
	static void Main(string[] args) {
        var d = new Dog();
        Console.WriteLine($"{d.Specie} has {d.NumberOfLegs} legs");
        Console.Write("The dog say: ");
        d.MakeASound();

        var h = new Human();
        Console.WriteLine($"{h.Specie} has {h.NumberOfLegs} legs");
        Console.Write("The human say: ");
        h.MakeASound();
   }
}

```

## OOP Elements

Objects are instances of classes. In other words, an instance of a class is an object defined by that particular class. Creating a new instance, or an object, is called instantiation.

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

## Object oriented thinking
CRC cards
http://c2.com/doc/oopsla89/paper.html
## 