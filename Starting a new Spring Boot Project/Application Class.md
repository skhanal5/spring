### Purpose
Does two things:
- Configuration
- Bootstrapping the app
`@SpringBootApplication`
- Enables component scanning and auto-configuration
- Combines:
	- `@Configuration`
		- Designates a configuration class using Java-based configuration
	- `@ComponentScan`
		- Allows for components to be discovered and registered as beans
	- `@EnableAutoConfiguration`
Bootstrapping
- main method allows you to run application as a executable JAR
- SpringApplication.run() takes the class and the CLI args to run the app
