### About
* Annotation indicates that this class is a source of bean definitions
* You can use `@Bean` annotation on methods in this class
	* Used to define inter-bean dependencies
* Example:
```java
@Configuration
public class AppConfig {

	@Bean
	public MyServiceImpl myService() {
		return new MyServiceImpl();
	}
}
```
### Importing
* Just like in XML where you can import other XML files containing beans, you can use the `@Import(Clazz.class)` annotation at the class level
