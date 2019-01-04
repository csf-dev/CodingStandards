# Domain entities
Entities are 'things' which have a unique identity within your application. They are often persisted in some way, such as a database. Entities are always **classes** and may have a simple inheritance hierarchy.

## Use an Entity base class
All entity classes must have an identity and related behaviour. In this case it makes sense to use a base class to provide that common functionality.

It is recommended to use the base class available in [CSF.Entities] for this.

[CSF.Entities]: https://github.com/csf-dev/CSF.Entities

## Use virtual properties
For compatibility with ORM software such as [NHibernate], all non-private members of entity classes must be declared `virtual`.

[NHibernate]: http://nhibernate.info/

## Avoid 'business logic' methods
It is possible to place methods and functionality upon entity objects. Beware doing this though, because *the only way in which an entity object's functionality can be extended* is by subclassing.

Because entities should all be declared in [the domain API project], they *should not have any methods which implement business logic*. Instead, declare [a single responsibility interface] for this functionality and implement it in [the domain implementation project].

[the domain API project]: DomainApiProject.md
[a single responsibility interface]: SingleResponsibilityInterfaces.md
[the domain implementation project]: DomainImplementationProject.md

## Entity relationships
### Many to one
Where an entity has a relationship to another (many-to-one), this should be represented using an object reference to that related entity. *Avoid using primitive foreign key values* in entity classes.

For example, if a **CustomerOrder** entity has a related **Customer** entity. This would be written as below and *not* with a `CustomerId` property.

```csharp
public class CustomerOrder
{
    public virtual Customer Customer
    { get; set; }
}
```

### One to many
Where an entity is related to many others (one-to-many) then this should be represented via an appropriate collection of related entity objects.

Consider the collection type and ensure that the appropriate one is used. The two most common are:

* `ISet<TRelated>` - this is a *normal foreign key relationship*.
* `IList<TRelated>` - used if *there is a meaningful order* to the related objects.

The collection itself should be modelled using the the [CSF.Collections.EventRaising] library. Add/remove events should be configured so that *the 'many-to-one side' of the relationship* is automatically updated as items are added/removed to/from the collection.

It is also usually desirable to model these collection relationships as **read-only**, since it is unusual to replace the entire collection with a new instance.

[CSF.Collections.EventRaising]: https://github.com/csf-dev/CSF.Collections.EventRaising

Continuing the many-to-one example above, the one-to-many side of the **CustomerOrder**/**Customer** relationship would be modelled like this.

```csharp
using CSF.Collections.EventRaising;
using System.Collections.Generic;

public class Customer
{
    readonly ISet<CustomerOrder> sourceOrders;
    readonly EventRaisingSet<CustomerOrder> orders;

    public virtual ISet<CustomerOrder> Orders => orders;

    public Customer()
    {
        sourceOrders = new HashSet<CustomerOrder>();
        orders = new EventRaisingSet<CustomerOrder>(sourceOrders);

        orders.SetUpBeforeAfterActions(
            (order) => order.Customer = this,
            (order) => order.Customer = null);
    }
} 
```