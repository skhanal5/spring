### Changing Endpoint Ids
- Set this property to update the path/id of the endpoint to a different value
	- `endpoints.endpoint-id.id`
	- Ex: `endpoints.shutdown-id=kill`
		- change `/shutdown` to `/kill`
### Enabling/Disabling Endpoints
* Set the property `endpoint.endpoint-id.enabled` to `true/false` to enable/disable respectively
* To disable all endpoints:
	* `endpoints.enabled= false`
### Adding Metrics & Gauges
* The Actuator contains a `CounterService` bean.
	* An interface with three methods
		* increment
		* decrement
		* reset
* `GaugeService` bean is similar
	* an interface with one method submit
* To use either, inject them onto the bean of interest and call the methods to update the metrics
* For custom metrics, use the `PublicMetrics` interface
### Custom Trace Repository
- `/trace` traces are capped to 100 entries
- Make you own `InMemoryTraceRepository` bean and set the capacity to a value > 100
- If you want to store traces outside of memory, use the `TraceRepository` interface
	- implement `findAll()` and `add()`
### Custom Health Indicators
- Implement the `HealthIndicator` interface and write your own health indicator
	- has one method `health()`
### Securing the Actuator
- Use [[Spring Security]]
