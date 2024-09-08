### @MockBean
* Use this anntoation to define a Mockito mock for a bean
* Limitations:
	* Cannot mock a bean that is exercised during application context refresh
		* use a normal bean to configure a mock
### @SpyBean
* Wraps a bean with a `Spy` from Mockito