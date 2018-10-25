# Good method design
A good method *is ideally one of two things*; either it is a **[side-effect-free function]** or an **[action]**. A function *asks a question* or *gets some information* without implying any side-effects. An action *makes a change* to the state of the application.

> The names "function" and "action" happen to be similarly-named to the C# built-in delegates `Func<T>` and `Action<T>` but they are otherwise *unrelated*.

[side-effect-free function]: SideEffectFreeFunctions.md
[action]: StateChangingActions.md

## Neither functions nor actions
Sometimes it's impossible to avoid methods which both get information and change the application. 

Creating 'impure' methods like this usually be a last resort, because impure methods are less reusable than functions and actions. Where it cannot be avoided, ensure that a separate side-effect-free function and an action are available which (together) perform the task of the 'impure' method. The impure method then becomes a convenient way to call the function and action together.

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