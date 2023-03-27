# Testing Internals
To unit test internal methods in C# using XUnit, you can use the InternalsVisibleTo attribute in your project's AssemblyInfo.cs file (or create one if it doesn't exist). This attribute allows you to expose internal members of an assembly to another assembly, which makes it possible to test internal methods.

Here's a step-by-step guide on how to do this:

In your project, create a file named AssemblyInfo.cs if it doesn't exist. This file is usually located in the Properties folder for .NET Framework projects, and in the root folder for .NET Core and .NET 5+ projects.

Open the `AssemblyInfo.cs` file and add the following line:

```csharp
using System.Runtime.CompilerServices;

[assembly: InternalsVisibleTo("YourTestProjectName")]
```

Replace YourTestProjectName with the name of your test project.

In your test project, add a reference to the project containing the internal methods you want to test.

Now you can write unit tests for your internal methods using XUnit, just as you would for public methods.

Here's an example:

Suppose you have an internal method `CalculateArea` in a class Rectangle:
```csharp
public class Rectangle
{
    public int Length { get; set; }
    public int Width { get; set; }

    internal int CalculateArea()
    {
        return Length * Width;
    }
}
```

In your test project, create a test class RectangleTests and write a test for the `CalculateArea` method:
```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;
using YourProjectNamespace;

[TestClass]
public class RectangleTests
{
    [TestMethod]
    public void CalculateArea_ShouldReturnCorrectArea_WhenCalled()
    {
        // Arrange
        var rectangle = new Rectangle
        {
            Length = 4,
            Width = 5
        };

        int expectedArea = 20;

        // Act
        int result = rectangle.CalculateArea();

        // Assert
        Assert.AreEqual(expectedArea, result);
    }
}
```

In this example, we've created a unit test for the `CalculateArea` method using XUnit. Although `CalculateArea` is an internal method, we're able to access it in the test project because we've specified the `InternalsVisibleTo` attribute in the `AssemblyInfo.cs` file of the project containing the `Rectangle` class.

Now you can run your test just as you would for any other test using XUnit. This approach allows you to test internal methods without making them public, ensuring that you can still maintain proper encapsulation while verifying the correctness of your code.