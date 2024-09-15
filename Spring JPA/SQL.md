### DataSources
* `javax.sql.DataSource` interface sets up DB connections 
	* Requires a URL and credentials
### Configuration
#### DataSource Configuration
* Specify the following properties:
```
spring.datasource.url=jdbc:mysql://localhost/test
spring.datasource.username=dbuser
spring.datasource.password=dbpass
```
* If you do not specify a URL, Spring Boot will try to make a embedded database instead
#### Connection Pools
* There are four connection pools offered:
	* HikariCP, Tomcat, Commons DBCP2, and Oracle UCP
* Unless you specify one of these in particular, Spring Boot has its own algorithm to choose one
	* Each connection pool has its own set of configuration options available
	* Specify a pool via `spring.datasource.type`