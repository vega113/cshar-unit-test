# Test Arrangement
Here's an example of an MSTest unit test that demonstrates the Arrange, Act, Assert pattern:
```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;
using YourProjectNamespace;

[TestClass]
public class MathOperationsTests
{
    [TestMethod]
    public void Divide_ShouldReturnCorrectQuotient_WhenGivenNonZeroDivisor()
    {
        // Arrange
        var mathOperations = new MathOperations();
        int dividend = 25;
        int divisor = 5;
        int expectedResult = 5;

        // Act
        int result = mathOperations.Divide(dividend, divisor);

        // Assert
        Assert.AreEqual(expectedResult, result);
    }
}
```

In this example:
- Arrange: A `MathOperations` instance is created, and the dividend, divisor, and expected result are defined.
- Act: The `Divide` method is called with the provided dividend and divisor.
- Assert: The expected result is compared to the actual result returned by the Divide method.