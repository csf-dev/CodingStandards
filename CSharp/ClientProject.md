# Client projects
Client projects are the way by which external systems or users *consume or interact with* the application. Often this is a UI of some kind, but it could just as readily be an API. Here are some examples of client projects.

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