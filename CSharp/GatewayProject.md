# Gateway projects
Gateway projects are a way to ring-fence code which depends upon a complex or third-party API and place it into a solution project of its own. In doing so, the gateway project abstracts away from a difficult API and exposes it in a simpler way, which is meaningful to domain logic.

This means that apart from the gateway project itself and perhaps the [dependency injection project], no other project in the solution need have any direct reference to the API itself.

## What deserves a gateway project?
A "complex or third-party API" (as described above) could mean many things, so how should you decide when an API needs a gateway project? Here are some questions which may help.

* Does the API offer *interfaces* and, where applicable, DTOs for all of its functionality?
* Does the API preform all of its work locally (IE: it does not communicate over a network)?
* Is there a very low chance that you will want to switch the implementation of this API at a later date?
* Does this API need only trivial coding to use its findings?
* Is it reasonable for *the entire application* to depend on this API?

*If any of the answers to the above are 'no'* then you should strongly consider a gateway project for this API.

### Examples of suitable gateway projects
Some examples of APIs which deserve gateway projects:

* The API for a web service
* Logic which configures and sets up an Object Relation Mapper
* Logic to serialise/deserialise objects to/from XML

## The contents of a gateway project
The most important classes which should be contained within a gateway project are implementations of interfaces which are declared in [the domain API project]. In the implementations of interfaces declared in the domain API, there is *a balance to be struck* between the level of abstraction to use. The ideal level of abstraction is *just enough* so that consuming code does need to understand the internals of the wrapped API.

Beyond the implementations of services, other types in the gateway project should be limited to *the minimum that is required* to make use of the wrapped API, without needing to expose its internals outside the gateway project. Beware of mixing business logic into a gateway project; business logic should be placed within the [domain implementation project].


[the domain API project]: DomainApiProject.md
[dependency injection project]: DependencyInjectionProject.md
[domain implementation project]: DomainImplementationProject.md