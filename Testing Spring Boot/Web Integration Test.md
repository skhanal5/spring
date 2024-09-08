### Testing with a Running Server
* `@SpringBootTest(webEnvironment=WebEnvironment.RANDOM_PORT)` is what you need 
	* random port is best for testing
* Then just use a `WebTestClient`