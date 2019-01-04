# C# coding standards
The intention of these coding standards is to produce *flexible, maintainable* code.

## Organisation
Good code is organised into [a layered solution structure] which encourages separation between business logic and 'infrastructure' concerns.

[a layered solution structure]: SolutionStructure.md

## Object design
All types should fall into one of the following broad categories:

* [Entity classes] represent individual, unique units of information.
* [Value types] complement entities, representing non-unique units of information.
    * Data Transfer Objects (DTOs) are a form of value type.
    * [Request and result types] are another kind of value type.
    * An amount of money (a decimal number, with a currency) is another sort of value type.
* A [stateless service] class, which encapsulates a single, reusable piece of business logic.
    * Ideally all services should be backed by [single responsibility interfaces].

[Entity classes]: DomainEntities.md
[Value types]: ValueTypes.md
[Request and result types]: RequestAndResultTypes.md
[single responsibility interfaces]: SingleResponsibilityInterfaces.md
[Stateless service]: StatelessServices.md