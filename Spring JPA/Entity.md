### About
* Annotating a class with `@Entity` defines the domain class/object for JPA to use in its Repository
* It is a POJO that you want to persist in a DB
* Typically an Entity is a table, and each instance of an Entity is a row
### @Entity
* JPA assumes that if you have a class annotated with `@Entity` without `@Table` then this Entity maps to a table with the same name as the class name
### @Table
* If your table name does not correspond to the name of the entity name, you can use `@Table` to pass in the name of the table
### Defining Fields of an Entity
#### @Id
* `@Id` is used to tell JPA that this is that object's id
* It is used as a primary key
##### @GeneratedValue
* You can also pass in `@GeneratedValue` to tell JPA to generate the id automatically instead of passing it in
* You can define a strategy to generate the id
	* `AUTO`, `TABLE`, `SEQUENCE`, or `IDENTITY`
#### @Column
* `@Column` can be used to annotate a field of an entity to describe what column this field should map to
	* You can pass in an alternative name with `@Column(name="...")`
	* You can define if the field is nullable, unique, etc.
#### @Transient
* `@Transient` is used to denote that this field should not be persisted
* Usage: we need additional data using existing fields that are persisted
#### @Temporal
* `@Temporal` is used to denote that this is a time-based field
#### @Enumerated
* `@Enumerated` is used to denote that this field maps to a enum value
	* By default is is persisted by ordinal value instead of name
		* You don't need to annotate the field if this is the case
	* If you want to use the name, use `@Enumerated(EnumType.STRING)`
#### Unannotated Fields
*  Any fields without annotations are assumed by JPA to be mapped to a column corresponding to that field's name
