# Attributes in C#

Attributes gives us the ability to associating metadata, or declarative information, with code (assemblies, types, methods,  properties etc.). This is in C# done using *[* and *]*, if you would like to add an attribute to a property:

```c#
[Description("This is a description of my property")]
public string MyProperty { get; set;}
```

Using reflection is it possible to retrieve the attributes.  We are especially going to use this when working with Object-relational mapping (ORM) later in the course.

Example of reading an attribute using reflection:

```c# runnable
using System;
using System.Reflection;

public class Program{
    void Main()
    {
        Test t = new Test();
        PropertyInfo info = t.GetType().GetProperty("MyProperty");
        var testAttribute = (DescriptionAttribute)info.GetCustomAttribute(typeof(DescriptionAttribute));
        Console.WriteLine(testAttribute.Description);
    }
}

public class Test
{
	[Description("This is a description of my property")]
	public string MyProperty { get; set;}
}
```

.NET comes with a range of build in attributes, among these are:

- [Category](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.categoryattribute?view=netcore-3.1)
- [Description](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.descriptionattribute?view=netcore-3.1)
- [Designer](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.designerattribute?view=netcore-3.1)
- [DataObject](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.dataobjectattribute?view=netcore-3.1)
- [ReadyOnly](https://docs.microsoft.com/en-us/dotnet/api/system.componentmodel.readonlyattribute?view=netcore-3.1)

## Custom attributes

It's possible to define your own attributes. This done by creating a class which inherits from 

https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/attributes/creating-custom-attributes

Read more: 

