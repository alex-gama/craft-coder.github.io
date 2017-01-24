---
layout: default
---

### Configuring Mockito with @Mock annotation

**Example 1**

Let's use @Mock annotation to mock a class

```java
@RunWith(MockitoJUnitRunner.class)
public class MockitoConfigurationUsingMockAnnotation {

	@Mock
	private UserDatabase userDatabase;

	@Test
	public void shouldReturnTheUserMockingTheDatabaseUsingStaticImport() throws Exception {
		when(userDatabase.findNameById(10L)).thenReturn("Mockito - Crafting Code");

		String name = userDatabase.findNameById(10L);

		assertThat(name, equalTo("Mockito - Crafting Code"));
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

Here we used the **@Mock** annotations instead of use [Mockito static methods](mockito-configuration-without-annotation).

Notice that we used the annotation:

```java
@RunWith(MockitoJUnitRunner.class)
```

This annotation is required here and is used to indicate that the JUnit should use the MockitoJUnitRunner class to run the tests.

Yeh, it's common to forget this annotation and see an Exception being thrown in our face :)

**Example 2**

Initializing Mockito Framework by using static method and @Mock annotation

```java
public class MockitoConfigurationUsingMockAnnotationAndStaticMethods {

	@Mock
	private UserDatabase userDatabase;

	@Before
	public void setup() {
		MockitoAnnotations.initMocks(this);
	}

	@Test
	public void shouldReturnTheUserMockingTheDatabaseUsingStaticImport() throws Exception {
		when(userDatabase.findNameById(10L)).thenReturn("Mockito - Crafting Code");

		String name = userDatabase.findNameById(10L);

		assertThat(name, equalTo("Mockito - Crafting Code"));
	}

}

```

Now, we're not using the @RunWith annotation and insteaf of that we're using the **MockitoAnnotations.initMocks(this)** methods
inside a method that should use the **@Before** annotation from JUnit.

This approach is similar to use @RunWith annotation.

[Back to Mockito Configuration Page](configuring-mockito-with-and-without-annotation)

[Back to Main page](/mockito-crafting-code)
