### Loading Application Context Elsewhere
- For context, we can saw how context is loaded in [[Application Test Class]] 
### JUnit4
- We can load the Spring application context for a specific class with `SpringJUnit4CLassRunner`
	- Support integration testing
	- Loads application context for a JUnit test
	- Handles autowiring all beans into the test class
- Given a test class, use the following annotations: 
	- `@RunWith(SpringJunit4ClassRunner.class)` 
		- enable integration test
	- `@ContextConfiguration(class=Clazz.class`
		- Specifies how to load the application context
- What is missing?
	- It doesn't load everything
	- You do not have access for things like application.properties
#### SpringApplicationConfiguration
- Instead of using `@ContextConfiguration(class=Clazz.class)`, you can use `@SpringApplicationConfiguration(class=Clazz.class)` instead
- This will load the application just like normal
### JUnit5
* You can use the `@SpringJunitConfig` which combines `@ExtendWith(SpringExtension.class) and @ContextConfiguration`
### Autowiring
- You can autowire fields of interest in the test class when you have one of the above setup