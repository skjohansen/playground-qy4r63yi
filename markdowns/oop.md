# Object Oriented Programming and C#

C# is a [multi paradigm](https://en.wikipedia.org/wiki/Comparison_of_multi-paradigm_programming_languages) programming language, which is used in the Microsoft .NET framework, currently (March 2021) the latest version is [version 9.0](https://stackoverflow.com/questions/247621/what-are-the-correct-version-numbers-for-c).

[Object Oriented Programming](https://en.wikipedia.org/wiki/Object-oriented_programming) (OOP) is a [programming paradigm](https://en.wikipedia.org/wiki/Programming_paradigm) which is highly used in C#.

## The definition of OOP

> Objects are simply experts. You tell them what you need and they get it done. Forget all of the handwaving about blueprints or "data with behaviors". Those are implementation details. And once you start thinking about objects as simply experts about a particular problem domain, OOP becomes much easier.
>
> Quote from:  [Alan Kay and OO Programming](https://ovid.github.io/articles/alan-kay-and-oo-programming.html)

It's **important** note that there is kind of a gap between the original definition of Object Oriented Programming [keyed by Alan Kays](https://wiki.c2.com/?AlanKaysDefinitionOfObjectOriented) in the 60s and the common definition used today. In this course will the definition of OOP be centred around the typical modern definition talking about blueprints/templates as it's the current standard in the industry.

### Steve Jobs explains object oriented programming

This is part of a [1994 interview with Steve Jobs from the The Rolling Stone](https://www.rollingstone.com/culture/culture-news/steve-jobs-in-1994-the-rolling-stone-interview-231132/):

> **Interviewer:**
>
> Would you explain, in simple terms, exactly what object-oriented software is?
>
> **Steve Jobs:**
>
> Objects are like people. They’re living, breathing things that have knowledge inside them about how to do things and have memory inside them so they can remember things. And rather than interacting with them at a very low level, you interact with them at a very high level of abstraction, like we’re doing right here.
>
> Here’s an example: If I’m your laundry object, you can give me your dirty clothes and send me a message that says, “Can you get my clothes laundered, please.” I happen to know where the best laundry place in San Francisco is. And I speak English, and I have dollars in my pockets. So I go out and hail a taxicab and tell the driver to take me to this place in San Francisco. I go get your clothes laundered, I jump back in the cab, I get back here. I give you your clean clothes and  say,  “Here are your clean clothes.”
>
> You have no idea how I did that. You have no knowledge of the laundry place. Maybe you speak French, and you can’t even hail a taxi. You can’t pay for one, you don’t have dollars in your pocket. Yet I knew how to do all of that. And you didn’t have to know any of it. All that complexity was hidden inside of me, and we were able to interact at a very high level of abstraction. That’s what objects are. They encapsulate complexity, and the interfaces to that complexity are high level.

## Programming concepts in OOP

Especially four programming concepts are important to understand when programming using OOP : Encapsulation, Inheritance, Polymorphism and Abstraction. These concepts often goes hand in hand, and can be hard to separate.

### Encapsulation

?[What is the goal of encapsulation within OOP?]
-[ ] To put your code in a "capsule", to make it secure
-[ ] To put a special focus on a specific feature in the code
-[x] To bind together data and functions that manipulate the data
-[x] To keep the internal state of the object within the object 

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
        c.CountUp(); // value wil be increased to: 1
        c.CountUp(); // value wil be increased to: 2
        Console.WriteLine(c.GetCounterValue()); //Expected 2
        c.CountDown(); // value wil be decreased to: 1
        Console.WriteLine(c.GetCounterValue()); //Expected 1
   }
}


```

### Inheritance

?[What is the goal of inheritance within OOP?]
-[ ] To use code without breaking the copyright
-[x] To reuse code functionality 
-[] To make sure code never dies

Example of inheritance, the species dog and human is in the functionality of the mammal, and modifies the two parameters legs and specie.

```C# runnable
using System;

public class Mammal
{
	private int numberOfLegs = 0;
	private string specie = string.Empty;

    public Mammal(){
		specie = "Unknown";
	}
    
	public Mammal(string specie, int numberOfLegs)
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

public class Dog : Mammal
{
	public Dog() : base("Dogs", 4)
	{
	}
}

public class Human : Mammal
{
	public Human() : base("Humans", 2)
	{
	}
}

class ExecuteInheritance {
	static void Main(string[] args) {
        var m = new Mammal();
		Console.WriteLine($"{m.Specie} has {m.NumberOfLegs} legs");
        
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

Example of polymorphism, the class Polymorph implements three different (polymorph) versions of the method Print. Type of input decides which of the implementations is executed.

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
-[x] To only show the essentials functionality of a class
-[ ] To make the code hard to read and understand
-[x] To hide away implementation details

Example of abstraction, the class mammal can't be instantiated since it have the modifier *abstract*, only the class Dog and Human can be instantiated, all functionality data which is generic for mammals are hidden in the Mammal class. The abstract method MakeASound needs to be implemented in all classes which inherits from Mammal.

```C# runnable
using System;

public abstract class Mammal
{
	private int numberOfLegs = 0;
	private string specie = string.Empty;

	public Mammal(string specie, int numberOfLegs)
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

public class Dog : Mammal
{
	public Dog() : base("Dogs", 4)
	{
	}

	public override void MakeASound()
	{
		Console.WriteLine("Wuf");
	}
}

public class Human : Mammal
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



## OOP Elements in C#

> An object is an entity that encapsulates **state** and **behaviour**. The state of an object is the current characteristics it possesses, for example, if a car is an object, one of its characteristics or *properties* may be how many people are in the car. A more static characteristic is the colour of the car.
>
> The behaviour of an object is represented by the possible actions or *methods* that the object can perform. In our automobile example, a car can start its engine, or shift into drive gear. A car can stop, make a turn, turn on its wipers, etc.
>
> An object can also inherit properties and methods from other types of objects (via *class* templates). For example, the car object can be considered a specialized form of “vehicle” which possesses more general properties and methods. A truck can inherit from the vehicle class. So can a farm tractor or an  airplane or a train or a boat.
>
> *Quote from: [How can I develop object oriented thinking in programming?](https://www.quora.com/How-can-I-develop-object-oriented-thinking-in-programming)* 

Objects are instances of classes. In other words, an instance of a class is an object defined by that particular class. Creating a new instance (in C# using the ```new``` term), or an object, is called instantiation.

**A class can be seen as a "template" or "blueprint" from which objects will be instantiated**. It’s like the mould from which objects can be created/instantiated from. A class represents a **real life concept** such as a person, an animal, a car, a house or a football.

A class consists of a collection of states (a.k.a. **variables** or **properties**) and **behaviours** (a.k.a. **methods**). 

An **object** is an **instance** of a **class**. The attributes of an object as stored using variables for storing data  and the behaviour/methods of an object are implemented as functions or procedures and can be used to perform operations on the data.

### Class

A representation of a collection of similar objects. Classes are often physical objects, representing a person, place, or thing. A class could be seen as a template of data with a given behaviour.

In C# we use the word ``class`` to define a class, example:

```csharp
class Car{
	int numberOfWheels;	
}
```

Read more: [Classes (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/classes)

### Object

An instance of a particular class. While a class may represent people, an object represents one particular person.

In C# we create an instance using the term ``new``, example:

```csharp
// instanciates two car obejcts
var car1 = new Car();
var car2 = new Car();	
```

Read more: [Objects (C# Programming Guide)](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/objects)

### Abstract Class

A class that can never instantiated into an object.

In C# we use ``abstract class`` to mark a class as abstract.

``` c#
abstract class Vehicle{
	public abstract void Start();
}

class Car : Vehicle{
    int numberOfWheels;
    public overrides void Start(){
        // logic to start the car
    }
}
```

Read more: [abstract (C# Reference)](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/abstract)

### Properties

An interesting property of a class. Usually in the form of a value.

In C# these are defined much the same way as a method:

```c#
class Car{
	int NumberOfWheels{ get; set; };	
}
```

Read more: [Properties](https://docs.microsoft.com/en-us/dotnet/csharp/properties)

Often these is used to access a hidden/encapsulated variable.

```c#
class Car{
    private int numberOfWheels;
    
    // The property makes it only possible to retrive the number of wheels, not modify it this increases the encapsulation
	public int NumberOfWheels{ 
		get {
			return this.numberOfWheels;
		}
	};	
}
```

## Design principles

I the following lecture will we look more into OOP design principles, but the there is two basic design principles of OOP which is important to look into in beforehand and that is [coupling and cohesion](https://sanaulla.info/2008/06/26/cohesion-and-coupling-two-oo-design-principles/).

?[What is our goal as developers when developing OO code?]
-[ ] High coupling and high cohesion
-[ ] High coupling and low cohesion
-[x] Low coupling and high cohesion
-[] Low coupling and low cohesion 

## Object oriented thinking
There is a lot of tools to support the development of OOP applications, one of the most wide spread is [UML](https://en.wikipedia.org/wiki/Unified_Modeling_Language).

In this course are we especially going to use [Use case diagrams](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-use-case-diagram/) which is good to identify the users of the system and the functionality the need.

A way to train OOP-thinking is through a techniuqe called "CRC cards": [Class Responsibility Collaborator (CRC) Models: An Agile Introduction](http://agilemodeling.com/artifacts/crcModel.htm), it worth noting that this technique is rarly used in a worklife enviroment.

