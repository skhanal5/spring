### Filters
* **Note**: For Servlets
* Based on Servlet Filters
* ![[filterchain.png]]
* Flow:
	* Client sends a request
	* Container makes a `FilterChain` with `Filter` instances and a `Servlet` for that request
* Rule:
	* Only one `Servlet` can handle a `HttpServletRequest`
	* Ordering for `Filter` matters
		* One `Filter` can affect downstream `Filters` in the `FilterChain`
### DelegatingFilterProxy
* An implementation of `FIlter`
* Purpose:
	* Bridges between Servlet container lifecycle and `ApplicationContext`
	* Allows you to register `Filter` without needing Spring-defined beans, has its own stnaadards
* ![[delegatingfilterproxy.png]]
* Looks up `Bean Filter 0` and invokes it 
* Other benefits:
	* delay looking up `Filter` bean instances
	* Read doc for more info on this
### FilterChainProxy
* A special `Filter` from Spring Security
* Allows you to delegate multiple `Filter` instances with `SecurityFilterChain`
* `FilterChainProxy` is a bean
	* wrapped with `DelegatingFilterProxy` usually
* Benefits of `FilterChainProxy`
	* starting point of Spring Security -> use this to debug
	* Allows you to use `RequestMatcher` to see which `Filter` to apply instead of depending on the URL like the Servlet
	* 
* ![[filterchainproxy.png]]
### SecurityFilterChain
* `FilterChainProxy` picks which `Filter` to use using this bean
* When matching, only the first `SecurityFilterChain` that applies is used
* ![[securityfilterchain.png]]
### Security Filters
* You can add a Security Filter using `SecurityFilterChain` API
* Like before, filters are executed in order
* Purpose for filters:
	* authentication
	* csrf
	* authorization
	* etc.
* Example:
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(Customizer.withDefaults())
            .authorizeHttpRequests(authorize -> authorize
                .anyRequest().authenticated()
            )
            .httpBasic(Customizer.withDefaults())
            .formLogin(Customizer.withDefaults());
        return http.build();
    }
}
```
 * Order:
	 * CSRF
	 * Authentication
	 * Authorization
* During application runtime:
	* Use logs for security events to see which filter is invoked
### Custom Filters
* Implement `Filter`
```java
public class TenantFilter implements Filter {

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest request = (HttpServletRequest) servletRequest;
        HttpServletResponse response = (HttpServletResponse) servletResponse;

        String tenantId = request.getHeader("X-Tenant-Id"); (1)
        boolean hasAccess = isUserAllowed(tenantId); (2)
        if (hasAccess) {
            filterChain.doFilter(request, response); (3)
            return;
        }
        throw new AccessDeniedException("Access denied"); (4)
    }

}
```
* Add filter to the SecurityFilterChain
```java
public class TenantFilter implements Filter {

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        HttpServletRequest request = (HttpServletRequest) servletRequest;
        HttpServletResponse response = (HttpServletResponse) servletResponse;

        String tenantId = request.getHeader("X-Tenant-Id"); (1)
        boolean hasAccess = isUserAllowed(tenantId); (2)
        if (hasAccess) {
            filterChain.doFilter(request, response); (3)
            return;
        }
        throw new AccessDeniedException("Access denied"); (4)
    }

}
```
### Exceptions
* Use `ExceptionTranslationFilter` to translate `AccessDeniedException` and `AuthenticationException` into HTTP Responses
* `ExceptionTranslationFilter` is added to FilterChainProxy as a Security Filter in the SecurityFilterChain
* ![[exceptiontranslationfilter.png]]
### RequestCache
* Scenario:
	* Suppose you send an unauthenticated request to a resource that requires authentication
	* Once the user authenticates, they should be able to get that resource
	* We need a way to replay the request after authentication
* `RequestCache` handles the above by saving the `HttpServletRequest`
* By default, `HttpSessionRequestCache` is used
* This can also be turned off with a `NullRequestCache`
### Logging
* A good log to use:
```yaml
logging.level.org.springframework.security=TRACE
```