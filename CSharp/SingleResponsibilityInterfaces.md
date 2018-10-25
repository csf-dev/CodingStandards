# Single responsibility interfaces
A **single responsibility interface** is an interface which describes a single operation which the application may perform, declaring *just one method*.

## Naming
Such an interface should have a **clear** and **understandable** name, using a **verb-based adjective phrase**. A way to create good names is to complete the following sentence and prefix it with `I` (to conform to usual C# standards).

> This interface is something that/which ...

Here are some good examples:
* IResetsUsersPassword
* IGetsDeliveryVehicleLocation
* ISavesCustomerOrder

## Design
Interface methods should be designed according to [the standard for good method design].

[the standard for good method design]: MethodDesign.md
