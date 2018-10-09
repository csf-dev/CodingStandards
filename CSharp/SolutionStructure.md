# Solution structure
A good solution structure promotes *flexibility*, *abstraction* of technical concepts and *maintainability*.

## .NET namespaces
A lesser aspect of the solution structure is [the hierarchy of **namespaces**] created by the various types. Solutions should have a **root namespace**, where all types within that solution are a descendent of that root namespace.

[the hierarchy of **namespaces**]: NetNamespaces.md

## Projects
The largest part of the solution structure is how the **projects** within that solution are organised. Generally speaking, .NET projects correspond directly to compiled assemblies, which are usually **libraries** (DLL files).

Projects are assigned a *root namespace*, just like the solution which contains them. The root namespace for every project should be either equal to the solution's root namespace or a descendent of the solution's root namespace.

### Applying to all solutions
Generally-speaking, all solutions should have a [domain API project]. This project should occupy the *root namespace* for the solution.

[domain API project]: DomainApiProject.md