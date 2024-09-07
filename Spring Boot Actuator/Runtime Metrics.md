### About
- Follows up on [[Actuator Endpoints]]
### Endpoints
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
* 