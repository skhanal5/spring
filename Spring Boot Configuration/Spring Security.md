### Default Configuration
- Application requires a username and password when you try to open it in the browser
	- Password is in the logs
### Custom Configuration
 - To override the above, you need to write a class annotated with `@Configuration` and `@EnableWebSecurity` and extend `WebSecurityConfigurerAdapter.SecurityConfig` class
	 - You need to two `configure()` methods
		 - First one handles authorizing routes in your controller
		 - The second one handles looking up users for authentication
			 - JDBC, LDAP, in-memory user stores are supported
* In practice:
	* Take a look at the `SpringBootWebSecurityConfiguration` class
	* See how it uses [[Conditional Configuration]] with the `@ConditionalOnMissingBean(WebSecurityConfiguration.class)` to ignore the default configuration iff that class exists already in the classpath
	* When will `WebSecurityConfiguration` exist in the classpath?
		* The annotation `@EnableWebSecurity` creates this bean