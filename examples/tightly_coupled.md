Writing unit tests can help reveal tightly coupled code, making it more apparent and encouraging developers to refactor their code for better maintainability and testability. Let's consider a simple example in C#:

Suppose we have a UserService class with a SaveUser method that directly interacts with a database, resulting in tight coupling:

```csharp
public class UserService
{
    public void SaveUser(string userName)
    {
        using (var connection = new SqlConnection("YourConnectionString"))
        {
            connection.Open();
            using (var command = new SqlCommand("INSERT INTO Users (UserName) VALUES (@UserName)", connection))
            {
                command.Parameters.AddWithValue("@UserName", userName);
                command.ExecuteNonQuery();
            }
        }
    }
}
```
In this example, the SaveUser method is tightly coupled to the database, making it difficult to test without interacting with the actual database. To test the SaveUser method, we can introduce an interface, IUserRepository, to decouple the database interaction:

```csharp
public interface IUserRepository
{
    void SaveUser(string userName);
}

public class UserRepository : IUserRepository
{
    public void SaveUser(string userName)
    {
        using (var connection = new SqlConnection("YourConnectionString"))
        {
            connection.Open();
            using (var command = new SqlCommand("INSERT INTO Users (UserName) VALUES (@UserName)", connection))
            {
                command.Parameters.AddWithValue("@UserName", userName);
                command.ExecuteNonQuery();
            }
        }
    }
}

public class UserService
{
    private readonly IUserRepository _userRepository;

    public UserService(IUserRepository userRepository)
    {
        _userRepository = userRepository;
    }

    public void SaveUser(string userName)
    {
        _userRepository.SaveUser(userName);
}
```

Now, we can create a unit test for the `SaveUser` method using a mock implementation of the `IUserRepository` interface:

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;
using Moq;
using YourProjectNamespace;

[TestClass]
public class UserServiceTests
{
    [TestMethod]
    public void SaveUser_WhenCalled_ShouldCallSaveUserInRepository_WhenGivenUserName()
    {
        // Arrange
        var userRepositoryMock = new Mock<IUserRepository>();
        var userService = new UserService(userRepositoryMock.Object);
        string userName = "John Doe";

        // Act
        userService.SaveUser(userName);

        // Assert
        userRepositoryMock.Verify(repo => repo.SaveUser(userName), Times.Once());
    }
}
```

In this test, we're using Moq to create a mock implementation of the IUserRepository interface. The test verifies that when SaveUser is called on the UserService instance, the SaveUser method on the IUserRepository instance is also called with the expected parameter.

By introducing the IUserRepository interface and decoupling the UserService class from the database, we've made it easier to unit test the SaveUser method. This approach also makes it more apparent that the original implementation was tightly coupled, encouraging a better separation of concerns and improved testability.