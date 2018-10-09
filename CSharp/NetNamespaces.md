# .NET namespaces
Namespaces offer a mechanism by which to **logically organise** your types. Namespaces are most useful when they are **clear** and **intuitive**.

A pitfall to avoid is over-designing the namespaces within a solution. A good rule of thumb is to keep to within *a maximum of four* levels/segments of name. Most of your types *should appear within the first two/three levels* of namespace. Be careful not to create new namespaces too quickly.

The first level of namespace (sometimes the first two levels) for a given .NET project is reserved for the [root namespace].

[root namespace]: RootNamespace.md

## Designing namespaces
Ideally, namespace segments should be based upon **the business function** of their contents, instead of the technology which provides that function. Using the name of a technology or specific solution is permitted if that technology is both:

* A part of the application requirements
* Well-known (at least by name) by both developers and non-developers alike

For example - an application which tracks delivery vehicles could feasibly include a namespace "GPS". The Global Positioning System is a technology that is understood to some degree by everyone, even though the business function is "getting the location".

Namespace segments based on business requirements should ideally use **verb phrases** or **plurals**, to avoid conflicting with class names.