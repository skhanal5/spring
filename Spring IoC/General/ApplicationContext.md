### About
* Functionality:
	* Configures and manages the beans
* How:
	* Reads configuration metadata 
* From where?
	* XML/Groovy scripts
	* Annotated based
	* Java based
* Configuration:
	* Spring Boot handles this for you
### Configuration Metadata

#### Annotation Based

### XML Based
* Define an xml file with `<bean/>` elements
	* Each bean has an `id` that uniquely defines it
	* It also has a `class` that defines its type
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
		https://www.springframework.org/schema/beans/spring-beans.xsd">

	<bean id="..." class="...">
		<!-- collaborators and configuration for this bean go here -->
	</bean>

	<bean id="..." class="...">
		<!-- collaborators and configuration for this bean go here -->
	</bean>

	<!-- more bean definitions go here -->

</beans>
```
* To create a container with all of this, you use `ClassPathXmlApplicationconext` constructor
* If you have a bunch of xml files, you can import it all into one file using `<import/>`
#### Java Based
* Define Java classes that are annotated with `@Configuration` and `@Bean` for example
* **Preferred approach**
### Interacting with the Container
#### Fetching Beans
* From the `ApplicationContext` you can invoke `getBean(<name>, Clazz.class)` and interact with that object
* **Note**: it is recommended that you do not do this, use `@Autowired` instead
#### Registering Beans
* You can get the `BeanFactory` and use `registerSingleton()` or `registerBeanDefinition(..)` to manually deifne a bean
* Also not recommended