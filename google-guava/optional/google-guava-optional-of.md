---
layout: default
---

### Optional.of

**Example 1**

Basic usage of **Optional.of()** and **Optional.isPresent()** methods from Guava Optional.

```java
public class GoogleGuavaOptionalTest {

	@Test
	public void shouldGetTheValueUsingGuavaOptional() throws Exception {
		Optional<Integer> optionalNumber = Optional.of(10);

		assertTrue(optionalNumber.isPresent());

		Integer value = optionalNumber.get();

		assertThat(value, equalTo(10));
	}

}
```

Notice that we used the **Optional.get()** method to retrieve the value wrapped by the Optional. But what will happen if we try to call this method with null values? Wait, we will see one more example before we try that :)

**Example 2**

Using the **Optional.isPresent()** method to check if the Optional has a value

```java
public class GoogleGuavaOptionalTest {

	@Test
		public void shouldPrintOutThatThereIsNoUser() throws Exception {
			Payment payment = new Payment();
			Optional<User> optional = payment.getNullableUser();

			if (optional.isPresent()) {
				System.out.println("Yeah! There is an User");
				User user = optional.get();
				System.out.println(user.getName());
			} else {
				System.out.println("There is no User, sorry about that :(");
			}
		}

}

class Payment {

	public Optional<User> getNullableUser() {
		User user = null;
		return Optional.fromNullable(user); //forcing the user to be null
	}

}
```

**Example 3**

Trying to get a value from an Optional that has a null value. Yes, we will get an Exception in our face!

```java
public class GoogleGuavaOptionalTest {

	@Test(expected = IllegalStateException.class)
	public void shouldThowsAnExceptionWhenWeTryToGetAnUserThatNoLongerExists() throws Exception {
		Payment payment = new Payment();
		Optional<User> optional = payment.getNullableUser();

		optional.get();
	}

}
```

Optional.get() cannot be called on a absent value, if you do that, Guava will throws an IllegalStateException. Again, the idea behind the Optional is that you should worry about nullable values, therefore, forcing you to check if you has or not a value.

**Example 4**

Retrieving a valid (non null or course) User from an Optional

```java
public class GoogleGuavaOptionalTest {

	@Test
	public void shouldGetTheNonNullableUserFromMethod() throws Exception {
		Payment payment = new Payment();

		Optional<User> userOptional = payment.getUserWithName();
		if (userOptional.isPresent()) {
			System.out.println("There is an User there! Nice!");
			User user = userOptional.get();
			assertThat(user.getName(), equalTo("Alexandre Gama"));
		}
	}
}

class Payment {

	public Optional<User> getUserWithName() {
		User user = new User("Alexandre Gama");
		return Optional.of(user);
	}

}
```

As you can see, we are retrieving a valid User by calling the **Optional.of(user)**

[<- Back to Guava](../../google-guava)

[<- Back to home](/)
