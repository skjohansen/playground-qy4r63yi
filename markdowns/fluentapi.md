# Fluent API

A fluent API is a sequence of chained function calls, often arranged in a way that reads like an English sentence:

```C#
someObject.ShouldNotifyFor(x => x.FirstName).And(x => x.FullName).When(x => x.FirstName = "Floyd").ToResult(); 
```

Fluent API is a design pattern. The pattern was initially described by Martin Fowler in his article on [Fluent Interface](https://martinfowler.com/bliki/FluentInterface.html), and the main idea is to make code which is readable to ordinary written prose. 

The code build on the design [Builder design pattern](https://refactoring.guru/design-patterns/builder). And as the reader notice in the code example above make the code an extensive use of lambda expressions, which is quite normal for Fluent API .

## Existing fluent APIs

There is a lot of existing fluent APIs for C#, some of them are:

- [LINQ](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/linq/)
- [Azure Management Libraries for .NET](https://github.com/Azure/azure-libraries-for-net)
- [RestSharp](http://restsharp.org/), used for accessing REST APIs
- [Fluent Assertions](https://fluentassertions.com/) (used for unit testing)

## Your own fluent API

As applications becomes more complex, can the development of a custom fluent API be a good investment, as fluent APIs gives the possibility to create a domain-specific language. Which makes is possible to describe complex business logic in few lines of fluent API (if of course it's implemented in the API).

As with all other APIs, designing fluent APIs is not an trivial task, as you will need to find a balance locking in the developer using the API or giving open access. The problem is that it's almost impossible to foresee how the users of your API is planning to use the API.

When designing you fluent API can it be a good trick to try to tell all the "stories" that you can think the users are going to implement with the API. This can be done be creating a tree of actions which you are imaging the user to perform, and in that way document the path you expect or limit the user to follow.

A path consist of fluent methods, and these could be categorized into either starting, context or exit methods:

- Start methods: Initializes the execution of a path
  - eg: StartX(), QueryX(), UpdateX(), SelectX()
- Context methods: Specify the information within a path (between start and end)
  - eg: WithX(), WithoutX(), UsingX(), AddX(), RemoveX()
- Exit methods: Ends execution of a path, initialized by a start method, defines what should be the output of the path
  - eg: ApplyX(), AttachX(), ToX(), And(), Or()

## Example of custom fluent API

```C# runnable
using System;
using System.Collections.Generic;

class Program{
    static void Main()
    {
        new Mammal("Human")
            .WithBrain()
            .WithLegs(2)
            .WithArms(2)
        .BringToLife();
    }
}

class Mammal : IMammal
{
	private IEnumerable<BodyPart> BodyParts {get; set;}
	private string Name {get; set;}

	public Mammal(string name)
	{
		// Start method
		BodyParts = new List<BodyPart>();
		Name = name;
	}

	public IMammal WithArms(int number)
	{
		// context method
		((List<BodyPart>)BodyParts).Add(new BodyPart() { Name = "Arms", Amount = 2 });
		return this;
	}

	public IMammal WithBrain()
	{
		// context method
		((List<BodyPart>)BodyParts).Add(new BodyPart() { Name = "Brain", Amount = 1});
		return this;
	}

	public IMammal WithLegs(int number)
	{
		// context method
		((List<BodyPart>)BodyParts).Add(new BodyPart() { Name = "Legs", Amount = 2 });
		return this;
	}
	
	public void BringToLife() 
	{
		// Exit method
		foreach (var bp in BodyParts)
		{
			Console.WriteLine($"{Name} has {bp.Amount} {bp.Name}");
		}	
	}
}

interface IMammal
{
	IMammal WithBrain();
	IMammal WithLegs(int number);
	IMammal WithArms(int number);
	void BringToLife();
}

class BodyPart
{
	public int Amount {get; set;}
	public string Name {get; set;}
}


```


## Fluent API and lambda expressions

Fluent APIs are often use in combination with Lambda expressions. 

For instance in LINQ:
```C#
var personsAbove18 = myPersonContext.Where(p => p.Age => 18).ToList();
```

### Example of fluent with lambda

Try to change the order of the Has and WithArms methods in the Main-method

```C# runnable
using System;
using System.Collections.Generic;

class Program{
    static void Main()
    {
        new Mammal("Human")
        	.Has(b => b.Name == "Arms") //the code after the lambda operator is the anonymous method which is going to be invoked by the has-method
            .WithArms(2)
        .BringToLife();
    }
}

class Mammal : IMammal
{
	private IEnumerable<BodyPart> BodyParts {get; set;}
	private string Name {get; set;}

	public Mammal(string name)
	{
		// Start method
		BodyParts = new List<BodyPart>();
		Name = name;
	}

	public IMammal WithArms(int number)
	{
		// context method
		((List<BodyPart>)BodyParts).Add(new BodyPart() { Name = "Arms", Amount = 2 });
		return this;
	}
	
	public IMammal Has(Func<BodyPart, bool> bodyPartCheck)
	{
        foreach(var bp in BodyParts){
            // loop all bodyparts and invoke the check for each
            // the check takes an BodyPart as input and outputs a bool
            if(bodyPartCheck.Invoke(bp) == true){
                throw new Exception($"{bp.Name} is already in place");
            }
        }
        
        // no matching bodyparts was found
        return this;
	}
	
	public void BringToLife() 
	{
		// Exit method
		foreach (var bp in BodyParts)
		{
			Console.WriteLine($"{Name} has {bp.Amount} {bp.Name}");
		}	
	}
}

interface IMammal
{
	IMammal Has(Func<BodyPart, bool> bodyPartQuery);
	IMammal WithArms(int number);
	void BringToLife();
}

class BodyPart
{
	public int Amount {get; set;}
	public string Name {get; set;}
}


```
