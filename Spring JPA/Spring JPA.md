### JpaRepository
- You can define an interface that extends `JPARepository<query type, response type>`
- The Spring Data JPA will give you can implementation of this interface at runtime
	- It contains many methods, each of which can be used with `query type`
### JPAEntity
* This is essentially a POJO that represents a JPA Entity
	* You must annotate this class with `@Entity`
* You define the fields that represents the Entity and any getter/setters
	* You can use the `@Id` annotation on a field to represent the ID for that Entity
