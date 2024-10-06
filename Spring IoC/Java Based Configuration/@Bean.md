### About
* Same functionality as the xml defined bean
* You can use `@Bean` in two places:
	* `@Configuration`  classes
	* `@Component` classes
### Defining a Bean
* Annotate a method with `@Bean`
* This will register the bean with the same type as the methods return value
	* Return type can be an interface as well
* Bean name is the method name by default
* Normal case:
```java
@Configuration
public class AppConfig {

	@Bean
	public TransferServiceImpl transferService() {
		return new TransferServiceImpl();
	}
}
```
* Interface:
```java
@Configuration
public class AppConfig {

	@Bean
	public TransferService transferService() {
		return new TransferServiceImpl();
	}
}
```
### Bean Parameters
* Every parameter in the method call that defines a bean is a direct dependency
* This is equivalent to constructor based dependency injection
	* [[Dependency Injection]]
### Bean Scope
* **IMPORTANT**: Scope is set to singleton by default