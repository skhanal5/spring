### Dependency Injection
* Objects define their dependencies (other objects) through:
	* constructor arguments
	* arguments to factory method
	* properties that are set on the object instance after it is made/returned from a factory
### IoC Container
* IoC container injects those dependencies defined above when the bean is created
* Inverse meaning:
	* This is the inverse of the bean itself managing those dependencies
#### Implementation
* `org.springframework.beans` and `org.springframework.context` are foundations for IoC container
* `BeanFactory` is an interface that allows you to manage any object
	* `ApplicationContext` is a sub-interface
* TDLR:
	* `BeanFactory` is the basic configuration
	* `ApplicationContext` adds enterprise level functionality
### Beans
* Beans are objects that are created, assembled, and managed by a Spring IoC container
* Beans are reflected in the configuration data used by the container