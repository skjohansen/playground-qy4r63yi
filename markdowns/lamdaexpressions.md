# Lambda expressions in C#

In this course are we going to work a lot with LINQ and one cornerstone of LINQ is lambda expressions (especially when using the method-syntax), which more or less is build on top of [Lambda Calculus](https://en.wikipedia.org/wiki/Lambda_calculus). Many places are lambda using the Greek symbol : **λ** .

## Anonymous Methods

Lambda expressions is build upon the notion of anonymous method, these are methods which doesn’t contain any name and can be parsed around like parameters. Anonymous methods are defined using the [delegate](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/delegates/) keyword and the user can assign this method to a variable of the delegate type.

### Example of anonymous method

In  this example is  a delegate called MakeASoundDelegate, this allow for us to define the implementation of MakeASound and parse this around as a variable. 

```C# runnable
using System;

public delegate void MakeASoundDelegate(string sound); 

public abstract class Mammal
{
	private int numberOfLegs = 0;
	private string specie = string.Empty;
	protected string sound = string.Empty;

	public Mammal(string specie, int numberOfLegs, string sound)
	{
		this.numberOfLegs = numberOfLegs;
		this.specie = specie;
		this.sound = sound;
	}

	public int NumberOfLegs => numberOfLegs;

	public string Specie => specie;

	public abstract void MakeASound(MakeASoundDelegate makeASound);
}

public class Dog : Mammal
{
	public Dog() : base("Dogs", 4, "Woof")
	{
	}

	public override void MakeASound(MakeASoundDelegate makeASound)
	{
		makeASound(sound);
	}
}

public class Human : Mammal
{
	public Human() : base("Humans", 2, "How YOU Doin’?")
	{
	}

	public override void MakeASound(MakeASoundDelegate makeASound)
	{
		makeASound(sound);
	}
}

class ExecuteAbstraction{
	static void Main(string[] args) {
         MakeASoundDelegate makeASound = delegate (string sound)
            {
                Console.WriteLine($"The dog goes: {sound}");
            };

        var d = new Dog();
        Console.WriteLine($"{d.Specie} has {d.NumberOfLegs} legs");
        d.MakeASound(makeASound);

        makeASound = delegate (string sound)
           {
               Console.WriteLine($"The human goes: {sound}");
           };
        var h = new Human();
        Console.WriteLine($"{h.Specie} has {h.NumberOfLegs} legs");
        h.MakeASound(makeASound);
   }
}

```

In some circumstances can [delegates be used as an alternative to an interface](https://docs.microsoft.com/en-us/previous-versions/visualstudio/visual-studio-2010/ms173173(v=vs.100)).

## Lambda expressions

As written previously is [lambda expressions](https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions) an evolution of anonymous methods, but there is some key differences:

* Lambda expressions don't need to have a *delegate* variable 
* Lambda expressions must return a value
* The result of a lambda expression is Func<inputs, output> 

The `=>` operator is called the "lambda operator", and is used when defining the expression.

### Example

The previous example rewritten to use Lambda expressions instead

```C# runnable
using System;

public abstract class Mammal
{
	private int numberOfLegs = 0;
	private string specie = string.Empty;
	protected string sound = string.Empty;

	public Mammal(string specie, int numberOfLegs, string sound)
	{
		this.numberOfLegs = numberOfLegs;
		this.specie = specie;
		this.sound = sound;
	}

	public int NumberOfLegs => numberOfLegs;

	public string Specie => specie;

	public abstract void MakeASound(Func<string, string> makeASound);
}

public class Dog : Mammal
{
	public Dog() : base("Dogs", 4, "Woof")
	{
	}

	public override void MakeASound(Func<string, string> makeASound)
	{
		Console.WriteLine(makeASound(sound));
	}
}

public class Human : Mammal
{
	public Human() : base("Humans", 2, "How YOU Doin’?")
	{
	}

	public override void MakeASound(Func<string, string> makeASound)
	{
		Console.WriteLine(makeASound(sound));
	}
}

class ExecuteAbstraction{
	static void Main(string[] args) {
        Func<string, string> makeASound = sound => {
                return $"The dog goes: {sound}";
            };

        var d = new Dog();
        Console.WriteLine($"{d.Specie} has {d.NumberOfLegs} legs");
        d.MakeASound(makeASound);

        makeASound = sound =>
        {
            return $"The human goes: {sound}";
        };

        var h = new Human();
        Console.WriteLine($"{h.Specie} has {h.NumberOfLegs} legs");
        h.MakeASound(makeASound);
   }
}

```

The defintion of the Lambda expressions in the main method can compressed a bit to make the code easier to read:
```csharp
void Main()
{
	var d = new Dog();
	Console.WriteLine($"{d.Specie} has {d.NumberOfLegs} legs");
	d.MakeASound(sound => { return $"The dog goes: {sound}"; });

	var h = new Human();
	Console.WriteLine($"{h.Specie} has {h.NumberOfLegs} legs");
	h.MakeASound(sound => {return $"The human goes: {sound}";});
}
```
## Lambda expression with mulitple parameters

It's possible to define lambda expressions with mulitple input parameters.

```C# runnable
using System;

public abstract class Mammal
{
	private int numberOfLegs = 0;
	private string specie = string.Empty;
	private string sound = string.Empty;

	public Mammal(string specie, int numberOfLegs, string sound)
	{
		this.numberOfLegs = numberOfLegs;
		this.specie = specie;
		this.sound = sound;
	}

	public void DescribeMammal(Func<string, int, string> describeMammal)
	{
		Console.WriteLine(describeMammal(specie, numberOfLegs));
	}

	public void MakeASound(Func<string, string> makeASound)
	{
		Console.WriteLine(makeASound(sound));
	}
}

public class Dog : Mammal
{
	public Dog() : base("Dogs", 4, "Woof")
	{
	}
}

public class Human : Mammal
{
	public Human() : base("Humans", 2, "How YOU Doin\’?")
	{
	}
}

class ExecuteAbstraction{
	static void Main(string[] args) {
        var d = new Dog();
        d.DescribeMammal((specie,numberOfLegs) => {return $"{specie} has {numberOfLegs} legs"; });
        d.MakeASound(sound => { return $"The dog goes: {sound}"; });

        var h = new Human();
        h.DescribeMammal((specie,numberOfLegs) => {return $"Those with {numberOfLegs} legs could be {specie.ToLower()}"; });
        h.MakeASound(sound => {return $"The human some times says: {sound}";});
   }
}

```


