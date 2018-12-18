# Root namespaces
Each **project** within a solution is associated with a [.NET namespace]. *All types in each project must be a descendent of that project's root namespace*.

A **solution** can be thought to have a root namespace also, although it is not enforced by the .NET project system.

[.NET namespace]: NetNamespaces.md

## For application solutions
.NET solutions for application software should use a root namespace which is comprised of **a single naming segment**. This should be a short name for the app. There is little to gain from using a more complex root namespace for an application, since it is unlikely that its libraries will be used outside the organisation where it is developed.

## For shared library solutions
Solutions which represent logic that is *intended for reuse by others outside the organisation* (such as release via NuGet) may use a two-segment root namespace. This should be in the format `OrganisationName.LibraryName`. Including the organisation name helps avoid namespace clashes with other packages.

## Domain logic projects
Two projects in each solution, the [domain API project] and the [domain implementation project] should use *the same root namespace as their parent solution*.

[domain API project]: DomainApiProject.md
[domain implementation project]: DomainImplementationProject.md

## Gateway projects
Projects which contain implementation logic for a specific technology are a little harder to assign a root namespace. The spirit of the following guidelines is to try where possible to relate that technology to the solution domain. Only if that's not possible should a namespace be created for the technology itself.

1. If the technology will need access to types throughout your entire domain API then - like the [domain API project] - use the same root namespace as the solution root.
2. If the technology relates only to an existing namespace in your domain API (all of its types will fall within that namespace) then use that namespace as the root of the project.
3. If the technology does not directly relate to your domain then create a new namespace for the technologies as a direct child of the solution root. This will be the root namespace for the project.

### Examples
* A solution is integrating an Object/Relationship Mapper (ORM). This ORM code will be going into a project of its own. That ORM project will need access to all of the entity types in the domain API project. This project should use *the same root namespace as the solution*.
* A solution which tracks parcel delivery is integrating a third party GPS library for locating its delivery vans. The domain API project already has a `Location` namespace as a child of the solution root. The project to integrate this technology should use that `Location` namespace as its root.
* A solution is integrating a third party logging framework to log debug/error information. This does not relate to the domain at all (it's purely a technological matter). In this case, it is acceptable to create a new `Logging` namespace under the solution root.