# The domain implementation project
The domain implementation is where the **core business logic** of the application lives.

The main classes in this project should be implementations of interfaces which are declared in [the domain API project].

It is also acceptable to add factories and other services within this project, which are not relevant to appear within the domain API. The advice is to err on the side of declaring everything within the API project though. Classes are more reusable if they have an interface present in the API project.

[the domain API project]: DomainApiProject.md

It is important *not to complicate the domain implementation project* with logic that deals with complex or third party technologies. This code should go instead into [gateway projects].

[gateway projects]: GatewayProject.md