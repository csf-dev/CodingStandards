# Good method design
## Prefer functions & actions
A good method *is ideally one of two things*; either it is a **[side-effect-free function]** or an **[action]**. A function *asks a question* or *gets some information* without implying any side-effects. An action *makes a change* to the state of the application.

> The names "function" and "action" are coincidentally similarly-named to the C# built-in delegates `Func<T>` and `Action<T>`. They are otherwise *unrelated*.

[side-effect-free function]: SideEffectFreeFunctions.md
[action]: StateChangingActions.md

## When functions/actions aren't practical
Sometimes it's impossible or impractical to avoid methods which both get information and change the application. 'Impure' methods like this should be a last resort because they are less reusable than functions and actions.

In these cases, the next best solution is to provide the method's functionality in three parts:

* One or more side-effect-free functions
* An action which makes the change
* A high-level, 'impure' method which coordinates the functions & action

If those component functions/actions are not useful in the application domain (they expose state which is invalid in practical senses) then it's reasonable *not to declare them* at the [domain API level].

[domain API level]: DomainApiProject.md

### Example
An example of an impure method is that of a number sequence generator. Each time the `GetNextNumber` method is called, it increments the sequence, returning a different number each time.

```csharp
int GetNextNumber();
```

This could be improved by providing two additional methods, one function and one action:

```csharp
int PeekNextNumber();
void IncrementSequence();
```

The 'peek' function does not imply that the sequence is modified with each call and the 'increment' action just increments the sequence without getting a number.