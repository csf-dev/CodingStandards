# .NET namespaces
Namespaces offer a mechanism by which to **logically organise** your types. Namespaces are most useful when they are **clear** and **intuitive**.

*Avoid over-designing* the solution's namespace hierarchy; think twice before creating a new namespace. A good rule of thumb is to keep to within *a maximum of four* levels/segments of name. Most of your types *should appear within the first two/three levels* of namespace.

The very first level (sometimes two levels) for a given .NET project is reserved for the [root namespace].

[root namespace]: RootNamespace.md

## Designing namespaces
Ideally, namespace segments should be based upon **the business function** of their contents, instead of the technology which provides that function. Using the name of a technology or specific solution is permitted if that technology is both:

* A part of the application requirements
* Well-known (at least by name) by both developers and non-developers alike

For example - an application which tracks delivery vehicles could feasibly include a namespace "GPS". The Global Positioning System is a technology that is understood to some degree by everyone, even though the business function is "getting the location".

Namespace segments based on business requirements should ideally use **verb phrases** or **plurals**, to avoid conflicting with class names.