# Porto (Software Architectural Pattern)

![](https://s31.postimg.org/v0tfzzevf/Porto_Logo.png)

<br>

- [Introduction](#Introduction)
- [Quality Attributes](#Quality-Attributes)
- [Layers](#layers)
	- [Layers Diagram](#Layer-Diagram)
	- [Port Layer](#Port-Layer)
	- [Containers Layer](#Containers-Layer)
		- [Structure](#Containers-Structure)
		- [Interactions](#Containers-Interactions)
		- [Example](#Containers-Example)
- [Components Categories](#Components-Categories)
	- [Class A](#Class-A-Components)
		- [Components Interaction Diagram](#Components-Interaction-Diagram)
		- [Request Life Cycle](#Request-Life-Cycle)
	- [Class B](#Class-B-Components)
	- [Class C](#Class-C-Components)
- [Components](#Components-Details)
	- [Routes](#Routes)
	- [Controllers](#Controllers)
	- [Requests](#Requests)
	- [Actions](#Actions)
	- [Tasks](#Tasks)
	- [Models](#Models)
	- [Views](#Views)
	- [Transformers](#Transformers)
	- [Repositories](#Repositories)
	- [Exceptions](#Exceptions)
	- [Criterias](#Criterias)
	- [Policies](#Policies)
	- [Tests](#Tests)
	- [Providers](#Providers)
	- [Events](#Events)
	- [Migrations](#Migrations)
	- [Seeders](#Seeders)
	- [Factories](#Factories)
	- [Middlewares](#Middlewares)
- [Projects](#Projects)
- [Feedback & Questions](#Feedback)
- [Credits](#Credits)



<a id="Introduction"></a>
# Introduction

**Porto** is a modern Software Architectural Pattern, designed to help developers organize their Code in a super maintainable way.

It is very helpful for big and long term projects, as these projects tend to have higher complexity with time.

Porto is inspired by the DDD (Domain Driven Design) and the MVC (Model View Controller) patterns.
It adapts techniques from multiple architectures (Layered, Clean, Task Oriented and Modular). 
And it adheres to the most convenient design principles (SOLID, LIFT, Generalization, GRASP and more).


In Porto, the Interfaces (WEB, API, CLI) are appendices to the Application Logic. And the Actions (Features) are the central organizing principle.



<a id="Quality-Attributes"></a>
# Quality Attributes

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
- Easy to locate anything and everything.
- Avoid bloated Classes and unmaintainable code.
- Clean and clear development workflow.




<a id="layers"></a>
# Layers

Porto consists of two layers the `Containers` and `Port`. 
And a set of `Components` with predefined responsibilities.

<a id="Layers-Diagram"></a>
## Layers Diagram

![](https://s9.postimg.org/tl2oum7r3/porto_layers.png)


<br>
<a id="Port-Layer"></a>
## Layer : Port

The Port is just a fancy name for the **Kernel**. It is the engine of the Containers Components. Almost all the Containers Components MUST extend or inherit from the Port layer.

The Port plays an important role in separating the Application code from the Framework code. And it holds most of the common jobs that should be applied to all Containers Components.

In general, you should not add any business logic or application specific code in the Port. However, in some case you might have to add some code there such as (example: Middleware, Exception, Test,...) 
if they are reusable by almost all the Containers and they doesn't make sense to live in a one Container.

The Port, facilitates upgrading the Framework without affecting the Application code.




<br>
<a id="Containers-Layer"></a>
## Layer : Containers

The Containers layer is where the Application specific business logic is written. 
*(Application functionalities)*. 
The Container wraps the related Components in one place. 

*"Example in a TODO App the Task would be a Container and the User would be another Container, each has it's own Routes, Controllers, Models, and so on.."*


<a id="Containers-Structure"></a>
### Containers Structure:

```
Container 1
	├── Actions
	├── Tasks
	├── Models
	└── UI
	    ├── WEB
	    │   ├── Routes
	    │   ├── Controllers
	    │   └── Views
	    ├── API
	    │   ├── Routes
	    │   ├── Controllers
	    │   └── Transformers
	    └── CLI
	        ├── Commands
	        └── Controllers

Container 2
	├── Actions
	├── Tasks
	├── Models
	└── UI
	    ├── WEB
	    │   ├── Routes
	    │   ├── Controllers
	    │   └── Views
	    ├── API
	    │   ├── Routes
	    │   ├── Controllers
	    │   └── Transformers
	    └── CLI
	        ├── Commands
	        └── Controllers
```


<a id="Containers-Interactions"></a>
### Interactions between Containers
- A Container MAY depends on one or many other Containers.
- A Controller MAY run Tasks And Actions from another Container.
- A Model MAY have a relationship with a Model from other Containers.


<a id="Containers-Example"></a>
### Typical Full Container Example:

```
Container
	├── Actions
	├── Tasks
	├── Models
	├── Events
	├── Pilicies	
	├── Exceptions
	├── Contracts
	├── Providers
	├── Tests
	│   └── Unit
	├── Data
	│   ├── Migrations
	│   ├── Seeders
	│   ├── Factories
	│   ├── Criterias
	│   └── Repositories
	└── UI
	    ├── API
	    │   ├── Routes
	    │   ├── Controllers
	    │   ├── Requests
	    │   ├── Transformers
	    │   └── Tests
	    │       └── Functional
	    ├── WEB
	    │   ├── Routes
	    │   ├── Controllers
	    │   ├── Requests
	    │   ├── Views
	    │   └── Tests
	    │       └── Acceptance
	    └── CLI
	        ├── Commands
	        ├── Controllers
	        └── Tests
	            └── Functional
```



<br>
<a id="Components-Categories"></a>
# Components Categories


Every Container consist of a number of Components, in **Porto** the Components are splitted into three categories based on their importance:
`Class A Components`, 
`Class B Components` and
`Class C Components`.

<a id="Class-A-Components"></a>
## Class A Components:

They are the main Components. (You must use them for almost all types of Apps):

Routes - Controllers - Requests - Actions - Tasks - Models - Views - Transformers.

> **Views:** should be used in case the App serves HTML pages.
> <br>
> **Transformers:** should be used in case the App serves JSON data.




<a id="Components-Interaction-Diagram"></a>
### Class A Components Interaction Diagram


![](https://s4.postimg.org/nqenznt25/porto_container.png)




<a id="Request-Life-Cycle"></a>
### Request Life Cycle

*In a typical scenario:*

1. `User` calls an Endpoint in the `Route` file.
2. `Endpoint` calls its `Controller` function.
3. `Request` injected in the `Controller` automatically applies the request validation/authrization rules.
4. `Controller` calls an `Action` and pass the `Request` data to it.
5. `Action` performs the business logic or calls `Tasks`.
6. `Tasks` performs the shared business logic between multiple `Actions`.
7. `Action` returns data to the `Controller`.
8. `Controller` builds the response (using `View` or `Transformer`) and send it back to the `User`.




<a id="Class-B-Components"></a>
## Class B Components:

They are optional but highly recommended Components. (You should use them as they give a lot of goodies):

Repositories - Exceptions - Criterias - Policies - Tests.

<a id="Class-C-Components"></a>
## Class C Components:

They are completely optional Components. (You can use them only when you need them, based on your App needs):

Middlewares - Task Providers - Events - Commands - DB Migrations - DB Seeders - Data Factories - Contracts...



<br>


<a id="Components-Details"></a>
# Components

Below is the explanation of the roles, usage and principles of each Component.




<a id="Routes"></a>
## A : Routes
 
Routes are the first receivers of the HTTP requests.

The Routes are responsible for mapping all the incoming HTTP requests to their controller's functions.

The Routes files contain Endpoints (URL patterns that identify the incoming request).

When an HTTP request hits your Application, the Endpoints match with the URL pattern and make the call to the corresponding Controller function.

#### Principles:
- There are two types of Routes, API Routes and Web Routes.
- The API Routes files SHOULD be separated from the Web Routes files, each in its own folder.
- The Web Routes folder will contain only the Web Endpoints, (accessible by Web browsers); And the API Routes folder will contain only the API Endpoints, (accessible by any consumer App).
- Every Container SHOULD have its own Routes.
- A single Route file MAY contain multiple Endpoints.
- The Endpoint job is to call a function on the corresponding Controller once an HTTP request is made. (It SHOULD NOT do anything else).


<a id="Controllers"></a>
## A : Controllers

Controllers are responsible for serving the request data and building responses.

The Controllers concept is the same as in MVC *(They are the C in MVC)*, but with limited and predefined responsibilities.

#### Principles:
- Controllers SHOULD NOT know anything about the business logic or about any business object.
- A Controller SHALL only does the following jobs:
   1. Reading a Request data (user input)
   2. Calling an Action (and passing request data to it)
   3. Building a Response (MAY build response based on the data collected from the Action call)
- Controllers SHOULD NOT have any form of business logic. (It SHOULD call an Action to perform the business logic).
- Controllers SHOULD NOT call Container Tasks. They MAY only call Actions. (And then Actions can call Container Tasks).
- Controllers MUST only be called by Routes Endpoints only.
- Every Container UI folder (Web, API, CLI) will have its own Controllers, so in a typical Container, you might have three Controllers.



<a id="Requests"></a>
## A : Requests

Requests mainly serves the user input in the application. And they are very useful to automatically apply the Validation and Authorization rules.

Requests are the best place to apply validations, since the validations rules will be related to every request. Without a Request class you can define multiple sets of validation rules in your Model (CreateValidation, UpdateValidation,..) to manually apply the validation from Controllers before every function. But with Request classes all this job will be automated, in addition to that the Request can also check of Authorization (check if this user has access to this controller function). Example: check if this user own that product before deleting it, or check if this user is admin to do edit something.

#### Principles:
- A Request MAY hold the Validation / Authorization rules.
- Requests SHOULD only be injected in Controllers. Once injected they automatically check if the request data matches the validation rules, and if the request input is not valid an Exception will be thrown.
- Requests MAY also be used for authorization, they can check if the user is authorized to make a request.



<a id="Actions"></a>
## A : Actions

Actions represent the Use Cases of the Application *(the actions that can be taken by a User or a Software in the Application)*. 

Actions do not hold business logic. They orchestrate the Tasks to perform the business logic of the Application.

Actions take Data Structures as inputs, manipulates them according to the business rules through the Tasks and output a new Data Structures.

Actions SHOULD NOT care how the Data is gathered, how it is manipulated or how it will be represented.

By just looking at the Actions folder of a Container, you can determine what Use Cases this Container provides. And by looking at all the Actions you can tell what your Application can do.

#### Principles:
- Every Action SHOULD be responsible for doing a single Use Case in the Application.
- An Action MAY call multiple Tasks. (They can even call Tasks from other Containers as well).
- An Action MAY retrieves data from Tasks and pass data to another Task.
- Actions MAY return data to the Controller.
- Actions SHOULD NOT return a response. (the Controller job is to return a response).
- An Action SHOULD NOT call another Action. Because this doesn't make logical sense.
- Actions are mainly used from Controllers. However, they can be used from Events, Commands or other Classes. But they SHOULD NOT be used from other Actions or from Tasks.
- Every Action SHOULD have only a single function named `run()`.


<a id="Tasks"></a>
## A : Tasks

The Tasks are the classes that holds the business logic. 
Every Task is responsibile for little part of the logic.


#### Principles:
- Every Task SHOULD have a single responsibility (job).
- An Action MAY receive and return Data. (Actions SHOULD NOT return a response, the Controller job is to return a response).
- A Task SHOULD NOT call another Task. Because that will cause a big mess.
- A Task SHOULD NOT call an Action. Because your code wouldn't make logical sense.
- Tasks are mainly called from Actions. (They could be called from Actions of other Containers as well).
- A Task may contain more than one function but the functions must be logically related and explicitly named "example: `FindUserTask` can have 2 functions `byId` and `byEmail`". In case a Task has a single function it can be named `run`.
- A Task SHOULD NOT be called from Controller. Because this leads to non-documented feature in your code. It's ok to have a lot of Actions "example: `FindUserByIdAction` and `FindUserByEmailAction` where both Actions are calling different functions of the same Task".


<a id="Models"></a>
## A : Models

The Models provide an abstraction for the data, they represent the data in the database. *(They are the M in MVC)*.

Models are responsible for how the data should be handled. They make sure that data arrives properly into the backend store (e.g. Database).

#### Principles:
- A Model SHOULD NOT hold business logic, it can only hold the code and data the represents itself. *(it's relationships with other models, hidden fields, table name, fillable attributes,...)*
- A single Container MAY contains multiple Models.
- Model MAY define the Relations between itself and any other Models (in case a relation exist).



<a id="Views"></a>
## A : Views

Views contain the HTML served by your application. 

Their main goal is to separate the application logic from the presentation logic. *(They are the V in MVC)*.

#### Principles:
- Views can only be used from the Web Controllers.
- View SHOULD be separated into multiple files and folders based on what they display.
- A single Container MAY contains multiple Views files.


<a id="Transformers"></a>
## A : Transformers

Transformers (are the short name for Responses Transformers). 

They are the same like Views but for JSON Responses. While Views takes data and represent it in HTML, Transformers takes data and represent it in JSON.

Transformers are classes responsible for transforming Models into an Arrays.

Transformers takes a Model or a group of Models "Collection" and converts it to a formatted serializable Array.


#### Principles:
- All API responses MUST be formatted via a Transformer.
- Every Model (that gets returned by an API call) SHOULD have a Transformer.
- Contain MAY have multiple Transformers.
- Usually every Model would have a Transformer.










<br>
<br>











<a id="Repositories"></a>
## B : Repositories

The Repository classes are an implementation of the Repository Design Pattern.

Their major roles are separating the business logic from the data (or the data access Task).

Repositories saves and retrieves Models to/from the underlying storage mechanism.

The Repository is used to separate the logic that retrieves the data and maps it to a Model, from the business logic that acts on the Model.


#### Principles:
- Every Model SHOULD have a Repository.
- A Model SHOULD always get accessed through its Repository. (Never direct access to Model).




<a id="Exceptions"></a>
## B : Exceptions

`Exceptions` are classes the handles errors, and helps developers debug their code in a more efficient way.

#### Principles:
- Exceptions can be thrown from anywhere in the application.
- Exceptions SHOULD be created inside the Containers. However, general Exceptions SHOULD be created the Port layer.





<a id="Criterias"></a>
## B : Criterias

Criterias are classes used to hold and apply query condition when retrieving data from the database through a Repository.

Without using a Criteria class, you can add your query conditions to a Repository or to a Model as scope. But with Criterias, your query conditions can be shared across multiple Models and Repositories. It allows you to define the query condition once and use it anywhere in the App.


#### Principles:

- Every Container MAY have its own Criterias. However, shared Criterias SHOULD be created in the Port layer.
- A Criteria MUST not contain any extra code, if it needs data, the data SHOULD be passed to it from the Actions or the Task. It SHOULD not run (call) any Task for data.



<a id="Policies"></a>
## B : Policies

Policies are used to group authorization logic based on the resource they authorize.

Without using a Policy class, you will have to write your authorization code in the Request class. But this will make the Request looks ugly, and won't allow you to reuse the authorization code. 

When using a Policy you can simply and easily apply authorization code in any request, with a simple good looking syntax code. Since every Policy will be linked to their Model using Task Providers.

Policy authorization example: check if this user owns that product before deleting it, or check if this user is an admin to do manage products.

#### Principles:
- A Container MAY have more than one Policy.
- Policies SHOULD mainly be used in the Requests because one of the Request jobs is to check the Authorization.



<a id="Tests"></a>
## B : Tests

Tests classes are created to test the Application classes are working as expected.

The two most essential Tests types for this architecture are the Unit Tests and the Functional Tests. However, Integration and Acceptance Tests can be used as well.

#### Principles:
- Containers MAY be covered by all types of Tests.
- Use Functional Tests to test Container Routes are doing what's expected from them.
- Use Unit Tests to test Container Actions and Tasks are doing what's expected from them.








<br>
<br>









<a id="Providers"></a>
## C : Providers

Providers (are short names for Task Providers).

Task providers are the central place of configuring and bootstrapping a Container.

They are the place where you register things such as container bindings, event listeners, middleware, routes... to the framework Task container.

#### Principles:
- A Container MAY have one or many Providers and MAY have no Provider at all.
- There are 2 types of Providers in a Container, the Main Provider, and the Additional Providers.
- The Main Task Provider: this is the Task Provider that is named after its Container
(Example in a Car Container it will be named CarServiceProvider).
- The Additional Task Providers: any additional Providers in the Container. (Example PoliciesServiceProvider or EventsServiceProvider).
- The Main Provider is responsible for registering the Additional Providers.
- The Main Provider will be auto registered in the framework by the Port layer.
- In case a Provider needs to be used in a Container, the Container MUST have a Main Provider first. Then the main Provider job is to load the additional Providers in the Container (Events Provider, Policies Provider,...).




<a id="Events"></a>
## C : Events

Events provide a simple observer implementation, allowing you to subscribe and listen for events in your application. 

#### Principles:
- A Container MAY have more than one Events.
- Events can be fired from other Containers.




<a id="Migrations"></a>
## C : Migrations

Migrations (are the short name for Database Migrations). 

Migrations are the version control of your database. They are very useful for generating and documenting the database tables.

#### Principles:
- Migrations SHOULD be created inside the Containers folders.




<a id="Seeders"></a>
## C : Seeders

Seeders (are a short name for Database Seeders). 

Seeders are classes that seed the database with data, this data might need to exist in the application after its installation (example: Roles and Permissions with Default Users types).


#### Principles:
- Seeders SHOULD be created in the Containers.
- Packages seeders SHOULD be placed in their own Containers unless they belong to an existing Container.




<a id="Factories"></a>
## C : Factories


Factories (are a short name for Models Factories). 

Factories are used to generate some fake data with the help of Faker to be used for testing purposes.

Factories are mainly used from Tests.

#### Principles:
- Factories SHOULD be created in the Containers.





<a id="Middlewares"></a>
## C : Middlewares


You can enable and disable Middlewares as you wish.

#### Principles:
- There's two types of Middlewares, General (applied on all the Routes by default) and Endpoints Middlewares (applied on some Endpoints).
- The General Middlewares SHOULD be placed in Port layer. While Endpoints Middlewares SHOULD be placed inside the Containers.















<br>
<a id="Projects"></a>
# Projects

> Ready to see the implementions!

- **PHP**
	- [**Hello API**](https://github.com/Mahmoudz/Hello-API) *(is an API starter, allows you to build an API-Centric App quickly)*.




<br>
<a id="Feedback"></a>
# Feedback & Questions

> Your feedback is appreciated.

You have a Feedback, Question or Suggestion? Get in touch, we are on [**Gitter**](https://gitter.im/porto-sap/Lobby), let's have a quick discussion.

[![Gitter](https://badges.gitter.im/porto-sap/Lobby.svg)](https://gitter.im/porto-sap/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)


<br>
<a id="Credits"></a>
# Credits

| Authors      | Twitter                                           | Site                      | Contact         |
|--------------|---------------------------------------------------|---------------------------|-----------------|
| Mahmoud Zalt | [@Mahmoud_Zalt](https://twitter.com/Mahmoud_Zalt) | [zalt.me](http://zalt.me) | mahmoud@zalt.me |


Task