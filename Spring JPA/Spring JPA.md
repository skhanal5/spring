### Repository
- `Repository` is the central interface in Spring Data
	- `CrudRepository` and `ListCrudRepository` extends `Repository` and offer more granular functionality
- Formal definition is `Repository<T, ID>` where T is the domain class and ID is the identifier type for that domain class
- Technology specific abstractions include
	- `JpaRepository` and `MongoRepository` both of which extend `CrudRepository`
- There also exist:
	- Reactive versions of Repository's
	- Paginated Repository's
	-  not covering all that in here
### Selectively Exposing CRUD methods
* You can define a separate base Repository interface that extends `Repository<T,ID>` that is annotated with `@NoRepositoryBean`
	* Expose all the methods you need
* Then in the actual Repository you want to use, extend the base Repository
### Multiple Spring Data Modules
- For Spring Data to figure out which repository for which persisted technology, you need to not mix and match or have ambiguous repository definition
	- This is contingent on the repository definition and the domain class