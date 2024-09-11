### About
- Specialized version of `@Component`
- One important feature:
	- Allows all implementation classes to be autodetected through classpath scanning
### Usage
- Do not use `@Service` on the interface
	- We can get a `NoSuchBeanDefinition` exception
	- Spring cannot auto-detect the corresponding component
- Use it on the implementation only
	- When we annotate the instance of the interface with `@Autowired`, Spring will detect the implementations marked with `@Service` and register them as beans
### Resources
1. [Service Annotation Placement](https://www.baeldung.com/spring-service-annotation-placement)
2. 