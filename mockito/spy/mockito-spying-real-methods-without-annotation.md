---
layout: default
---

# Mockito Spy - Spying Real Methods without Annotation

Spying an object means that you will **spy** the object and its **real method** will be called, therefore
you will not have a stubbed method being called.

### Example 1

In this example, just to be clear, we will use a mocked object and we will call methods from it.

```java
public class MockitoSpyingObjectTest {

	@Test
	public void shouldNotPrintTheLogMessageWhenWeAreUsingMockObject() throws Exception {
		Users users = mock(Users.class);

		UserController userController = new UserController(users);

		userController.save();

		verify(users).persist();
	}

}
```

The method save() was called and we have a few code snippets to examine:

- The Users class was **mocked**
- The method **save** was called in the userController variable

Notice that, when save method is called, then it calls the **persist** method from **Users**.

The persist method prints a message but we are using a mocked object, therefore any message will be printed

But notice something here! The class Users has the attribute **Logger** that is instantiated by the Users class. So,
we can't mock it, but we would like to have the Logger variable printing a message with the persist method.

In the next example we will use the Mockito.spy() method to do that :)

### Example 2

In this example we are interested in call the save message from UserController but we would like
to call the Real method from the Users and Logger class.

But wait, why do we just instantiate the Users class? We are interested in call the real method, right?

Here is the treasure! I would like to call the real method **BUT** I must track all invocations in the object and
this invocations are possible using mocked objects.

To resolve that, we will use the **Mockito.spy()** method instead of use **Mockito.mock()** method.

```java
public class MockitoSpyingObjectTest {    

	@Test
	public void shouldPrintTheLogMessageWhenWeAreUsingSpyObject() throws Exception {
		Users users = spy(Users.class);

		UserController userController = new UserController(users);

		userController.save();

		verify(users).persist();
	}

}
```

If you run the code above, you will see that the real method **persist** was called, and we **verified** it
using Mockito.verify() method.

So, just to recapitulate, we used the Mockito.spy but we verified if there are interactions with the object. Again,
when we use spy, the real method is called


```java
class UserController {

	public Users users;

	public UserController(Users users) {
		this.users = users;
	}

	public void save() {
		users.persist();
	}
}
```

```java
class Users {

	private Logger logger = new Logger();

	public void persist() {
		System.out.println("Saving");

		logger.log("Logging while saving the user");
	}

}
```

```java
class Logger {

	public void log(String message) {
		System.out.println(message);
	}

}
```

[<- Back to Spy page](mockito-spying-real-methods)

[<- Back to Mockito page](../)

[<- Back to home](/)
