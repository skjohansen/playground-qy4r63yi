# Interfaces

To some extend interfaces reminds a lot of an abstract class. But there is some big differences.

1. An interface can't contain any logic
2. A class can implement several interfaces
3. An abstract class is a class which can't be instantiated.

An interfaces should be seen as a contract which define the public properties, methods, and events, which the class or struct must implement.

An object never can be an instance of an interface, but an object can be an instance of a class implementing one or more interfaces.

## Naming

Interfaces is more or less the only type in [Microsoft C# naming convension](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-classes-structs-and-interfaces) where prefixes is used in the naming. 

So when naming an interface should the name be prefixed with an *I*. Eg. an interface for a mammal would would be named IMammal.

```C# runnable
using System;

public interface IMammal
{
	int NumberOfLegs { get; }

	string Specie { get; }

	void MakeASound();
}


public class Dog : IMammal
{
	private int numberOfLegs = 4;
	private string specie = "Dogs";

	public int NumberOfLegs => numberOfLegs;

	public string Specie => specie;

	public void MakeASound()
	{
		Console.WriteLine("Wuf");
	}
}

public class Human : IMammal
{
	private int numberOfLegs = 2;
	private string specie = "Humans";

	public int NumberOfLegs => numberOfLegs;

	public string Specie => specie;

	public void MakeASound()
	{
		Console.WriteLine("Hello World");
	}
}

class ExecuteAbstraction{
	static void Main(string[] args) {
        IMammal d = new Dog();
        Console.WriteLine($"{d.Specie} has {d.NumberOfLegs} legs");
        Console.Write("The dog say: ");
        d.MakeASound();

        IMammal h = new Human();
        Console.WriteLine($"{h.Specie} has {h.NumberOfLegs} legs");
        Console.Write("The human say: ");
        h.MakeASound();
   }
}

```

