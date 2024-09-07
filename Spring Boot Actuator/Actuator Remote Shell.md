### Context
* Follows up with [[Actuator]]
- Spring Boot integrates with CRaSH
	- Shell that works can be embedded into any Java app
### Connecting to the Shell
- Add `spring-boot-starter-remote-shell` to your pom file
- When you run the application, it will log a password (like Spring Security)
	- Username is `user`
- Now, ssh into the shell `ssh user@localhost -p 2000`
### Useful Shell Commands
- `autoconfig`
	- similar to `/autoconfig` in [[Configuration Endpoints]]
	- Just in text format
- `beans`
	- similar to `/beans` in [[Configuration Endpoints]]
- `metrics`
	- similar to /metrics in [[Runtime Metrics]] BUT provides data in real time (neat)
- `endpoint`
	- lets you view endpoints with `list`
	- can invoke endpoints with `invoke [endpoint]`
	