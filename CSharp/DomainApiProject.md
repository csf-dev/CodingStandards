# The domain API project
Every solution for *application software* should have one project for the **Domain API**. This API is a declaration of *what the application can do*, without any concerns as to *how it is done*. There should be no logic code in this project.

It is best for an application solution to have only **one** domain API project. There are rarely any practical benefits to come of splitting it into multiple projects. Splitting the domain API up can create often-unwanted dependency problems though, because circular assembly references are not permitted.

## Naming
The project name for the domain API project should follow the format `[SolutionName].Domain`. It should use the same [root namespace] as the solution which contains it, without the `.Domain` suffix.

[root namespace]: RootNamespace.md

## Contents
The domain API project *should never contain any logic code*, nor should it contain any references to implementation-specific technologies. The correct types for this project are:

* [Entity classes]
* [Value types] and [domain DTOs]
* [Single responsibility interfaces] representing domain services
    * These services & operations should be those which are useful in the context of [the application domain]
    * Where appropriate, this includes [request and result types] required by those services

[the application domain]: TheApplicationDomain.md
[Single responsibility interfaces]: SingleResponsibilityInterfaces.md
[request and result types]: RequestAndResultTypes.md
[Entity classes]: DomainEntities.md
[Value types]: ValueTypes.md
[domain DTOs]: DomainDtos.md

## References and packages
Because this project provides only the API for the application *without any consideration as to how it will be implemented*, this project *should not reference any other projects* within the same solution.

Likewise, the domain API project should have *no third-party dependencies* such as NuGet packages. It also should not reference any implementation-specific .NET framework libraries such as `System.Data`.

Remember that anything referenced-by/used-by the domain API project *must be understood by all [client projects] & [technology projects]* which consume the domain API. It is desirable to keep that to a minimum, ideally zero.

Conversely, it is common for every other project in the solution to use the domain API project as a dependency.

[client projects]: ClientProject.md
[technology projects]: TechnologyImplementationProject.md