---
layout: default
---

# Mockito Stub - Stubying with Fluent Interface

### Example 1

Sometimes we need to stub an object with different returns for the same method call. A real case is when you should mock iterations in the same mocked object.

This is not a common scenario, but if you must test it, Mockito will support you :)

In this example, we stubbied the method to return three values

- Mockito
- Guava
- java 8

Those values will be returned when the method will be called once, twice and three times respectively

```java
public class MockitoStubbingWithFluentInterfaceTest {

	@Test
	public void shouldStubAnObjectWithThreeIterations() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		when(userDatabase.findNameById(1L)).thenReturn("Mockito", "Guava", "Java 8");

		String firstName = userDatabase.findNameById(1L);  //first call
		String secondName = userDatabase.findNameById(1L); //second call
		String thirdName = userDatabase.findNameById(1L);  //third call

		assertThat(firstName, equalTo("Mockito"));
		assertThat(secondName, equalTo("Guava"));
		assertThat(thirdName, equalTo("Java 8"));
	}

}
```

### Example 2

This example will show us the same behavior of the previous one, but using consecutive calls

Note that this can be used as a Fluent Interface :)

```java
public class MockitoStubbingWithFluentInterfaceTest {

	@Test
	public void shouldStubAnObjectWithThreeIterationsConsecutiveCalls() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		when(userDatabase.findNameById(1L))
			.thenReturn("Mockito").thenReturn("Guava").thenReturn("Java 8");

		String firstName = userDatabase.findNameById(1L);  //first call
		String secondName = userDatabase.findNameById(1L); //second call
		String thirdName = userDatabase.findNameById(1L);  //third call

		assertThat(firstName, equalTo("Mockito"));
		assertThat(secondName, equalTo("Guava"));
		assertThat(thirdName, equalTo("Java 8"));
	}

}
```

**Auxiliar UserDatabase class**

```java
class UserDatabase {

	public String findNameById(Long id) {
		if (id == 1) {
			return "Alexandre Gama";
		}
		return "Craft Coder - Mockito";
	}

}
```

[Back to Behavior and Stubbing](mockito-behavior-and-stubbing)

[<- Back to home](/)
