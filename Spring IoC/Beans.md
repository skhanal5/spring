### About
* In the [[ApplicationContext]], we define beans in xml
* How are they represented in the container?
	* As `BeanDefinition` objects
#### BeanDefinition
* Contains:
	* class name
	* configuration elements (how it behaves in the container)
	* references to other beans (dependencies)
	* other configuration options (e.g., connection pool)
	* and more
### Bean Instantiation
* If you are using `xml` you must define the `class` attribute
* A class attribute is used two ways when making a bean by the container:
	* Using reflection to call its constructor
	* Using the static factory method to create the bean
		* you can define this in xml with `factory-method`