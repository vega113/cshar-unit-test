# Testing Internals
To unit test internal methods in C#, you can use the InternalsVisibleTo attribute. This attribute allows you to expose internal members of an assembly to another assembly, which makes it possible to test internal methods.

Here's a step-by-step guide on how to do this:

Add the following attribute to the class you want to test:
```
[assembly: InternalsVisibleTo("YourCompany.Shapes.UnitTest")]
```
Examples in the Core project:
- [AdyenApiTest](https://bitbucket.org/globaleteam/core/src/develop/Testing/Old/UnitTestProject1/ExternalAPIs/Payments/Gateways/AdyenApiTest.cs)
- [AdyenApi](https://bitbucket.org/globaleteam/core/src/develop/GlobalE.ExternalAPIs.Secured/Payments/Gateways/AdyenAPI.cs)

Replace `YourCompany.Shapes.UnitTest` with the namespace of your unit test project.

In your test project, add a reference to the project containing the internal methods you want to test.

Now you can write unit tests for your internal methods, just as you would for public methods.

Here's an example:

Suppose you have an internal method `CalculateArea` in a class Rectangle:
```csharp
[assembly: InternalsVisibleTo("YourCompany.Shapes.UnitTest")]
namespace YourCompany.Shapes
{
    public class Rectangle
    {
        public int Length { get; set; }
        public int Width { get; set; }
    
        internal int CalculateArea()
        {
            return Length * Width;
        }
    }
}
```

In your test project, create a test class RectangleTests and write a test for the `CalculateArea` method:
```csharp
namespace YourCompany.Shapes.UnitTest
{
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
}
```

In this example, we've created a unit test for the `CalculateArea` method. Although `CalculateArea` is an internal method, we're able to access it in the test project because we've specified the `InternalsVisibleTo` attribute in the `AssemblyInfo.cs` file of the project containing the `Rectangle` class.

Now you can run your test just as you would for any other test. This approach allows you to test internal methods without making them public, ensuring that you can still maintain proper encapsulation while verifying the correctness of your code.