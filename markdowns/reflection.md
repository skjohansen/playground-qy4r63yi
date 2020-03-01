# Reflection using C#

Reflection as word means something like consideration of some subject matter, or the return of light or sound waves from a surface.

In relation to code is it when managed code reads its codes [metadata](https://en.wikipedia.org/wiki/Metadata) to retrieve extended information, this is in C# done by providing objects (of type [Type](https://docs.microsoft.com/en-us/dotnet/api/system.type)) that describe assemblies, modules, and types.

You can among other use reflection to:
* obtain type information
* get information of an assembly
* build new types at runtime
* performing [late binding](https://www.geeksforgeeks.org/late-binding-using-reflection-in-c-sharp/) 

We are going use reflection working with attributes.

## Simple example on reflection

```C# runnable
using System;

class Program{
    static void Main()
    {
    	int i = 42;
    	Type type = i.GetType();
    	Console.WriteLine(type);
    }
}
```


