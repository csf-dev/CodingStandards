# Stateless services
Services are where *almost all of the business logic of an application* lies. Service classes are especially useful when they are backed by [single responsibility interfaces].

[single responsibility interfaces]: SingleResponsibilityInterfaces.md

As indicated by the name, stateless services *should not contain any mutable state*. It is normal for services to require read-only dependencies - passed via the constructor and stored as read-only fields. This means that a single instance of a service class is *reusable* as many times as desired and that the service will be *thread-safe* by design.

## Designing service functionality
Where practical, [methods offered by services] should be either [side-effect-free functions] or [state-changing actions].

Well-designed methods, backed by single responsibility interfaces are well-suited for extension by [the decorator pattern].

[methods offered by services]: MethodDesign.md
[side-effect-free functions]: SideEffectFreeFunctions.md
[state-changing actions]: StateChangingActions.md
[the decorator pattern]: TheDecoratorPattern.md

## Prefer well-known patterns
Where possible, a service class should implement [one of a number of well-known patterns]. This pattern should become a part of that class' name (see below).

Well-known patterns make the class easier to understand because developers familiar with the pattern will immediately know what to expect.

[one of a number of well-known patterns]: ServiceClassPatterns.md

## Naming service classes
Where [single responsibility interfaces] should be named based on *what they can do*, service classes should be named based on *what they are*.

A good way to name a class is to complete the following sentence. Where the class uses a well-known pattern (above), the name of that pattern should be a suffix to the class name.

> This class is a/the ...

Here are some examples:

* UserPasswordResetStrategy
* ProductIsInStockSpecification
* CustomerOrderPersister