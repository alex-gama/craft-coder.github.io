---
layout: default
---

# Mockito Interactions - Verifying Redundant Interactions

### Example 1

Sometimes we would like to verify an interaction with the mocked object but we are interested in
if there is no invocations that we didn't make.

Let's see the example and talk about it!

```java
public class MockitoInteractionsTest {

    @Test
    public void shouldFailIfThereIsMoreVerificationThanThatVerificationWasMade() throws Exception {
        UserDatabase userDatabase = mock(UserDatabase.class);

        userDatabase.findNameById(10L);

        verify(userDatabase).findNameById(10L);

        verifyNoMoreInteractions(userDatabase);
    }

}
```

Notice that we used the **Mockito.verifyNoMoreInteractions()** method. With that, we are asking for Mockito:

- Hey Mockito, please check if there is just the verification that has been made by me

In other others, if we have another invocation in the mocked object without verifying it, then the test will fail
in our face! Let's see it happening in the next example!

### Example 2

```java
public class MockitoInteractionsTest {

    @Test
	public void shouldFailIfThereIsMoreVerificationThanTheVerificationThatWasMade() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.delete(10L);

		verify(userDatabase).findNameById(10L);

		verifyNoMoreInteractions(userDatabase);
	}

}
```

This test will fail! Yes, I know, it is not so obvious but it is correct. In the code we:

- Called the findNameById() method once
- Called the delete() method once
- We verified JUST the method findNameById()

And to finish the test, we checked with the verifyNoMoreInteractions() method if there is
more interactions in the userDatabase objet than was made and yes, we called the delete() method without verifying it! Yes, we are lying to Mockito :(

Let's fix that!

### Example 3

Just fixing the code above, let's verify the method **delete()**

```java
public class MockitoInteractionsTest {

    @Test
	public void shouldBeOkIfThereIsCorrectNumberOfVerifications() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.delete(10L);

		verify(userDatabase).findNameById(10L);
		verify(userDatabase).delete(10L);

		verifyNoMoreInteractions(userDatabase);
	}

}    
```

This approach is useful when you must check if there is no Invocation in the mocked object that you don't know
or if there is invocations under the hood that you need to worry about

[Back to Interactions Page](mockito-number-of-interactions)

[<- Back to home](/)
