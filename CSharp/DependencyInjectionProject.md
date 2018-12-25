# Dependency injection project
The dependency injection (DI) project is used to configure a DI framework (such as **Autofac**) to create and provide *almost every type in the application*.

The DI project should register everything within the [domain implementation project] as well as all [gateway projects]. The *project types for which it cannot (and should not) register types* are [client projects] and, of course, [test projects]. The DI project should be client-neutral & clients need to be able to reference and use the DI project directly.

Because of the above, it is expected that the dependency injection project will reference *most other projects in the solution*.

[client projects]: ClientProject.md
[test projects]: TestAndSpecProjects.md
[client project]: ClientProject.md
[domain implementation project]: DomainImplementationProject.md
[gateway projects]: GatewayProject.md

## How to structure a DI project
Even though dependency injection should be configured centrally, it is [client projects] which actually use it. This means that it should provide an external API which is both *easy to use* and also *extensible*.

### Sample API
Here is a suggestion as to the external interface of a dependency injection project.

```csharp
public interface IGetsDiConfiguration
{
  DiConfiguration GetConfiguration();
}

public interface IGetsDiContainer
{
  DiContainer GetContainer();
}

public class ContainerFactory : IGetsDiContainer
{
  readonly IGetsDiConfiguration configProvider;
  
  public DiContainer GetContainer()
  {
    var config = configProvider.GetConfiguration();
    // Use the config to create and
    // return the container.
  }

  public ContainerFactory(IGetsDiConfiguration configProvider)
  {
    this.configProvider = configProvider;
  }
}
```

Under this example, the types `DiConfiguration` and `DiContainer` should be substituted by *the native configuration/container types* within the chosen DI framework.

The DI project should fully implement the `ContainerFactory` (using the example above as a guide). It should also have a type which implements `IGetsDiConfiguration`.

### Using dependency injection
When a [client project] *uses dependency injection* it should first construct an instance of `IGetsDiConfiguration`. Typically this begins with the configuration provider from the DI project. The client may then extend that, using the **decorator pattern**, to register types which are specific to that client.

Once the final configuration is created, it may be passed to the `ContainerFactory` in order to get a container.