# Why unit test?

## Less time performing functional tests

- Unit tests, on the other hand, take milliseconds
- Don't depend on external services
- Allow reproducible results

## Arranging your tests
Arrange, Act, Assert is a common pattern when unit testing. As the name implies, it consists of three main actions:
- Arrange your objects, create and set them up as necessary. [Example](examples/test_arrangement.md)
- Act on an object.
- Assert that something is as expected.
  Readability is one of the most important aspects when writing a test. Separating each of these actions within the test clearly highlight the dependencies required to call your code, how your code is being called, and what you're trying to assert. While it might be possible to combine some steps and reduce the size of your test, the primary goal is to make the test as readable as possible.

## Protection against regression

- Provides confidence that your new code doesn't break existing functionality [Example](examples/regression_example.md)

## Improved Bug handling
- Unit testing helps identify bugs and issues in the code at an early stage, making it easier to fix them. [Example](examples/bug_identification.md)
- When a test fails, it is much easier to locate the problem since the tests are focused on specific units of code.

## Executable documentation

- Tests provide functionality documentation [Example](examples/documentation_example.md)
- Allows to easily run certain scenarios and check what happens if we pass certain input
- Well named test explain what can be done with the code and ensure it actually works

## Less coupled code

- When code is tightly coupled, it can be difficult to unit test. Without creating unit tests for the code that you're
  writing, coupling might be less apparent. [Example](examples/tightly_coupled.md)
- The principle of developers eating their own dog food. Be the customer of your own code.

## Characteristics of a good unit test

- Fast: It isn't uncommon for mature projects to have thousands of unit tests. Unit tests should take little time to
  run. Milliseconds.
- Isolated: Unit tests are standalone, can be run in isolation, and have no dependencies on any outside factors such as
  a file system or database.
- Repeatable: Running a unit test should be consistent with its results, that is, it always returns the same result if
  you don't change anything in between runs.
- Self-Checking: The test should be able to automatically detect if it passed or failed without any human interaction.
- Timely: A unit test shouldn't take a disproportionately long time to write compared to the code being tested. If you
  find testing the code taking a large amount of time compared to writing the code, consider a design that is more
  testable.

## Code coverage

- Code coverage is often associated with a higher quality of code. However, the measurement itself can't determine the
  quality of code. Good practice is to maintain 85%-90% code coverage.

## Mocks vs. Stubs
- The main thing to remember about mocks versus stubs is that mocks are just like stubs, but you assert against the mock object, whereas you don't assert against a stub.

## Dependencies on infrastructure
- Dependencies make the tests slow and brittle
- Avoid these dependencies by:
  - Using [Dependency Injection](https://learn.microsoft.com/en-us/dotnet/core/extensions/dependency-injection)
  - Following the [Explicit Dependencies Principle](https://deviq.com/principles/explicit-dependencies-principle) (i.e. all dependencies should be declared explicitly)
  - Following [The Dependency Inversion Principle](https://deviq.com/principles/dependency-inversion-principle) (i.e. high level modules should not depend on low level modules, but both should depend on abstractions)

## Test Naming
- The name of the method being tested [Example](examples/test_naming.md)
- The scenario under which it's being tested
- The expected behavior when the scenario is invoked

## Validate private methods by unit testing public methods when possible
- Private methods are an implementation detail and never exist in isolation.
- At some point, there's going to be a public facing method that calls the private method as part of its implementation.
- What you should care about is the end result of the public method that calls into the private one.

## Testing internal methods in case it is hard to test the public method
- In some cases we have tightly coupled legacy code in public method which makes it hard to unit test it directly. In these cases we might want to unit test `internal` methods separately. [Example](examples/testing_internal.md)

## Avoid using static calls/references in the code
- For example, if we need to use `DateTime.Now`, instead of directly calling it in the code, create an instance of IDateTimeProvider.

#### Based on [Unit testing best practices with .NET Core and .NET Standard](https://learn.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices)