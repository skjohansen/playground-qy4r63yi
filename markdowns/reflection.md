# Reflection using C#

Reflection as word means something like consideration of some subject matter, or the return of light or sound waves from a surface.

In relation to code is it when managed code reads its codes [metadata](https://en.wikipedia.org/wiki/Metadata) to retrieve extended information, this is in C# done by providing objects (of type [Type](https://docs.microsoft.com/en-us/dotnet/api/system.type)) that describe assemblies, modules, and types.

You can among other use reflection to:
* obtain type information
* get information of an assembly
* build new types at runtime
* performing [late binding](https://www.geeksforgeeks.org/late-binding-using-reflection-in-c-sharp/)

## Example on reflection

```csharp runnable
void Main()
{
	int i = 42;
	Type type = i.GetType();
	Console.WriteLine(type);
}
```



## Late binding

https://docs.microsoft.com/en-us/dotnet/framework/reflection-and-codedom/dynamically-loading-and-using-types


late binding

```csharp runnable
class Program { 
  
    // Main Method 
    static void Main(string[] args) 
    { 
        // Declare Instance of class Assembly 
        // Call the GetExecutingAssembly method  
        // to load the current assembly 
        Assembly executing = Assembly.GetExecutingAssembly(); 
  
        // To find the type of the Class Student 
        Type studentType = executing.GetType("LateBinding.Student"); 
  
        // Create an Instance of the Student type 
        object studentObject = Activator.CreateInstance(studentType); 
  
        // Store the info of the method in an object 
        // of class MethodInfo 
        MethodInfo getMethod = studentType.GetMethod("GetDetails"); 
  
        // To store the parameters required 
        // by Method GetDetails 
        String[] param = new String[2]; 
        param[0] = "1"; 
        param[1] = "Lisa"; 
  
        // To display the result of the method 
        String det = (String)getMethod.Invoke(studentObject, param); 
        Console.WriteLine("Student Details : "); 
        Console.WriteLine("Roll Number - Name \n{0}", det); 
  
    }  
} 
  
  
public class Student { 
  
    public String GetDetails(String RollNumber, String Name) 
    { 
        return RollNumber + " - " + Name; 
    } 
  
} 
```



https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/reflection