---
layout: default
---

# Mockito Stubbing Void Methods - doReturn()

### Example 1

Sometimes is not possible to use **Mockito.when()** method. In this example, we are Spying an object
and testing it.

```java
public class MockitoStubbingVoidMethodsUsingDoReturnMethodTest {

	@Test
	public void shouldVerifyIfTheMessageIsCorrect() throws Exception {
		WebService webService = spy(WebService.class);

		UserService userService = new UserService(webService);

		String message = userService.save();

		verify(webService).sendMessage();
		assertThat(message, equalTo("Sending message"));
	}

}
```

Note that if we run the test, we should have a message printed out in the console

```bash
Sending message
```

This happens because we are using **Mockito.spy()** method that will record the object invocations but different
from **Mockito.mock()**, **spy** will let the code call the **Real method**

Let's move on and see what kind of problem we could have with this example

### Example 2

In this example we stubbed the sendMessage() method, indicating that a specific message should be retrieved
when the method is called.

```java
public class MockitoStubbingVoidMethodsUsingDoReturnMethodTest {

	@Test
	public void shouldVerifyIfTheMessageIsCorrectButCallingTheRealMethod() throws Exception {
		WebService webService = spy(WebService.class);

		UserService userService = new UserService(webService);

		when(webService.sendMessage()).thenReturn("Another message");

		String message = userService.save();

		verify(webService).sendMessage();
		assertThat(message, equalTo("Another message"));
	}

}
```

Note again that the test will pass but we yet have the message being **printed out in the console**
because we have a spied object being tested.

In the next example, we will try to fix that :)

### Example 3

In this example, we are using the **Mockito.doReturn()** method to sub the method, since **Mockito.when()**
can't help us with that.

Note that now we don't have a message being printed out in the console. Here the **real method is not called anymore**

```java
public class MockitoStubbingVoidMethodsUsingDoReturnMethodTest {

	@Test
	public void shouldVerifyIfTheMessageIsCorrectButWithoutCallingTheRealMethod() throws Exception {
		WebService webService = spy(WebService.class);

		UserService userService = new UserService(webService);

		doReturn("Another message").when(webService).sendMessage();

		String message = userService.save();

		verify(webService).sendMessage();
		assertThat(message, equalTo("Another message"));
	}

}
```    

### Example 4

Another approach that you can follow by using doReturn() method is overriding an exception that was
stubbed previous in the test

Here, we stubbed the sendMessage() method and it should throws an Exception when it is called.

```java
public class MockitoStubbingVoidMethodsUsingDoReturnMethodTest {    

	@Test
	public void shouldThrowsAnUnsupportedOperationException() throws Exception {
		WebService webService = mock(WebService.class);

		when(webService.sendMessage()).thenThrow(new UnsupportedOperationException());

		when(webService.sendMessage()).thenReturn("Some message"); //the test will fail
	}

}
```    

But note that we can't override the subbed method with another when() method because an exception will be thrown in our face!

In the next example we will fix it!

### Example 5

Now it's time to fix the Exception that is being thrown after call the sendMessage() method.

To do that, we will use the doReturn() method again, overriding the previous exception-stubbing

```java
public class MockitoStubbingVoidMethodsUsingDoReturnMethodTest {    

	@Test
	public void shouldNotThrowsAnUnsupportedOperationException() throws Exception {
		WebService webService = mock(WebService.class);

		when(webService.sendMessage()).thenThrow(new UnsupportedOperationException());

		doReturn("Some message").when(webService).sendMessage();


	}

}
```

Now our test is passing because the Exception was overridden.

Keep in mind that this scenario is really rare and you should avoid it. If you are overriding previous stubbed
methods, probably it is a code smell indicating that you are testing too much or you code is to much complex
and could be refactored.

**UserService utility class**

```java
class UserService {

	private WebService webService;

	public UserService(WebService webService) {
		this.webService = webService;
	}

	public String save() {
		String messageSent = webService.sendMessage();

		return messageSent;
	}

	public String unsupportedMethod() {
		throw new UnsupportedOperationException();
	}

}
```

**WebService utility class**

```java
class WebService {

	public String sendMessage() {
		System.out.println("Sending message");

		return "Sending message";
	}

}
```

[Back to Stubbing void methods](stubbing-void-methods)

[<- Back to home](/)
