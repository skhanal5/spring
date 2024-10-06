### Recap
* Objects define their dependencies (other objects) through:
	* constructor arguments
	* arguments to factory method
	* properties that are set on the object instance after it is made/returned from a factory
* Two types
	* Constructor-based
	* Setter-based
#### Constructor Based
* Container invokes a constructor with a # of args
* Each arg is a dependency
* Alternative: call a static factory method
* Great example from Spring docs
```java
public class SimpleMovieLister {

	// the SimpleMovieLister has a dependency on a MovieFinder
	private final MovieFinder movieFinder;

	// a constructor so that the Spring container can inject a MovieFinder
	public SimpleMovieLister(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}

	// business logic that actually uses the injected MovieFinder is omitted...
}
```
* Constructor arguments are usually resolved in the order which they are defined
* Note: when using xml and you define a bean's constructor arg with a simple type (e.g. a primitive) with an explicit value, you need to pass in the type explicitly
* **Preferred approach**
#### Setter-based Dependency Injection
* To construct a bean, we will use a no-arg constructor or a no-arg static factory method
* Then there must be a setter method that sets that dependency
* Example:
```java
public class SimpleMovieLister {

	// the SimpleMovieLister has a dependency on the MovieFinder
	private MovieFinder movieFinder;

	// a setter method so that the Spring container can inject a MovieFinder
	public void setMovieFinder(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}

	// business logic that actually uses the injected MovieFinder is omitted...
}
```