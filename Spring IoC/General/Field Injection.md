### About
* We can inject fields by using `@Autowired` like so:
```java
@Component
public class SomeService {
     @Autowired private SomeOtherService someOtherService;
}
```
* Alternatively, we can use constructor based injection
```java
@Component
public class SomeService {
    private final SomeOtherService someOtherService;

    @Autowired
    public SomeService(SomeOtherService someOtherService){
        this.someOtherService = someOtherService;
    }
}
```
* Second option is preferred for testing
* Benefits
	* Immutable
	* Easier to test (no need for reflection)
	* Safer code
* [Why field injection is evil](olivergierke.de/2013/11/why-field-injection-is-evil/)
