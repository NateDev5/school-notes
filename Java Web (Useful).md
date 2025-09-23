#### Annotation:
Starts with `@`
A special marker that gives extra instruction to the compiler
Useful for avoiding boilerplate code (which java is known for)

#### Lombok annotations
`@Getter`: Generates getters for each field in a class
`@Setter`: Generates setters for each field in a class
`@NoArgsConstructor`: Creates public no-argument constructor
`@AllArgsConstructor`: Create a public constructor with all args

```java
@Getters
@Setters
@AllArgsConstructor
public class Car {
	private String brand_name;
	private Integer mileage;
}
```