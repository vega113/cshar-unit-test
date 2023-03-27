# Test Naming
Here is a code example in C# using MSTest that demonstrates the Test Naming rule. The rule states that a test method name should include:

- The name of the method being tested
- The scenario under which it's being tested
- The expected behavior when the scenario is invoked

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;
using YourProjectNamespace;

[TestClass]
public class StringFormatterTests
{
    [TestMethod]
    public void Truncate_ShouldReturnOriginalString_WhenMaxLengthIsGreaterThanStringLength()
    {
        // Arrange
        var stringFormatter = new StringFormatter();
        string input = "Hello, world!";
        int maxLength = 20;

        // Act
        string result = stringFormatter.Truncate(input, maxLength);

        // Assert
        Assert.AreEqual(input, result);
    }

    [TestMethod]
    public void Truncate_ShouldReturnTruncatedString_WhenMaxLengthIsLessThanStringLength()
    {
        // Arrange
        var stringFormatter = new StringFormatter();
        string input = "Hello, world!";
        int maxLength = 5;

        // Act
        string result = stringFormatter.Truncate(input, maxLength);

        // Assert
        Assert.AreEqual("Hello", result);
    }
}
```

In this example, the test method names follow the Test Naming rule:

- Truncate_ShouldReturnOriginalString_WhenMaxLengthIsGreaterThanStringLength: Indicates that the Truncate method should return the original string when the maxLength is greater than the string length.
- Truncate_ShouldReturnTruncatedString_WhenMaxLengthIsLessThanStringLength: Indicates that the Truncate method should return a truncated string when the maxLength is less than the string length.
These test names make it easier for developers to understand the purpose of each test and the expected behavior.
