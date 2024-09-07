### About
- Follows up on [[Actuator Endpoints]]
#### Useful Endpoints
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
