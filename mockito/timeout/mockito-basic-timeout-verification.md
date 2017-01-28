---
layout: default
---

# Mockito Timeout Test - Basic Timeout Verification

### Example 1

Sometimes you have a multi-threaded system that is a little bit difficult to test because you don't have
your method being called immediately. In this cases, you will have the result after a few seconds, since the result will be
retrieved from another Thread

In this example, we will verify if the **WebService.sendMessage()** method was called after the
**UserService.update()** method. But notice that the sendMessage() method is being called inside a new Thread

```java
public class MockitoTimeoutTest {

	@Test
	public void shouldFailBecauseTheMethodHasNotCalledInTime() throws Exception {
		WebService webService = mock(WebService.class);

		UserService userService = new UserService(webService);

		userService.update();

		verify(webService).sendMessage();
	}

}
```

**UserService utility class**

```java
class UserService {

	private WebService webService;

	public UserService(WebService webService) {
		this.webService = webService;
	}

	public void update() {
		Runnable runnable = new Runnable() {

			@Override
			public void run() {
				try {
					TimeUnit.SECONDS.sleep(5);
				} catch (InterruptedException e) {
					throw new RuntimeException("Something bad happened :(");
				}
				webService.sendMessage();
			}
		};
		Thread thread = new Thread(runnable);
		thread.start();
	}

}
```

**WebService utility class**

```java
class WebService {

	public void sendMessage() {
		System.out.println("Sending message through WebService");
	}

}
```

In the example above, the test will fail because the response will be retrieved after 5 seconds and Mockito
can't wait for that :(

With this problem in mind, Mockito created the **Timeout** concept since the version **1.8.5**. With that version
is possible to indicate to Mockito a timeout to be used to wait for the response.

As you can see in the next example, we used the **Mockito.timeout()** method

### Example 2

```java
public class MockitoTimeoutTest {

    @Test
	public void shouldVerifyThatTheMethodHasCalledEvenAfter5Seconds() throws Exception {
		WebService webService = mock(WebService.class);

		UserService userService = new UserService(webService);

		userService.update();

		int fiveSeconds = 6_000;

		verify(webService, timeout(fiveSeconds)).sendMessage();
	}

}
```

Therefore, this test will pass because now Mockito will **wait 6 seconds** to verify if the **sendMessage()** method was called. Great! :)

[Back to Timeout Page](mockito-verifying-with-timeout)

[<- Back to home](/)
