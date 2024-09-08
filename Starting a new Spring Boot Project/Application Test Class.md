### Test Class
- Comes by default in Spring projects
- Annotated with `@SpringBootTest
* Loads the  full `ApplicationContext` from the main application class
	* [[Application Class]]
* `contextLoads()` function
	* passes if the application context loads
### @SpringBootTest
* Sets up a mock environment for testing web endpoints
	* The real server is NOT started