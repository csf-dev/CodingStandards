# .NET namespaces
Namespaces offer a mechanism by which to **logically organise** your types. Namespaces are most useful when they are **clear** and **obvious**.

A pitfall to avoid is over-designing the namespaces within a solution. A good rule of thumb is to keep to within a maximum of four 'levels' of namespace, so at maximum `NSpace1.NSpace2.NSpace3.NSpace4.TypeName`. Most of your types should appear within the first two/three levels of namespace.

## Designing namespaces
Well-designed namespaces should be named based upon the **business function** of that namespace's contents, and *not upon a technological description of the contained code*.

For example, if our solution root namespace (below) were `RobotTracker` then the next level of namespaces might include:

* `RobotTracker.Locators`
* `RobotTracker.Maps`
* `RobotTracker.JourneyPlanning`

### Naming each segment
Namespace segments (apart from the root) should generally be named using a **plural noun**, for example "Maps" or a **verb phrase**, for example "JourneyPlanning". This helps keep them *clear as to their meaning* and also *avoids naming clashes with types*.

## Root namespaces
Each .NET solution, and each project within that solution has a namespace within which all of their types are contained.

### For solutions
#### Applications software
.NET solutions for application software should use a root namespace which is comprised of *a single naming segment*, which is a short name for the application.

When an application is to be used stand-alone, there is no need to use a more complex root namespace. Doing so 'uses up' excess levels of namespace with no benefit.

#### Shared library code
When the solution is not for a standalone application but rather s library which will be shared for use by developers outside of the organisation, then it makes sense to use a two-segment namespace for the root of the solution.

Generally this should use the format `OrganisationName.LibraryName`. The primary benefit of prefixing the namespace with the organisation's name is to *avoid potential namespace clashes* across different libraries.


### For projects
Projects which contain **business logic code** should use *the same root namespace as their solution*. This is because they could potentially contain logic for any business-logic namespace in that solution.

Where it comes to projects created to work with a specific technology, it *might* be worth creating a new namespace subordinate to the solution root. *If in doubt, use the same namespace as the solution root.* Create a sub-namespace for a technology-based project only if:

* That technology is well-known and well-understood by both the development team and the product owners/analysts.
* The usage of that technology is part of the core business logic of the application, rather than a way to solve a coding problem.

For example a project which provides location information service via a GPS service deserves a namespace segment `GPS`. GPS is well-known and understood by almost all people. Two non-developers might feasibly talk together and say something like "Then we get the delivery truck's location from GPS to find out how far away it is". On the other hand, a project which configure and sets up a dependency injection framework for the application is *not* a good candidate for a different root namespace.



For most projects, the root namespace should be formed from only a single naming segment. Generally this is the short name of the application. For example `ShippingCoordinator`.

Solutions which are intended for sharing outside of a single organisation as a library (for example, as a NuGet package) may be named using a two-segment namespace convention. Typically this is `OrganisationName.LibraryName`, for example `MomsRobots.StandingAndBalance`.

*Avoid using more than two segments* for the root namespace of a solution. This is likely to lead to namespace bloat. A good rule of thumb is to use no more than four segments for any namespace through the solution.