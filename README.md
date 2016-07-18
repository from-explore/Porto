# Porto (Software Architectural Pattern)

![](https://s31.postimg.org/v0tfzzevf/Porto_Logo.png)


<br>

- [Introduction](#Introduction)
- [Quality Attributes](#Quality-Attributes)
- [Request Life Cycle](#Request-Life-Cycle)
- [Diagrams](#Diagrams)
- [Full Documentation](#Full-Documentation)
	- [Port Layer](#Port-Layer)
	- [Containers Layer](#Containers-Layer)
- [Projects](#Projects)
- [Credits](#Credits)



<a id="Introduction"></a>
## Introduction

**Porto** is a modern Software Architectural Pattern, designed to help developers organize their Code in a super maintainable way.

It is very helpful for big and long term projects, as these projects tend to have higher complexity with time.

Porto is inspired by the DDD (Domain Driven Design) and the MVC (Model View Controller) patterns.
It adapts techniques from multiple architectures (Layered, Clean, Service Oriented and Modular). 
And it adheres to the most convenient design principles (SOLID, LIFT, Generalization, GRASP and more).



In Porto, the Interfaces (Web, API, Cli) are appendices to the Application. Whereas, the central organizing principle of the Application is the Actions (Use Cases) that your Application provides.


**Porto is Laravel 5 friendly :)**







<a id="Quality-Attributes"></a>
## Quality Attributes

- Reusable Code (Containers of Business Logic).
- Easy to understand by any developer (less magic, more readable code).
- Fast Development.
- Decoupled Code (editing this doesn’t break that).
- Organized Code base.
- Easy Maintenance (easy to adapt changes).
- Easy to Test (test driven).
- Zero Technical debt (low communication between Developers).
- Zero Code Decoupling.
- Scalable Code (easy to modify and implement features).
- Easy Framework Upgrade.
- Simple folders structure. (easy to locate anything and everything).
- Clean and clear development workflow.



<a id="Request-Life-Cycle"></a>
## Request Life Cycle

*In a typical scenario:*

1. `User` calls an Endpoint *(defined in a `Route` file)*.
2. `Endpoint` calls a `Controller`.
3. (`Request` injected in the `Controller` automatically applies the request validation rules).
4. `Controller` run a `Action` and pass the `Request` data to it.
5. `Action` run multiple `Services` (passing data from one to another).
6. `Services` performs the business logic (can also call `Services`).
7. `Services` returns result data to the `Action`.
8. `Action` returns the collected results data to the `Controller`.
9. `Controller` builds the response and send it back to the `User`.




<a id="Diagrams"></a>
## Diagrams


Diagrams coming soon..




<a id="Full-Documentation"></a>
## Full Documentation

Porto consists of 2 Layers only the `Containers`, and the `Port`. In addition to a set of `Components` with predefined responsibilities.



<br>
<a id="Port-Layer"></a>
### Port (Layer)

> Be happy, you do not have to touche the Port layer :)

The Port is just a fancy name for the **Kernel**. It is the engine of the Containers Components. Almost all the Containers Components MUST extend or inherit from the Port layer.

The Port plays an important role in separating the Application code from the Framework code. And it holds most of the common jobs that should be applied to all Containers Components.

In general you should not add any business logic or application specific code in the Port. However, in some case you might have to add some code there such as (example: Middleware, Exception, Test,...) if they are reusable by almost all the Containers and doesn't make sense to live a one Container.

The Port, facilitates upgrading the Framework without affecting the Application code.




<br>
<a id="Containers-Layer"></a>
### Containers (Layer)

The Containers layer is where the Application specific business logic is written. *(Application functionalities)*. The Container wraps the related Components in one place. *Example in a TODO App the Task would be a Container and the User would be another Container, each has it's own Routes, Controllers, Models, and so on..*

The Container consist of Components such as:

Routes - Controllers - Models - Actions - Services - Views - Requests - Middlewares - Commands - Repositories - Providers - Events - Exceptions - Jobs - Listeners - Policies - Contracts - Criterias - Transformers - Migrations - Seeders - Factories - Languages - Assets - Tests - Consoles...

Each Container can have only the Components it needs.

A typical Container folder structure looks like this:

```
Container
	├── Actions
	├── Services
	├── Models
	├── Events
	├── Exceptions
	├── Contracts
	├── Tests
	│   └── Unit
	├── Database
	│   ├── Migrations
	│   └── Seeders
	├── Settings
	│   ├── Providers
	│   ├── Factories
	│   └── Repositories
	└── UI
	    ├── API
	    │   ├── Routes
	    │   ├── Controllers
	    │   ├── Requests
	    │   ├── Pilicies
	    │   ├── Transformers
	    │   └── Tests
	    │       └── Functional
	    ├── CLI
	    │   ├── Commands
	    │   ├── Controllers
	    │   └── Tests
	    │       └── Functional
	    └── WEB
	        ├── Routes
	        ├── Controllers
	        ├── Requests
	        ├── Views
	        └── Tests
	            └── Acceptance
```


<a id="Container-Components"></a>
#### Components

The Components documentations are merged with the [Hello API](https://github.com/Mahmoudz/Hello-API) project documentation. 
Click on the links below to read them. 

**Note:** you just need to read the `Definition`, `Porto Principles` and the `Folder Structure` sections from each Component page, everything else is related to Hello API.

- [Routes](https://hello-api.readme.io/docs/routes)
- [Controllers](https://hello-api.readme.io/docs/controllers)
- [Actions](https://hello-api.readme.io/docs/actions)
- [Services](https://hello-api.readme.io/docs/services)
- [Models](https://hello-api.readme.io/docs/models)
- [Views](https://hello-api.readme.io/docs/views)
- [Providers](https://hello-api.readme.io/docs/providers)
- [Requests](https://hello-api.readme.io/docs/requests)
- [Repositories](https://hello-api.readme.io/docs/repositories)
- [Criterias](https://hello-api.readme.io/docs/criterias)
- [Tests](https://hello-api.readme.io/docs/tests)
- [Exceptions](https://hello-api.readme.io/docs/exceptions)
- [Migrations](https://hello-api.readme.io/docs/migrations)
- [Transformers](https://hello-api.readme.io/docs/transformers)
- [Events](https://hello-api.readme.io/docs/events)
- [Middlewares](https://hello-api.readme.io/docs/middlewares)
- [Policies](https://hello-api.readme.io/docs/policies)
- [Factories](https://hello-api.readme.io/docs/factories)
- [Seeders](https://hello-api.readme.io/docs/seeders)

<!--
	- [Jobs](https://hello-api.readme.io/docs/jobs)
	- [Commands](https://hello-api.readme.io/docs/commands)
	- [Consols](https://hello-api.readme.io/docs/consols)
-->


#### Interactions between Containers
- A Container MAY depend on one or many other Containers.
- A Controller MAY run Services from another Container (But cannot run Actions of other Containers).
- A Model MAY have relationship with a Model from other Containers.


#### Create a Container
Create a new folder in the Containers folder and name it anything you like. The Port will load and register everything  automatically for you (such as Routes, Service Providers,...).

For the autoloading to work flawlessly you MUST adhere to the Component's naming conventions and structure. *(Example: if you want to add a Controller you MUST place it on the root of a Controllers folder inside the Container folder)*. 

You need to read the documentation page of every Component before creating it and making sure you follow the exact folder structure shown in the documentation.


#### Container naming convention
Container MAY be named anything. 
However, for a good practice you MAY name it like the most important model in the current feature you are building. 

Example: if the User Story is (User can create a Stores and Stores can have Items) then we you could have 3 Containers (User, Store and Item).





<a id="Projects"></a>
## Projects

> Ready to see it in action!

- Build API-Centric Apps with [**Hello API**](https://github.com/Mahmoudz/Hello-API) *(an API starter)*.




<a id="Credits"></a>
## Credits

| Authors      | Twitter                                           | Site                      | Contact         |
|--------------|---------------------------------------------------|---------------------------|-----------------|
| Mahmoud Zalt | [@Mahmoud_Zalt](https://twitter.com/Mahmoud_Zalt) | [zalt.me](http://zalt.me) | mahmoud@zalt.me |


