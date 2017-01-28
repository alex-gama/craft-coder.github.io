---
layout: default
---

# Mockito Interactions - Never Doing Interactions

### Example

In this example, we are checking if the method was never called by using **Mockito.never()** method

```java
public class MockitoInteractionsTest {

	@Test
	public void shouldCheckIfThereIsNoInteractionInTheMockedObject1() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		verify(userDatabase, never()).findNameById(10L);
	}

}
```

[Back to Interactions Page](mockito-number-of-interactions)

[<- Back to home](/)
