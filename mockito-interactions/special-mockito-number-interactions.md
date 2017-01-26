---
layout: default
---

# Mockito Interactions - Useful Way to Verify Number of Interactions

### Example 1

Just to facilitate, Mockito enables us to use a few common methods when we are checking the
number of interactions.

In this example we are using the **Mockito.atLeastOnce()** method, that as you can guess, will check
if the method was called at least once

```java
public class MockitoInteractionsTest {

	@Test
	public void shouldCheckIfThereIsAtLeastOnceInteractionInTheMockedObject() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.findNameById(10L);

		verify(userDatabase, atLeastOnce()).findNameById(10L);
	}

}
```

### Example 2

In this example we are using the Mockito.atLeast() method but this time we passed a value to the method
indicating which number should be used to compare.

In this case, we are checking if the method was called at least twice

```java
public class MockitoInteractionsTest {

	@Test
	public void shouldCheckIfThereIsAtLeastTwiceInteractionInTheMockedObject() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.findNameById(10L);

		verify(userDatabase, atLeast(2)).findNameById(10L);
	}
}
```     

### Example 3

In this example we are checking if the method was called at most three times by using
the **Mockito.atMost()** method

```java
public class MockitoInteractionsTest {

	@Test
	public void shouldCheckIfThereIsAtMostThreeTimesInteractionInTheMockedObject() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.findNameById(10L);

		verify(userDatabase, atMost(3)).findNameById(10L);
	}

}
```     

[Back to Interactions Page](mockito-number-of-interactions)

[Back](/mockito-crafting-code) to Main Page
