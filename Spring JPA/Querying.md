### General Info
* Repositories determine a query from a method name by:
	* Parsing the method name
	* Using a manually defined query
* Available options are all contingent on the data store that you use (JPA, Mongo, etc.)
### Query Method Names
#### Structure
* Query method names consist of two things:
	* a subject
	* a predicate
* For example: `findPeopleByFirstnameOrLastname(String firstname, String lastname)
	* `find...By` is the subject
	* `FirstnameOrLastname` is the predicate
* Subjects are keywords that are supported by a particular datastore
* Predicates are typically a property expression, referring to one or more properties in the Entity
#### Query Implementation
* Parsing the method name and turning it into a query completely is contingent on the persistence store
##### Property Expression
* Must refer to the property of an entity
	* Must exist as well 
* Can traverse nested properties
	* `findByAddressZipCode` where Address contains ZipCode
###### Nested Properties Algorithm:
* first looks for property `AddressZipCode`
* If it doesn't exist, then it splits this property via camel case from the right side into a head and tail
	* `AddressZip` and `Code`
	* `Code` is the head
		* if the head exists, continue this algo with the remainder and build a tree
* If the head doesn't exist, it moves the split point over to the left and continues to look for a match
	* `Address` and `ZipCode`
* In case you have property names that can break this algorithm, use `_` in the method name to define the traversal point
	* Scenario:
		* `addressZip` and `Address.ZipCode` both exist
#### Subject Keywords
* Search
	* `find...By`
* Exists
	* `exists...By`
	* Returns Boolean usually
* Count
	* `count...By`
	* Returns numeric result
*  Delete
	* `delete...By`
	* Returns void or delete count
* First
	* `...First<number>...
	* Can be placed  in between `find` and `by`
* Distinct
	* `...Distinct...`
	* Can be placed  in between `find` and `by`
#### Predicate Keywords
* `AND`, `OR`, `AFTER`, `BEFORE`, etc.
#### Predicate Filter Modifiers
* `IgnoreCase`
	* case insensitive
* `AllIgnoreCase`
	* ignore case for all properties
* `OrderBy`
### Query Annotation
* `@Query` allows you to pass in a specific query that you want to use for that particular method
### Resources
1. [Repository query keywords](https://docs.spring.io/spring-data/commons/reference/repositories/query-keywords-reference.html#appendix.query.method.subject)

