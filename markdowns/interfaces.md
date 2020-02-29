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

## Interface example

In this example is does the interface Mammal tell us that all mammal have two properties of number of legs and the specie of the mammal, and that the mammal have the behavior of making a sound.

The example is quite simplified, but a key difference between a dog and a human is the ability to speak, so the implementation of human and dog differs a bit, but they still implement to the same contract (interface). This contract is used by the DisplayMammal method to display the information on the mammal.

Question to think about: What could we do if the mammal does not have any legs? Like a whale

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
	private string quote;


	public Human(string quote){
		this.quote = quote;
	}

	public int NumberOfLegs => numberOfLegs;

	public string Specie => specie;

	public void MakeASound()
	{
		Console.WriteLine(quote);
	}
}

class ExecuteAbstraction{
    void DisplayMammal(IMammal mammal)
    {
        Console.WriteLine($"{mammal.Specie} has {mammal.NumberOfLegs} legs");
        Console.Write($"The {mammal.Specie} say: ");
        mammal.MakeASound();
    }
    
	static void Main(string[] args) {
        DisplayMammal(new Dog());
        DisplayMammal(new Human("The Ultimate Answer to Life, The Universe and Everything is...42!"));
   }
}

```

