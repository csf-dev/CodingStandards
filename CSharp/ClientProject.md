# Client projects
Client projects are how the application interacts with users or 'systems external to itself'. This could mean any of several things:

* An MVC web application
* A REST/JSON web API
* A desktop user interface
* A command-line interface

Code in client projects should be limited to that which is specific to the client. No *business logic code* should exist in any client projects - that belongs instead in the [domain implementation project].

[domain implementation project]: DomainImplementationProject.md

It is feasible for multiple client projects to *coexist*. In a way, [integration test projects] *could be thought of as a special sort of client project*.

[integration test projects]: TestAndSpecProjects.md

## Client project references
Client projects should ideally reference *only two other projects in the solution*: [the domain API] and [the dependency injection] projects.

[the domain API]: DomainApiProject.md
[the dependency injection]: DependencyInjectionProject.md

Whilst the client project will be using types from the domain implementation, it will be accessing them via DI and the interfaces declared in the domain API project.