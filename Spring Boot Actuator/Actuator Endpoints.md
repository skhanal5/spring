### Actuator Endpoints
- Comes with useful endpoints like:
	- `/health`
	- `/trace`
	- `/shutdown`
	- `/metrics/{name}`
- Three types of endpoints:
	- configuration
	- metrics
	- misc
- To make use of this, add the `spring-boot-starter-actuator` dependency
### Configuration Endpoints
* `/beans` allows you to see every bean in the application context and other beans it injected
	* This is useful in case you want to know how beans are wired up in the auto-configuration
	* Provides data in JSON format
		* bean = name
		* resource = location of the class
		* dependencies = which other beans are injected with it
		* scope = self explanatory
		* type = Java's type
* `/autoconfig` tells you which of the [[[Conditional Configuration]] passed and failed
	* Provides JSON data:
		* positive matches and negative matches
* `/env` tells you all environment properties available to the application
	* To hide sensitive information, any property with password or key is hidden
	* Comes with `/env/{name}` endpoint
* `/mappings` provides a mapping of controllers to endpoints
### Metric Endpoitns
* `/metrics` gives you a bunch of runtime metrics
	* related to garbage collection
	* heap available vs used memory
	* number of classes loaded
	* amount of free memory
	* http related
		* `counter.status` is the http status code
		* `gauge.response` is used to gauge http responses
			* e.g. how long it took to serve a request
	* can fetch a specific metric with `/metric/{metricname}`
* `/trace` allows you to trace web request
	* you can see which method, path, headers, request/response
* `/dump` gives you thread snapshot
* `/health` endpoint is a basic health check endpoint...
	* alb/fargate