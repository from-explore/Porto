# Porto (Software Architectural Pattern)

![](https://s31.postimg.org/v0tfzzevf/Porto_Logo.png)

<br>

- [Introduction](#Introduction)
- [Quality Attributes](#Quality-Attributes)
- [Layers](#layers)
	- [Layers Diagram](#Layer-Diagram)
	- [Ship Layer](#Ship-Layer)
	- [Containers Layer](#Containers-Layer)
		- [Structure](#Containers-Structure)
		- [Interactions](#Containers-Interactions)
		- [Example](#Containers-Example)
- [Components Categories](#Components-Categories)
	- [Main Components](#Main-Components)
		- [Components Interaction Diagram](#Components-Interaction-Diagram)
		- [Request Life Cycle](#Request-Life-Cycle)
	- [Optional Components](#Optional-Components)
- [Main Components Definitions & Principles](#Components-Details)
	- [Routes](#Routes)
	- [Controllers](#Controllers)
	- [Requests](#Requests)
	- [Actions](#Actions)
	- [Tasks](#Tasks)
	- [Models](#Models)
	- [Views](#Views)
	- [Transformers](#Transformers)
- [Container Example](#Container-Example)
- [Projects](#Projects)
- [Feedback & Questions](#Feedback)
- [Credits](#Credits)



<a id="Introduction"></a>
# Introduction

**Porto SAP** is a modern Software Architectural Pattern, designed to help developers organize their Code in a super maintainable way. 
It is very helpful for big and long term projects, as they tend to have higher complexity with time.


> AND IT IS REALLY EASY TO USE.


In Porto, the Interfaces (`WEB`, `API`, `CLI`) are appendices to the Application Logic, while the `Actions` (Features) are the central organizing principle.
At its core it consists of 2 layers (`Containers` & `Ship`), in addition to a set of `Components` with predefined responsibilities, living inside the `Containers` and powered by the `Ship`.

<br>

*Porto was inspired by the DDD (Domain Driven Design) and the MVC (Model View Controller) patterns.
And it adapts techniques from multiple architectures (Layered, Clean, Task Oriented and Modular). 
As well as it adheres to the most convenient design principles (SOLID, LIFT, Generalization, GRASP and more).*



<a id="Quality-Attributes"></a>
# Quality Attributes

- Reusable Business Logic (Containers of Code).
- Easy to understand by any developer (no magic).
- Fast Development of similar type Apps.
- Easy Maintenance (easy to adapt changes).
- Easy to Test (test driven).
- Zero Technical debt (low communication between Developers).
- Decoupled Code (editing X doesn’t break Y).
- Very Organized Code base with Zero Code Decoupling.
- Scalable Code (easy to modify and implement features).
- Easy Framework Upgrade (separation between the App and the Framework).
- Easy to locate anything and everything.
- Avoid bloated Classes and unmaintainable code (S.R.P.).
- Clean and clear development workflow.



<a id="layers"></a>
# Layers

Layers are just folders! And in Porto we only have 2 of them (`Containers` & `Ship`). These folders can be created anywhere inside your framework. 

*(example: in Laravel PHP you can place them in the `app/` directory or create an `src/` directory on the root)*






<a id="Layers-Diagram"></a>
## Layers Diagram


![](https://s19.postimg.org/cgh6yqtn7/porto_layers.png)

#### Visual Image:

![](https://s19.postimg.org/d79x4iw0j/porto_visual_diagram.png)





<br>
<a id="Ship-Layer"></a>
## Layer : Ship

The Ship layer, contains the engine of the Ship which autoloads all the Components of your Containers. 
It can also contain code that can be used by all your Containers Components.

The Ship layer, plays an important role in separating the Application code from the Framework code. 
Thus it facilitates upgrading the Framework without affecting the Application code.



### Ship Strcuture

The Ship, contains 3 folders:

- **Engine**: is the engine that auto-register all your Container's Components and boots your Application.
- **Features**: contains any shared code between multiple Containers. Example, Global Exceptions and Application Middleware's..
- **Parents**: contains the classes for each Component in your Container. (Adding functions to the parent classes makes them avialble in every Container).


Note: All the Container's Components MUST extend or inherit from the Ship layer *(in particular the Parents folder)*.




<br>
<a id="Containers-Layer"></a>
## Layer : Containers

The Containers layer is where the Application specific business logic is written *(Application functionalities)*.

Containers are wrappers of business logic. 

*"Example in a TODO App the Task would be a Container and the User would be another Container, each has it's own Routes, Controllers, Models, and so on.."*

It's advised to use Single Model per Container, however if you want to add more you can easely do this, 
but keep in mind 2 Models means 2 Repositories, 2 factories, 2 of almost everything..! so unless you want to use both Models always together, do split them into 2 Containers.





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
	        ├── Routes
	        └── Commands

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
	        ├── Routes
	        └── Commands
```


<a id="Containers-Interactions"></a>
### Interactions between Containers
- A Container MAY depends on one or many other Containers.
- A Controller MAY run Tasks from another Container.
- A Model MAY have a relationship with a Model from other Containers.


<br>
<a id="Components-Categories"></a>
# Components Categories


Every Container consist of a number of Components, in **Porto** the Components are splitted into two categories:
`Main Components` and
`Optional Components`.



<a id="Main-Components"></a>
## Main Components:

You must use these Components as they are essential for almost all types of Web Apps:

Routes - Controllers - Requests - Actions - Tasks - Models - Views - Transformers.

> **Views:** should be used in case the App serves HTML pages.
> <br>
> **Transformers:** should be used in case the App serves JSON or XML data.


<a id="Components-Interaction-Diagram"></a>
### Main Components Interaction Diagram


![](https://s19.postimg.org/67vv55w2b/porto_container.png)


<a id="Request-Life-Cycle"></a>
### Request Life Cycle

*A typical very basic API call scenario:*

1. **User** calls an `Endpoint` in a `Route` file.
2. `Endpoint` calls a `Middleware` to handle the Authentication.
3. `Endpoint` calls its `Controller` function.
4. `Request` injected in the `Controller` automatically applies the request validation & authrization rules.
5. `Controller` calls an `Action` and pass each `Request` data to it.
6. `Action` calls multiple `Tasks` to perform the business logic, *{or it handles all the job itself}*.
7. `Tasks` performs the business logic (every `Task` does a single portion of the main Action).
8. `Action` collects data from the `Tasks` and returns them to the `Controller`.
9. `Controller` builds the response using a (`View` or `Transformer`) and send it back to the **User**.





<a id="Optional-Components"></a>
## Optional Components:

You can add these Components when you need them, based on your App needs, however some of them are highly recommended:

Repositories - Exceptions - Criterias - Policies - Tests - Middlewares - Service Providers - Events - Commands - DB Migrations - DB Seeders - Data Factories - Contracts - Traits...



<br>


<a id="Components-Details"></a>
# Main Components Definitions & Principles

Below is the explanation of the roles, usage and principles of each Main Component.




<a id="Routes"></a>
## Routes
 
Routes are the first receivers of the HTTP requests.

The Routes are responsible for mapping all the incoming HTTP requests to their controller's functions.

The Routes files contain Endpoints (URL patterns that identify the incoming request).

When an HTTP request hits your Application, the Endpoints match with the URL pattern and make the call to the corresponding Controller function.

#### Principles:
- There are three types of Routes, API Routes, Web Routes and CLI Routes.
- The API Routes files SHOULD be separated from the Web Routes files, each in its own folder.
- The Web Routes folder will contain only the Web Endpoints, (accessible by Web browsers); And the API Routes folder will contain only the API Endpoints, (accessible by any consumer App).
- Every Container SHOULD have its own Routes.
- Every Route file SHOULD contain a single Endpoints.
- The Endpoint job is to call a function on the corresponding Controller once a request of any type is made. (It SHOULD NOT do anything else).


<a id="Controllers"></a>
## Controllers

Controllers are responsible for serving the request data and building responses.

The Controllers concept is the same as in MVC *(They are the C in MVC)*, but with limited and predefined responsibilities.

#### Principles:
- Controllers SHOULD NOT know anything about the business logic or about any business object.
- A Controller SHOULD only do the following jobs:
   1. Reading a Request data (user input)
   2. Calling an Action (and passing request data to it)
   3. Building a Response (usually build response based on the data collected from the Action call)
- Controllers SHOULD NOT have any form of business logic. (It SHOULD call an Action to perform the business logic).
- Controllers SHOULD NOT call Container Tasks. They MAY only call Actions. (And then Actions can call Container Tasks).
- Controllers CAN be called by Routes Endpoints only.
- Every Container UI folder (Web, API, CLI) will have its own Controllers.



<a id="Requests"></a>
## Requests

Requests mainly serves the user input in the application. And they are very useful to automatically apply the Validation and Authorization rules.

Requests are the best place to apply validations, since the validations rules will be related to every request. 
Requests can also check of Authorization to check if this user has access to this controller function. 
*(Example: check if this user own that product before deleting it, or check if this user is admin to do edit something).*

#### Principles:
- A Request MAY hold the Validation / Authorization rules.
- Requests SHOULD only be injected in Controllers. Once injected they automatically check if the request data matches the validation rules, and if the request input is not valid an Exception will be thrown.
- Requests MAY also be used for authorization, they can check if the user is authorized to make a request.



<a id="Actions"></a>
## Actions

Actions represent the Use Cases of the Application *(the actions that can be taken by a User or a Software in the Application)*. 

Actions CAN hold business logic or/and they orchestrate the Tasks to perform the business logic.

Actions take data structures as inputs, manipulates them according to the business rules internally or through some Tasks, then output a new data structures.

Actions SHOULD NOT care how the Data is gathered, or how it will be represented.

By just looking at the Actions folder of a Container, you can determine what Use Cases (features) your Container provides. 
And by looking at all the Actions you can tell what an Application can do.



#### Principles:
- Every Action SHOULD be responsible for doing a single Use Case in the Application.
- An Action MAY retrieves data from Tasks and pass data to another Task.
- An Action MAY call multiple Tasks. (They can even call Tasks from other Containers as well!).
- Actions MAY return data to the Controller.
- Actions SHOULD NOT return a response. (the Controller job is to return a response).
- An Action CAN call another Action (but it's recommended not to do that).
- Actions are mainly used from Controllers. However, they can be used from Events, Commands and/or other Classes. But they SHOULD NOT be used from Tasks.
- Every Action SHOULD have only a single function named `run()`.




<a id="Tasks"></a>
## Tasks

The Tasks are the classes that holds shared business logic between multiple Actions. 

Every Task is responsibile for little part of the logic.

Tasks are optional, but in most cases you find yourself in need for them.

Example: Let's say we have an Action 1 that needs to find a record by its ID from the DB, then fires an Event and pass the record data to it. 
And we have an Action 2 that needs to find the same record by its ID then makes a call to an API and pass the record data to it.
Since both actions are performing the "find a record by ID" job, it would be much better to have a task the does this job and returns that record.

Whenever you see the possiblitiy of reusing a piece of code from an Action, you should put that piece of code in a Task.




#### Principles:
- Every Task SHOULD have a single responsibility (job).
- An Action MAY receive and return Data. (Actions SHOULD NOT return a response, the Controller job is to return a response).
- A Task SHOULD NOT call another Task. Because that will takes us back to the Services Architecture and it's a big mess.
- A Task SHOULD NOT call an Action. Because your code wouldn't make any logical sense then!
- Tasks SHOULD only be called from Actions. (They could be called from Actions of other Containers as well!).
- Tasks usually need a single function `run`. However, if you prefer you can have more than one function, but make sure to explicitly name them "example: `FindUserTask` can have 2 functions `byId` and `byEmail`". 
- A Task SHOULD NOT be called from Controller. Because this leads to non-documented feature in your code. It's totally fine to have a lot of Actions "example: `FindUserByIdAction` and `FindUserByEmailAction` where both Actions are calling the same Task" as well as it's totally fine to have single Action `FindUserAction` making a decision to which Task it should call.


<a id="Models"></a>
## Models

The Models provide an abstraction for the data, they represent the data in the database. *(They are the M in MVC)*.

Models are responsible for how the data should be handled. They make sure that data arrives properly into the backend store (e.g. Database).

#### Principles:
- A Model SHOULD NOT hold business logic, it can only hold the code and data the represents itself. *(it's relationships with other models, hidden fields, table name, fillable attributes,...)*
- A single Container MAY contains multiple Models.
- Model MAY define the Relations between itself and any other Models (in case a relation exist).



<a id="Views"></a>
## Views

Views contain the HTML served by your application. 

Their main goal is to separate the application logic from the presentation logic. *(They are the V in MVC)*.

#### Principles:
- Views can only be used from the Web Controllers.
- View SHOULD be separated into multiple files and folders based on what they display.
- A single Container MAY contains multiple Views files.


<a id="Transformers"></a>
## Transformers

Transformers (are the short name for Responses Transformers). 

They are the same like Views but for JSON Responses. While Views takes data and represent it in HTML, Transformers takes data and represent it in JSON.

Transformers are classes responsible for transforming Models into an Arrays.

Transformers takes a Model or a group of Models "Collection" and converts it to a formatted serializable Array.


#### Principles:
- All API responses MUST be formatted via a Transformer.
- Every Model (that gets returned by an API call) SHOULD have a Transformer.
- A single Container MAY have multiple Transformers.
- Usually every Model would have a Transformer.






<br>





<a id="Container-Example"></a>
## Typical Container Example:

```
Container
	├── Actions
	├── Tasks
	├── Models
	├── Events
	├── Policies	
	├── Exceptions
	├── Contracts
	├── Traits
	├── Providers
	├── Configs
	├── Data
	│   ├── Migrations
	│   ├── Seeders
	│   ├── Factories
	│   ├── Criterias
	│   └── Repositories
	├── Tests
	│   ├── Unit
	│   └── Traits
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
	        ├── Routes
	        ├── Commands
	        └── Tests
	            └── Functional
```






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
