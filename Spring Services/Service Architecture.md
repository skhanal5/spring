### About
- A way of abstracting away business logic
	- Recall: your code should only service 1 purpose
### Usage
* Typically you define a base Service interface to expose all the methods that the Service can accomplish
* Why use an interface?
	* Easy to mock during tests
	* Loose coupling
	* Allows you to define new service implementations without breaking existing codebase
* Then you define a corresponding implementation for that Service, usually denoted as `Impl` 
	* This class is usually annotated with `@Service`
* In the method where you intend to use this logic, you can autowire the Service interface
	* See [[@Service]] for more information on how it picks up the implementation
### Resources
1. [Services and Interfaces](https://davidgiard.com/java-services-and-interfaces-in-a-spring-boot-application)