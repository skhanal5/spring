### Scenario
- You need different types of configuration for different environments
#### @Profile
- Passing in `@Profile` to something like a `@Configuration` annotated class allows you to conditionally configure that class so it is only used when that profile is active at runtime
	- [[Conditional Configuration]]
### Active Property
- Use `spring.profiles.active` property in your application.properties to define which profile is active at runtime
### Profile Specific Properties File
* You can provide application-{profile}.properties file where profile can be things like dev, prod, etc.
* All properties common to each profile can be maintained in application.properties