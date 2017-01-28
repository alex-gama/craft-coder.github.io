---
layout: default
---

# Mockito Timeout Test - Special Timeout Verification

### Example 1

If is it your first time visiting the verification with Timeout, probably you should start with the [previous page](mockito-basic-timeout-verification)
that will show you a few examples with motivation.

Let's now create our example using **Timeout** with **Number of Interactions**

In this example, as you can see, we used the **Mockito.times()** method with the **Mockito.timeout()** method

```java
public class MockitoTimeoutTest {

    @Test
	public void shouldVerifyThatTheMethodHasCalledEvenAfter5SecondsUsingTimes() throws Exception {
		WebService webService = mock(WebService.class);

		UserService userService = new UserService(webService);

		userService.update();

		int fiveSeconds = 6_000;

		verify(webService, timeout(fiveSeconds).times(1)).sendMessage();
	}

}
```

As you may guess, we can use with another methods that can check the number of interactions

### Example 2

In this example we are using the **Mockito.atLeastOnce()** method with **Mockito.timeout()**

```java
public class MockitoTimeoutTest {

    @Test
	public void shouldVerifyThatTheMethodHasCalledEvenAfter5SecondsUsingAtLeastOnce() throws Exception {
		WebService webService = mock(WebService.class);

		UserService userService = new UserService(webService);

		userService.update();

		int fiveSeconds = 6_000;

		verify(webService, timeout(fiveSeconds).atLeastOnce()).sendMessage();
	}

}    
```    

### Example 3

In this example we are using the **Mockito.atLeast()** method with **Mockito.timeout()**

```java
public class MockitoTimeoutTest {

	@Test
	public void shouldVerifyThatTheMethodHasCalledEvenAfter5SecondsUsingAtLeast() throws Exception {
		WebService webService = mock(WebService.class);

		UserService userService = new UserService(webService);

		userService.update();

		int fiveSeconds = 6_000;

		verify(webService, timeout(fiveSeconds).atLeast(1)).sendMessage();
	}

}
```

[Back to Timeout Page](mockito-verifying-with-timeout)

[<- Back to home](/)
