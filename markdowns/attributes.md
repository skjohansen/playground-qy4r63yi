# Attributes in C#

Attributes gives us the ability to associating metadata, or declarative information, with code (assemblies, types, methods,  properties etc.). This is in C# done using *[* and *]*, if you would like to add an attribute to a property:

```c#
[Description("This is a description of my property")]
public string MyProperty { get; set;}
```

Using reflection is it possible to retrieve the attributes.  We are especially going to use this when working with Object-relational mapping (ORM) later in the course.

Example of reading an attribute using reflection:

```C# runnable
using System;
using System.Reflection;
using System.ComponentModel;

public class Program{
    static void Main()
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

It's possible to define your own attributes. This done by creating a class which inherits from [Attribute](https://docs.microsoft.com/en-us/dotnet/api/system.attribute?view=netcore-3.1),

```C# runnable
using System;
using System.Reflection;
using System.ComponentModel;
using System.Collections.Generic;

class Program{
    static void Main()
    {
        ShowTaxonomyAttribute(typeof(Wolf));
        ShowTaxonomyAttribute(typeof(Human));
    }

    static void ShowTaxonomyAttribute(Type type)
    {
        System.Attribute[] attrs = System.Attribute.GetCustomAttributes(type);
        foreach (System.Attribute attr in attrs)
        {
            if (attr is Taxonomy)
            {
                Taxonomy t = (Taxonomy)attr;
                System.Console.WriteLine(t);
            }
            else
            {
                Console.WriteLine($"Non-taxonomy attribute: {attr.TypeId}");
            }
        }
    }
}

[Taxonomy("Eukarya", Kingdom = "Animala", Specie = "Vulpes vulpes")]
public class Wolf
{
	public void MakeASound()
	{
		Console.WriteLine("Wooooooww!");
	}
}

[Description("This is a human")]
[Taxonomy("Eukarya", Kingdom = "Animala", Phylum = "Chordata", Class = "Mammalia", Order= "Primates", Genus ="Homo", Specie = "Homo sapiens", Family = "Hominidae")]
public class Human
{
	public void MakeASound()
	{
		Console.WriteLine("Hallo world");
	}
}

// Custom Taxonomy attribute
[System.AttributeUsage(System.AttributeTargets.Class)]
public class Taxonomy : Attribute
{
	public string Domain { get; set; }
	public string Kingdom { get; set; }
	public string Phylum { get; set; }
	public string Class { get; set; }
	public string Order { get; set; }
	public string Family { get; set; }
	public string Genus { get; set; }
	public string Specie { get; set; }
	public Taxonomy(string domain)
	{
		Domain = domain;
	}

	public override string ToString()
	{
		List<string> descriptions = new List<string>();
		if(string.IsNullOrEmpty(Domain)) descriptions.Add("N/A"); else descriptions.Add(Domain);
		if(string.IsNullOrEmpty(Kingdom)) descriptions.Add("N/A"); else descriptions.Add(Kingdom);
		if(string.IsNullOrEmpty(Phylum)) descriptions.Add("N/A"); else descriptions.Add(Phylum);
		if(string.IsNullOrEmpty(Class)) descriptions.Add("N/A"); else descriptions.Add(Class);
		if(string.IsNullOrEmpty(Order)) descriptions.Add("N/A"); else descriptions.Add(Order);
		if(string.IsNullOrEmpty(Family)) descriptions.Add("N/A"); else descriptions.Add(Family);
		if(string.IsNullOrEmpty(Genus)) descriptions.Add("N/A"); else descriptions.Add(Genus);
		if(string.IsNullOrEmpty(Specie)) descriptions.Add("N/A"); else descriptions.Add(Specie);
		return string.Join(" -> ", descriptions);
	}
}
```

