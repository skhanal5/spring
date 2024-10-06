### About
* `AnnotationConfigApplicationContext` lets you define `@Configuration` and `@Component` classes as input
* Everything in `@Configuration` class are registered as beans
	* including the `@Bean` annotated methods
* Example:
```java
public static void main(String[] args) {
	ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
	MyService myService = ctx.getBean(MyService.class);
	myService.doStuff();
}
```
### Component Scanning
* Annotate your `@Configuration` class with `@ComponentScan(basePackage="..."`
	* Looks for any `@Component` classes and register them as bean definitiosn