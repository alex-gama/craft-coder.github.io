---
layout: default
---

### Configuring Mockito without annotation

**Example 1**

Let's configure Mockito without annotation. In this first example we will use static methods from Mockito Framework

```java
public class MockitoConfigurationMockingWithoutAnnotation {

	@Test
	public void shouldReturnTheUserMockingTheDatabase() throws Exception {
		UserDatabase userDatabase = Mockito.mock(UserDatabase.class);

		Mockito.when(userDatabase.findNameById(10L)).thenReturn("Mockito - Crafting Code");

		String name = userDatabase.findNameById(10L);

		MatcherAssert.assertThat(name, Matchers.equalTo("Mockito - Crafting Code"));
	}

}

class UserDatabase {

	public String findNameById(Long id) {
		if (id == 1) {
			return "Alexandre Gama";
		}
		return "Craft Coder - Mockito";
	}

}

```

**Example 2**

We mocked the UserDatabase class by using the **Mockito.mock()** method. There is a few boilerplate code and we can fix it importing
Mockito methods statically as you can see below

```java
public class MockitoConfiguration {

	@Test
	public void shouldReturnTheUserMockingTheDatabaseUsingStaticImport() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		when(userDatabase.findNameById(10L)).thenReturn("Mockito - Crafting Code");

		String name = userDatabase.findNameById(10L);

		assertThat(name, equalTo("Mockito - Crafting Code"));
	}

}
```

Better, isn't it? :)

[Back to Mockito Configuration Page](configuring-mockito-with-and-without-annotation)
[Back to Main page](index)
