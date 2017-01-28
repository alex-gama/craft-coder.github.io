---
layout: default
---

# Mockito Interactions - Basic Number of Interactions

### Example 1

When we check if there is interactions in the mocked object, actually under the hood
we are checking if there is **just 1 interaction** with the object.

In this example, we are verifying if the **findNameById()** method was called

```java
public class MockitoInteractionsTest {

	@Test
	public void shouldCheckIfThereIsInteractionInTheMockedObject() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);

		verify(userDatabase).findNameById(10L);
	}
}
```

But under the hood, Mockito is checking if the method was called **just once**.

In the next example we will see what is happening under the **verify()** method

### Example 2

In this example we are checking explicitly if there is **only 1 interaction** with the method
by calling the method **Mockito.times(1)**

```java
public class MockitoInteractionsTest {

	@Test
	public void shouldCheckIfThereIsInteractionInTheMockedObjectUsingTimes() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);

		verify(userDatabase, times(1)).findNameById(10L);
	}
}
```

Of course, as you may guess, we could verify if the method was called **more than once**, as you can follow in the next example

### Example 3

In this example, we are checking if there is **only 2** interactions with the mocked object by using **Mockito.times(2)**

```java
public class MockitoInteractionsTest {

	@Test
	public void shouldCheckIfThereIsTwiceInteractionInTheMockedObject() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.findNameById(10L);

		verify(userDatabase, times(2)).findNameById(10L);
	}

}
```

[Back to Interactions Page](mockito-number-of-interactions)

[<- Back to home](/)
