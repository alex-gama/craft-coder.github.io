---
layout: default
---

# Mockito BDD - Behavior Driven Development with Mockito

### Example 1

 Here we are stubbing the object as we used to stub, using the Mockito.when() method

```java
public class BehaviorDrivenDevelopmentTest {

	@Test
	public void shouldStubTheObjectUsingTheCommonlyUsage() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		when(userDatabase.findNameById(10L)).thenReturn("Crafting Code - Mockito");

		String name = userDatabase.findNameById(10L);

		assertThat(name, equalTo("Crafting Code - Mockito"));
	}

}
```

### Example 2

In this example we are using the BDD - Behavior Driven Development - approach with
given / when / then

```java
public class BehaviorDrivenDevelopmentTest {

	@Test
	public void shouldStubTheObjectUsingBDDApproach() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		given(userDatabase.findNameById(10L)).willReturn("Crafting Code - Mockito");

		String name = userDatabase.findNameById(10L);

		assertThat(name, equalTo("Crafting Code - Mockito"));
	}

}
```

**UserDatabase - Auxiliary class**


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

[Back](/mockito-crafting-code) to Main Page
