### Scenario
- Instead of loading the full application configuration, it is best to load a slice of the application configuration that is needed for your test
- Use `spring-boot-test-autoconfigure` for this
- Structure:
	- Each annotation in this module has a `@...Test` annotation that loads the `ApplicationContext`
	- But you can use `@AutoConfigure...` to limit the configuration
### Example with Spring MVC
* To test just the MVC controller, use `@WebMvcTest`
	* limits the scanned beans
	* Stuff like `@Component` and `@ConfigurationProperties` is not loaded
* [[Testing Web Applications]] for more detail on this
