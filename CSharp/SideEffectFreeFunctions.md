# Side-effect-free functions
A function is [a type of method] to use in your domain logic. Functions represent *a question or query* about the application. In human language this could be something like:

* Get a list of this user's past purchases
* Is this user eligible for this named promotional discount

Importantly, function names *should not imply side effects*. That is, they get the answer to a question, without changing anything about the application state.

## Dealing with complex parameters
Most functions need parameters but it is also important to avoid *parameter bloat*. Functions with large numbers of parameters are difficult to work with and maintain, because any change to those parameters impacts many upstream usages. Here are some strategies to help mitigate this risk.

### Avoid adding parameters
If you find yourself wanting to add parameters to an existing function then it is likely that you are in fact changing *what the function does*. This should be avoided.

Instead, prefer keeping the original function the same and creating a new [single responsibility interface] with a new higher-order function. This would reuse the existing function (unchanged) and also add the new functionality.

### Wrap multiple parameters in a request type
Where functions require large amounts of informationv which would be spread across many parameters, it is a good idea to create a [a request type] which wraps all of those.

The barrier to doing this should be quite low - it is recommended for any function which requires more than four parameters.

### Split up large functions
If a function requires many parameters (such as within a request type) then it is a good idea to split its functionality up into many smaller functions, each of which requiring onlya subset of the parameters. The 'large' function with many parameters then becomes only a coordinator for these low-level functions.

## Dealing with complex outputs
Function return types should be one of the following:

* An object instance (or null). This could be:
    * An entity
    * A value type
    * A primitive
* A collection (such as `IList<T>`) of any of the above
* [A result type]

In short, when a function's output is complex, create a result type to represent that output. Functions should not return tuples or other complex types which have no 'domain meaning'.

[a request type]: RequestAndResultTypes.md#Request-types
[a result type]: RequestAndResultTypes.md#Result-types

## Examples
These two examples match the human-language examples given at the beginning of this page. They have been contained within [single responsibility interfaces] to provide some context.

```csharp
public interface IGetsPastOrdersForUser
{
    IReadOnlyList<Order> GetPastOrders(User user);
}

public interface IGetsUsersEligibilityForPromotion
{
    bool IsUserEligible(User user, Promotion promotion);
}
```
[a type of method]: MethodDesign.md
[single responsibility interfaces]: SingleResponsibilityInterfaces.md