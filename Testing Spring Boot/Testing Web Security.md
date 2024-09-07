### Scenario
- Follow up from [[Testing Web Applications]]
- What if you want to test how secure your endpoints are?
### Spring Security Test
- Import the dependency for this
- When building your `MockMvc` you can use this method `apply(springSecurity())` 
	- returns a Mock MVC configurer that enables security
### Helper Annotations
* `@WithMockUser`
	* Loads security context
	* You can pass in authorization details
* `@WithUserDetails`
	* Can lookup a particular user
* Annotate methods with these