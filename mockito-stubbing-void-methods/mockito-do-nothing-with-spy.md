---
layout: default
---

# Mockito Stubbing Void Methods - doNothing() with Spy

### Example 1

Let's extend the [use](mockito-do-nothing) of doNothing() method.

Sometimes you want that a spied object does not call the real method when you are testing your code.

In this example, we **Spy** the UserWebService class and we call the save() method from UserController class.

```java
public class MockitoStubbingVoidMethodsUsingDoNothingMethodTest {

	@Test
	public void shouldVerifyIfTheMethodWasCalledSpyingAnObject() throws Exception {
		UserWebService webService = spy(UserWebService.class);

		UserController userService = new UserController(webService);

		userService.save();
	}

}
```

After run the code above, notice that a message is printed out:

```bash
Sending message
```

Of course for this example we will not worry about that. But in a real scenario, probably the WebService will
an external service and this operation could be costly and even impossible in the test.

Let's fix it out using the **Mockito.doNothing()** method

### Example 2

Now we would like to call the save() method but without call the WebService real method.

```java
public class MockitoStubbingVoidMethodsUsingDoNothingMethodTest {

	@Test
	public void shouldVerifyIfTheMethodWasCalledSpyingAnObjectWithoutCallingTheRealMethod() throws Exception {
		UserWebService webService = spy(UserWebService.class);

		UserController userService = new UserController(webService);

		doNothing().when(webService).sendMessage();

		userService.save();
	}

}
```

As you can see, we are using the **Mockito.doNothing()** method to fix the problem. Keep in mind that this method
only can be used in **void methods**

[Back to Stubbing void methods](stubbing-void-methods)

[Back to the Main Page](/mockito-crafting-code)
