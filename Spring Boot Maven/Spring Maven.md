### Starter dependencies
- Provides transitive dependencies needed for common functionality
	- Manages version compatibility for each dependency
	- Reduces # of dependencies you need to include
### Overriding starter transitive dependencies
* Can exclude dependencies in the starters with `<exclusions><exclusions/>`
* Can 
### spring-boot-maven-plugin
- packages the project as an executable uber-JAR
	- meaning all dependencies are packaged together
	- manifest is included
	- can run the app with java -jar 
- Want to use a different version of a dependency?
	- Just declare it with that version
	- Be aware that this might break compatibility of other dependencies in the starters