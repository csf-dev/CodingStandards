# Side-effect-free functions
A function is [a type of method] to use in your domain logic. Functions represent *a question or query* about the application. In human language this could be something like:

* Get a list of this user's past purchases
* Is this user eligible for this named promotional discount

Importantly, function names *should not imply side effects*. That is, they get the answer to a question, without changing anything about the application state.

## Dealing with complex parameters
It is reasonable for a function to declare a small number of parameters but some functions require a great deal of information in order to correctly perform their work.

* If you are needing to add/change the parameters to an existing function
* If a function requires more than four parameters

In these cases, it is a good idea to encapsulate the parameters within [a request type].

## Dealing with complex outputs
Where a function returns more than a single existing object type (or a collection of objects), that result must be encapsulated within [a result type].

[a request type]: RequestAndResultTypes.md#Request-types
[a result type]: RequestAndResultTypes.md#Result-types

## Examples
These two examples match the human-language examples given above. They have been contained within [single responsibility interfaces] to provide some context.

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