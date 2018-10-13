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
The single method exposed by the interface should be classified as either **a function** which gets/queries some information without implying that it will change anything or it should be **an action** which instructs the application to change something.

The names "function" and "action" happen to be similarly-named to the C# built-in delegates `Func<T>` and `Action<T>` but they are otherwise *unrelated*.

### Functions
A function is *a question or query* about the application. In human language this could be something like:

* Get a list of this user's past purchases
* Is this user eligible for this named promotional discount

Importantly, function names *should not imply side effects*. That is, they get the answer to a question, without changing anything about the application state.

Here are the two examples above, designed as single responsibility interfaces.

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

### Actions 
Unlike a function, an action *makes a change to the state of the application*.

#### Returning values from actions
Often, action methods will have a return type of `void`, but sometimes they may return 'response' or 'result' information.

When designing such a method, consider the following. *Could calling code meaningfully expect the action to fail and could it meaningfully deal with a failure?* If a failure is not meaningfully expected them the method should return `void`; any failures would result in the raising of an exception.

If in the other hand a failure is expected (as part of normal application operation), and the calling code would be expected to deal with such a failure, then a **request/response** design would be superior. The response object would contain information about the success/failure of the action.

#### Examples
Examples of actions might be as follows:

* Save a user's shopping basket
* Add a drop-off to a delivery vehicle's schedule

In these examples, saving a shopping basket is unlikely to require a return value (see above). In an application it's very unusual for a 'save' operation to fail because of meaningful business rules which calling code could deal with.

On the other hand, it's feasible that adding to a delivery vehicle's schedule could fail for business rules. Perhaps it's not servicing that area today, perhaps its schedule is already full and so on. This second method could reasonably be structured as a request/response.

```csharp
public interface ISavesShoppingBasket
{
    void Save(ShoppingBasket basket);
}

public interface IAddsToDeliveryVehicleSchedule
{
    AddToDeliveryScheduleResult AddToVehicleSchedule(DeliveryVehicle vehicle, ScheduledDelivery delivery);
}
```