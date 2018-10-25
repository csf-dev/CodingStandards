# Request & Result types
Request and result (aka request and response) types are classes which are created to support [methods] which expose complex inputs and outputs. Request and result classes are *always specific to a single method*, usually one which is defined as part of a [single responsibility interface].

[methods]: MethodDesign.md
[single responsibility interface]: SingleResponsibilityInterfaces.md

## Request types
Creating a request type is applicable when a method has *complex parameters* which are at medium-to-high risk of changing as business requirements change.

A request class is useful because as the parameters which the method accepts are expanded, the method signature remains the same (it still takes the one parameter).

## Result types
Result (or response) types are useful for [functions] which return complex data structures, such as those which aggregate other stand-alone data structures which might otherwise not relate to one another.

Result types are also used to support [request and result action methods]. In this case, the result type should indicate success/failure as well as the reasons for failure. When indicating these reasons it is better to use a series of named boolean flag properties than it is to use an enumerated type.

[functions]: SideEffectFreeFunctions.md
[request and result action methods]: StateChangingActions.md#request_result