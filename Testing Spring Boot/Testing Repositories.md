### Scenario
- You wrote a repository, how do you test its functionality?
- No need to unit test, unless you provide custom functionality (additional queries, etc.)
- You need a way of integration testing the Repository to see:
	- If queries work and return the intended domain class
### @DataJPATest
 * Provides a minimal Spring context for the persistence layer
	 * Doesn't load the full Application Context
* Provides:
	* EntityManager
	* TestEntityManager\
* It creates a **in-memory H2 database** to use in place of your production database 
* All tests annotated with this are executed within a transaction
	* Any changes made to the DB are rolled back the end of the test
### Configuration
#### Properties
* You can pass in properties to `@DataJpaTest` to adjust connection details, etc.
* For example:
	* `@DataJpaTest(properties = {...})`
#### showSQL
* Allows you to see the SQL queries that are being executed by each of the methods in the Repository
* For example:
	* `@DataJpaTest(showSql=true)
#### Disabling Transactional Behavior
* To prevent transactions from rolling back after the end of the testing, you can use `@Transaction`
	* For example: `@Transactional(propagation = Propagation.NOT_SUPPORTED)` at either the class level or the method level will stop this behavior