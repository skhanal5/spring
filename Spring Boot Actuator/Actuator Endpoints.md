### About
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
- By default all endpoints are enabled except for `shutdown`
### Configuring Endpoints

#### Available Endpoints by Default
* To prevent all endpoints from being enabled by default use `management.endpoints.enabled-by-default=false`
#### Enabling/Disabling An Endpoint
* Use `management.endpoint.<endpoint-id>.enabled = <boolean>` property to enable/disable it
* Disabling an endpoint will remove it from the entire application context
#### Exposing Endpoints over a Transport
* Only the `health` endpoint is exposed over HTTP and JMX
* For JMX: 
	* `management.endpoints.jmx.exposure.[include/exclude]=[endpoint ids]`
* For html:
	* `management.endpoints.web.exposure.[include/exclude]=[endpoint ids]`
#### Actuator Discovery Page
* Contains links to all endpoints
* to disable: `propertiesmanagement.endpoints.web.discover.enabled=false`
### Configuring Actuator Path
#### Setting the Base Path
* Set `managment.endpoints.web.base-path=[/path]`
#### Remapping the Path of Existing Endpoints
* Set `management.endpoints.web.path-mapping.[endpoint-name]=[new endpoint path name]`
	* Turns `/actuator/old-path` to `/actuator/new-path`
### Security
#### Customizing Security
* By default, all endpoints besides `health` are secured Spring Boot if the following conditions are true;
	* Spring Security is on the classpath
	* There are no other `SecurityFilterChain` beans
* If you define your own `SecurityFilterChain` bean, then it is your responsibility to handle access to the actuator endpoints
#### Example
```java
import org.springframework.boot.actuate.autoconfigure.security.servlet.EndpointRequest;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.web.SecurityFilterChain;

import static org.springframework.security.config.Customizer.withDefaults;

@Configuration(proxyBeanMethods = false)
public class MySecurityConfiguration {

	@Bean
	public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
		http.securityMatcher(EndpointRequest.toAnyEndpoint());
		http.authorizeHttpRequests((requests) -> requests.anyRequest().hasRole("ENDPOINT_ADMIN"));
		http.httpBasic(withDefaults());
		return http.build();
	}

}
```

#### Allowing Unauthenticated Access
* Set this property: `management.endpoints.web.exposure.include=*`
* If Spring Security is also present, do this in addition:
```java
import org.springframework.boot.actuate.autoconfigure.security.servlet.EndpointRequest;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.web.SecurityFilterChain;

@Configuration(proxyBeanMethods = false)
public class MySecurityConfiguration {

	@Bean
	public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
		http.securityMatcher(EndpointRequest.toAnyEndpoint());
		http.authorizeHttpRequests((requests) -> requests.anyRequest().permitAll());
		return http.build();
	}
}
```

### Implementing Endpoints
* Define a `@Bean` with `@Endpoint` 
	* Any methods annotated with:
		* `@ReadOperation`
		* `@WriteOperation`
		* `@DeleteOperation`
	* Are exposed via JMX/HTML
* Alternatively:
	* Use `@JmxEndpoint` or `@WebEndpoint` in place of `@Endpoint`