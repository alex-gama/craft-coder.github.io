---
layout: default
---

# Mockito Verification - Printing Custom Message when the Verify fails

### Example 1

Now, since 2.1.0 version we can custom the failure message when the verify fails

As you can see below, we can print out the custom message using the Mockito.description() method.

Again. you will be capable to use this feature just since 2.1.0 version

```java
public class CustomFailureMessageVerificationTest {

	@Test
	public void shouldShowACustomMessageWhenVerificationFails() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		verify(userDatabase, description("Sorry, but the method has not been called")).findNameById(10L);
	}

}
```

### Example 2

We can use the custom message when we are testing the code with Mockito.times() method

```java
public class CustomFailureMessageVerificationTest {

	@Test
	public void shouldShowACustomMessageWhenVerificationFailsUsingTimes() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		verify(userDatabase, times(3).description("Sorry, but the method has not been called")).findNameById(10L);
	}
}
```

### Example 3

We can use the custom message when we are testing the code with Mockito.atLeast() method

```java
public class CustomFailureMessageVerificationTest {

	@Test
	public void shouldShowACustomMessageWhenVerificationFailsUsingAtLeast() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		verify(userDatabase, atLeast(2).description("Sorry, but the method has not been called")).findNameById(10L);
	}

}
```

### Example 4

We can use the custom message when we are testing the code with Mockito.atLeastOnce() method

```java
public class CustomFailureMessageVerificationTest {

	@Test
	public void shouldShowACustomMessageWhenVerificationFailsUsingAtLeastOnce() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		verify(userDatabase, atLeastOnce().description("Sorry, but the method has not been called")).findNameById(10L);
	}

}
```

### Example 5

We can use the custom message when we are testing the code with Mockito.atMost() method

```
public class CustomFailureMessageVerificationTest {

	@Test
	public void shouldShowACustomMessageWhenVerificationFailsUsingAtMost() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		verify(userDatabase, atMost(2).description("Sorry, but the method has not been called")).findNameById(10L);
	}

}
```

### Example 6

We can use the custom message when we are testing the code with Mockito.never() method

```java
public class CustomFailureMessageVerificationTest {

	@Test
	public void shouldShowACustomMessageWhenVerificationFailsUsingNever() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);

		verify(userDatabase, never().description("Sorry, but the method has not been called")).findNameById(10L);
	}

}
```

[Back to Behavior and Stubbing](mockito-behavior-and-stubbing)

[<- Back to home](/)
