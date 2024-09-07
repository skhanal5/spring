#### Scenario
- If you have a configuration specific to a part of the application (.e.g., a controller), 
### Injecting Configuration Properties
you can use the  `@ConfigurationProperties` annotation on a class and pass in a `prefix=value`
	- You will need to provide an instance field and a  setter method for that config
	- Now this configuration can be passed into your application.properties file and be picked up accordingly in that class
	- prefix might be `amazon`, and the full property `amazon.client-id=...`
### Configuration Properties in a Bean
* **Why?** This makes your application more modularized, separation of powers is a good thing
* Define a class with the properties, e.g. `AmazonProperties`
* Pass in the `@ConfigurationProperties` annotation and the `@Component` annotation
* Make the fields, setter/getters
* Wherever you need that property, just use `@Autowired` and pass it in as a parameter