### Spring 4.0
- Uses conditional configuration to determine which configurations to be used and which to ignore
- JAR file called spring-boot-autoconfigure has multiple configuration classes
	- filtered by conditional configuration
### Condition Interface
- Implement this interface and override the matches() method
```
package readinglist;
import org.springframework.context.annotation.Condition;
import org.springframework.context.annotation.ConditionContext;
import org.springframework.core.type.AnnotatedTypeMetadata;

public class JdbcTemplateCondition implements Condition {
  @Override
  public boolean matches(ConditionContext context,
                         AnnotatedTypeMetadata metadata) {
    try {
      context.getClassLoader().loadClass(
             "org.springframework.jdbc.core.JdbcTemplate");
      return true;
    } catch (Exception e) {
      return false;
    }
  }
}
```
* You can use this when declaring beans
```
@Conditional(JdbcTemplateCondition.class)
public MyService myService() {
    ...
}
```
* Bean will only be used if that class is provided
## Conditional On Missing Bean
* Annotation `@ConditionalOnMissingBean(Clazz.class)` allows you to override auto configuration
* When you annotate a bean with this, it will only trigger the bean if and only if that bean doesn't already exist