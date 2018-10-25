# State-changing actions
An action is [a type of method] which is used within your application design, which makes a change to the application's state.

Whereas [functions] ask questions about the state of the application without changing anything, actions often *do not return any information*. Actions might make a change to data in a database, change data on a filesystem, or make an external API call which indicates a chance should be performed upon a remote system.

[a type of method]: MethodDesign.md
[functions]: SideEffectFreeFunctions.md

## A simple example
This is an example of a simple action method definition. It is shown within a [single responsibility interface] to provide some context.

```csharp
public interface ISavesShoppingBasket
{
    void Save(ShoppingBasket basket);
}
```

## <a name="request_result"></a>Request/Result actions
Usually, action methods will have a return type of `void`; when an action is performed, either it succeeds or something is significantly wrong with the application and an exception is raised.

Sometimes it's not appropriate to raise an exception when an action fails. Typically this is when failure is *part of the action's expected behaviour*. In these circumstances, it is more appropriate to design the action using [**request and result objects**] as the method's input/output.

[**request and result objects**]: RequestAndResultTypes.md

### Example
Imagine an application for users to order at a restaurant using pre-paid credit. An action to order a specific item might be *expected to fail* under the following circumstances:

* The kitchen has run out of the ordered item
* The user doesn't have sufficient credit to make the order
* The restaurant is about to close and the kitchen is not accepting new orders

Here's the definition of the corresponding action method, describing the above logic. As with the previous example, the action method itself is shown within a [single responsibility interface].

```csharp
public class OrderItemRequest
{
    public int RemainingCredits { get; set; }
    public Item ItemToOrder { get; set; }
}

public class OrderItemResult
{
    public bool Success { get; set; }
    public bool KitchenIsClosed { get; set; }
    public bool ItemNotInStock { get; set; }
    public bool InsufficientCredit { get; set; }
}

public interface IOrdersItemFromKitchen
{
    OrderItemResult OrderItem(OrderItemRequest request);
}
````

[single responsibility interface]: SingleResponsibilityInterfaces.md