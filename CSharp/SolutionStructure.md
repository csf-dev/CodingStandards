# Solution structure
A good solution structure promotes *scalability*, *abstraction* of technical concepts and *maintainability*.

Solution structure primarily refers to the organisation of **projects**, which usually correspond to compiled assemblies, for example **libraries** (DLL files). In solutions for applications software, the projects should be designed to allow expansion as new features and functionality is added. This tends to lead to the following categories of project. Each has its own linked information.

## Domain logic projects
Domain logic (aka "Business logic") is the rules of how the application functions. Most applications have two domain logic projects, a [domain API project] and a [domain implementation project].

## Technology implementation projects
[Technology implementation projects] exist to interface with a specific third-party technology, such as a .NET library. This might be a NuGet package, a proprietary library from a vendor or partner, or even a remote web-based API.

## Client projects
A [client project] is a way in which the application's functionality is exposed to 'something external'. That could be a UI of some kind like a web or desktop application. It could also be something like a web API, designed to be consumed by other software.

## Dependency injection projects
Application software should be using a [dependency injection framework]. All 'type registrations' and other logic specific to the chosen DI framework must go into a [dependency injection project].

## Test/spec projects
Projects for [specifying and testing the application] are not shipped in production but are used by the development team.

[domain API project]: DomainApiProject.md
[domain implementation project]: DomainImplementationProject.md
[Technology implementation projects]: TechnologyImplementationProject.md
[client project]: ClientProject.md
[specifying and testing the application]: TestAndSpecProjects.md
[dependency injection framework]: DependencyInjectionFramework.md
[dependency injection project]: DependencyInjectionProject.md

## Exception: Library solutions
If the *sole purpose of an entire solution* is to be used as a 'utility' or infrastructure library then it is acceptable for all of its code to exist within just a single project. This is OK because, unlike applications solutions, their scope of functionality is tightly limited and unlikely to expand with diverse new requirements.