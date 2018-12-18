# Solution structure
A good solution structure promotes *scalability*, *abstraction* of technical concepts and *maintainability*.

Solution structure primarily refers to the organisation of **projects**, which usually correspond to compiled assemblies, for example **libraries** (DLL files). In solutions for applications software, the projects should be designed to allow expansion as new features and functionality is added. This tends to lead to the following categories of project. Each has its own linked information.

## Domain logic projects
Domain logic (aka "Business logic") is the rules of how the application functions. Most applications have two domain logic projects, a [domain API project] and a [domain implementation project].

## Gateway projects
[Gateway projects] provide implementation logic which connects your domain logic projects to third party or external technologies which have their own specialised APIs.

APIs which warrant a gateway project could include technology-specific .NET libraries such as XML or a database, a vendor-provided library such as a NuGet package or it could be a web-based API which communicates with another software system.

## Client projects
A [client project] is a way in which the application's functionality is exposed to 'something external'. That could be a UI of some kind like a web or desktop application. It could also be something like a web API, designed to be consumed by other software.

## Dependency injection projects
Application software should be using a **dependency injection framework**. All 'type registrations' and other logic specific to the chosen DI framework must go into a [dependency injection project].

## Test/spec projects
Projects for [specifying and testing the application] are not shipped in production but are used by the development team.

[domain API project]: DomainApiProject.md
[domain implementation project]: DomainImplementationProject.md
[Gateway projects]: GatewayProject.md
[client project]: ClientProject.md
[specifying and testing the application]: TestAndSpecProjects.md
[dependency injection project]: DependencyInjectionProject.md

## Exception: Library solutions
It is usually OK to simplify this to a single project if *the sole purpose of the solution* is to publish a reusable code package. This could be a library DLL or a NuGet package for example. When choosing whether to do this, consider:

* Is the library likely to expand with new functionality or changed requirements?
* Does the library serve as a gateway to an API which consuming should not need to know about?

If either of the above are true then it might be best to use the solution structure described above.

If the solution's requirements are unlikely to change and it does not expose consumers to APIs beyond its own then it is acceptable to design the solution as a single project.