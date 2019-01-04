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