---
layout: default
---

# Mockito Stubbing Void Method - doCallRealMethod()

### Example 1

Imagine that you need to test a mocked object, right? Now your problem is:

- You should mock the object but the real method should be called

It is a little bit strange, because does not make a reaaally sense if you mock your object, right?

In this example we will just see the default behavior from Mockito when we mock an object and call its methods

```java
public class MockitoStubbingVoidMethodsUsingDoCallRealMethodTest {

	@Test
	public void shouldTryToCallTheRealMethodFromTheMockedObject() throws Exception {
		UserWebService webService = mock(UserWebService.class);

		UserController userService = new UserController(webService);

		userService.save();
	}

}
```

**UserController auxiliary class**

```java
class UserController {

	private UserWebService webService;

	public UserController(UserWebService webService) {
		this.webService = webService;
	}

	public void save() {
		webService.sendMessage();
	}

	public String unsupportedMethod() {
		throw new UnsupportedOperationException();
	}

}
```

**UserWebService auxiliary class**

```java
class UserWebService {

	public void sendMessage() {
		System.out.println("Sending message");
	}

}
```

Notice that Mockito didn't call the real method from the UserWebService class. It is the default behavior
when we are working with mocked objects.

But sometimes (really sometimes, it is not usual) you **need to call the real method** even in yout mocked object.

To get this situation, you should use the **Mockito.doCallRealMethod()** method as you can see in the next example

### Example 2

In this example we are calling the real method from a mocked object

```java
public class MockitoStubbingVoidMethodsUsingDoCallRealMethodTest {

	@Test
	public void shouldToCallTheRealMethodFromTheMockedObject() throws Exception {
		UserWebService webService = mock(UserWebService.class);

		UserController userService = new UserController(webService);

		doCallRealMethod().when(webService).sendMessage();

		userService.save();
	}

}
```

If you run the code above, you will see a message that will be printed out in the console

```bash
Sending message
```

[Back to Stubbing void methods](stubbing-void-methods)

[<- Back to home](/)
