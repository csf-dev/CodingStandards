# Test & specification projects
Test and specification projects are *never deployed in production* but are used to improve the quality of development code. There are a number of different types of project dealt with under this name.

## Unit test projects
**Unit tests** test only *a single class*. Each unit test class (aka "Test fixture") should test precisely one implementation class. Any of that implementation class' dependencies should be substituted with *a test fake* such as a mock object.

Unit tests should be written by directly using a testing framework such as **NUnit**. There is little to gain by using high-level specification languages like cucumber for unit tests.

Generally, unit tests should be grouped into one project for each project which they test. This makes it easier to manage dependencies and avoid bloat (such as unit test projects needing to reference APIs upon which [gateway projects] the depend).

[gateway projects]: GatewayProject.md

## Integration test projects
Integration tests differ from unit tests (above) in that they test segments of application code in a manner close to how they would be used by the application itself.

Mock objects are permitted in integration tests (for example, to substitute a database) but generally they should use the same API as the rest of the application would use.

> There are gains to be had in using high-level testing languages like cucumber to write integration tests. It's not mandatory but it's worth considering.

Integration tests should be configured just like they were [a type of client project]. They should use **dependency injection** (via [the dependency injection project]) to instantiate the components which are tested.

[a type of client project]: ClientProject.md
[the dependency injection project]: DependencyInjectionProject.md

## System test projects
System tests test the entire application as a real user would. Generally speaking, a system test project would not participate in the solution structure like any other project. A system test does not reference other projects in the application because it does not use their functionalities via the APIs, rather by 'driving' a user interface via an appropriate framework.