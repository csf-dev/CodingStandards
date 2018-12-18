# Value types
Value types refer to data/state-carrying objects which do not have a unique identity, but which have good cause to be a part of the application domain. Examples of value types include amounts of money and/or dimensions (width/height).

## Favor immutability
When designing value types, it is beneficial to make your types **immutable**. The 'raw' value(s) which make up the instance are injected via the constructor and are then *only* exposed in a **read-only** manner by properties and methods. *Nothing* is permitted to modify the underlying values of an instance which has already been constructed.

Where an instance must be used to derive a new value, rather than altering an existing instance, the functionality should create a new instance containing the result.

## Favor structs
When designing value types, *prefer using structs over classes*. Structs are true value types in the C# language which means they have the correct expected behaviour for this purpose.

## Implement `Equals` and `GetHashCode`
All value types should at least have an implementation of the methods `bool Equals(object)` and `int GetHashCode()`. You may also want to implement `IEquatable<T>` for its own type as well.