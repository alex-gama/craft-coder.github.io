---
layout: default
---

### Mockito Spy - Spying Real Methods with Annotation

In this example we are just using **annotations** instead of call the Mockito.spy directly.

If you want to know more about **Mockito Spy** just go to the [page](mockito-spying-real-methods-without-annotation) :)

Here we are using the @Mock and @Spy annotations, that keep our code clean and easier to read

```java
@RunWith(MockitoJUnitRunner.class)
public class MockitoSpyingObjectWithAnnotationTest {

	@Mock
	private Users users;

	@Spy
	private Users usersSpy;

	@Test
	public void shouldNotPrintTheLogMessageWhenWeAreUsingMockObject() throws Exception {
		UserController userController = new UserController(users);

		userController.save();

		verify(users).persist();
	}

	@Test
	public void shouldPrintTheLogMessageWhenWeAreUsingSpyObject() throws Exception {
		UserController userController = new UserController(usersSpy);

		userController.save();

		verify(usersSpy).persist();
	}

}
```

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
