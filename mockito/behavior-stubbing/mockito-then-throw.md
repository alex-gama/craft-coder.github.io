---
layout: default
---

# Mockito - Usage of the thenThrow() method

### Example 1

This is the perfect scenario when you just need to Stub an object and test something with this stubbed object

```java
public class MockitoWorkingWithExceptionsTest {

	@Test
	public void shouldStubTheObjectAndGetItsStubbedValue() throws Exception {
		UserDatabase userDatabase = Mockito.mock(UserDatabase.class);

		when(userDatabase.findNameById(20l)).thenReturn("Craft Coder - Google Guava");

		String userName = userDatabase.findNameById(20l);

		assertThat(userName, equalTo("Craft Coder - Google Guava"));
	}

}
```

### Example 2

But sometimes you just need to test a situation when things goes wrong :(

In that scenario, you might be **worried** about what will happen if a **specific Exception** been thrown by your code

With Mockito we just need to use the **thenThrow()** method as you can see below

```java
public class MockitoWorkingWithExceptionsTest {

	@Test
	public void showThrowAnExceptionInSpecificSituation() throws Exception {
		UserDatabase userDatabase = Mockito.mock(UserDatabase.class);

		when(userDatabase.findNameById(20l)).thenThrow(new RuntimeException());

		userDatabase.findNameById(20l);
	}
}
```

### Example 3

But if you run the previous code, your test will not pass :(

This happens because **Mockito didn't know** that you was really expecting that Exception.

To fix that, we can use the **@Test(expected)** approach, and we will let Mockito know about the expected Exception that will be thrown by the method

```java
public class MockitoWorkingWithExceptionsTest {

	@Test(expected = RuntimeException.class)
	public void showThrowAnExceptionInSpecificSituationAndLetMockitoKnowAboutThat() throws Exception {
		UserDatabase userDatabase = Mockito.mock(UserDatabase.class);

		when(userDatabase.findNameById(20l)).thenThrow(new RuntimeException());

		userDatabase.findNameById(20l);
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
