# The domain API project
Almost every software solution should have a project for the **Domain API**.

## Purpose
To declare *the business functionality* that the solution provides. That is - this project defines **what** the solution can do, without any reference as to **how** it is done.

## Project references
Generally, the domain API project should have no references/dependencies upon any other project in the solution. Conversely, any other project in the solution is allowed to reference/depend-upon the domain API project.

## Naming
The domain API project should be named with a convention such as **[SolutionName].Domain**, for example `MomsRobots.Domain`.

The **root namespace** for this project should be just the solution name. Following the previous example, it would be just `MomsRobots`.

## Contents
The contents of the domain API project should be limited to:
* **[Single Responsibility Interfaces]** for actions and queries which have *a business meaning*.

[Single Responsibility Interfaces]: SingleResponsibilityInterfaces.md