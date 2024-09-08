### Scenario
- Given a controller, how do you test any given endpoint?
- For example:
	- How do you assert the endpoint was triggered?
	- How do you assert the form fields are bound correctly?
	- etc.
### Spring Mock MVC
 * Mocks the servlet container allowing you to test controllers
 * Use `MockMvcBuilders` with the following builder methods
	 * `standaloneSetup()` 
		 * mock one or more controllers
		 * You must inject the controllers
	* `webAppContextSetup()`
		* build Mock MVC using Spring app context
		* Used for integration tests
### WebAppContextSetup
* To use `webAppContextSetup()`, you need to pass in a `WebApplicationContext`
* Use `@WebAppConfiguration` and `@Autowire` an instance of it
	* This annotation creates a `WebApplicationContext` bean
* Then initialize the `MockMvc` using the builder
* From there you can write something like the following (from *Spring Boot in Action*):
```
@Test
public void homePage() throws Exception {
  mockMvc.perform(get("/readingList"))
      .andExpect(status().isOk())
      .andExpect(view().name("readingList"))
      .andExpect(model().attributeExists("books"))
      .andExpect(model().attribute("books", is(empty())));
}
```
