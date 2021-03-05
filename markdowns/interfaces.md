# Interfaces

To some extend interfaces reminds a lot of an abstract class. But there is some big differences.

1. An interface can't contain any logic (not quite true as C# 8.0 introduces [default implementations](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-8.0/default-interface-methods))
2. A class can implement several interfaces, but only on inherit one class
3. An interface says nothing about the internal state of a class

An interfaces should be seen as a contract which define the public properties, methods, and events, which the class or struct must implement.

An object never can be an instance of an interface, but an object can be an instance of a class implementing one or more interfaces.

## Naming

Interfaces is more or less the only type in [Microsoft C# naming convension](https://docs.microsoft.com/en-us/dotnet/standard/design-guidelines/names-of-classes-structs-and-interfaces) where prefixes is used in the naming. 

So when naming an interface should the name be prefixed with an *I*. Eg. an interface for a mammal would would be named IMammal.

## Interface example

In this example does the interface IMammal tell us that all mammals have two properties: number of legs and the specie of the mammal, and that the mammal have the behavior of making a sound.

The example is quite simplified, but a key difference between a dog and a human (in this example) is the ability to speak, so the implementation of human and dog differs a bit, but they still implement to the same contract (interface). This contract is used by the DisplayMammal method to display the information on the mammal.

Question to think about: What could we do if the mammal does not have any legs? Like a whale

```C# runnable
using System;

public interface IMammal
{
	int NumberOfLegs { get; }
	string Specie { get; }
	void MakeASound();
}

// Dog implements the interface IMammel
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

// Human implements the interface IMammel
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

class ExecuteInterfaceExample{  
   static void Main(string[] args) {
        DisplayMammal(new Dog());
        DisplayMammal(new Human("The Ultimate Answer to Life, The Universe and Everything is...42!"));
   }
   
   static void DisplayMammal(IMammal mammal)
   {
       Console.WriteLine($"{mammal.Specie} has {mammal.NumberOfLegs} legs");
       Console.Write($"The {mammal.Specie} say: ");
       mammal.MakeASound();
   }
}

```

