---
layout: default
---

# Mockito - Using Mocks with mock() and verify() methods

**Example 1**

In this example we will not use Mocked objects and instead of that we will use the Real object. Just to see the difference between Real and Mocked objects


```java
public class MockitoMockAndStubsTest {

	@Test
	public void shouldWorkWithTheRealUserDatabaseObjectWithExistingId() throws Exception {
		UserDatabase userDatabase = new UserDatabase();

		String userName = userDatabase.findNameById(1L); //yes, the id 1 exists as you can see in the UserDatabase class below

		assertThat(userName, equalTo("Alexandre Gama"));
	}

}
```

**Example 2**

Now we're trying to retrieve a user which id does not exists

```java

public class MockitoMockAndStubsTest {

	@Test
	public void shouldWorkWithTheRealUserDatabaseObjectWithUnkwonId() throws Exception {
		UserDatabase userDatabase = new UserDatabase();

		String userName = userDatabase.findNameById(15L); //this id doesn't exist

		assertThat(userName, equalTo("Craft Coder - Mockito"));
	}

}
```

**Example 3**

 Imagine that the UserDatabase makes a costly operation when try to find a user name
 given an id :(
 Now it's time to mock our object!

 One of the greatest feature to have when we'are using Mockito is its capability to
 record all interactions that a Mocked object had.

 In this example we did a few things:

 - We mocked the UserDatabase class
 - We called the findNameById() method
 - We check if is true that the findNameById() method was called with the value 18

```java
public class MockitoMockAndStubsTest {

	@Test
	public void shouldMockTheUserDatabaseClassAndVerifyIfTheMethodWasCalledWithTheCorrectId() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(18L);

		verify(userDatabase).findNameById(18L);
	}

}
```

**Example 4**

In the following example the test will not pass since we are verifying that the method was called
	 with a different id. Mockito just recorded that the method has called with id = 18

```java
public class MockitoMockAndStubsTest {

	@Test
	public void shouldMockTheUserDatabaseClassButVerifyTheCalledMethodWithWrongId() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(18L);

		verify(userDatabase).findNameById(21L); //come on, I didn't call you with the value 21. The test will not pass :(
	}

}
```

If you are new in the Mockito world, don't worry if you didn't understand yet :) We will see a lot, A LOT of examples using Mockito!

```java
class UserDatabase {

	public String findNameById(Long id) {
		if (id == 1) {
			return "Alexandre Gama";
		}
		return "Craft Coder - Mockito";
	}

}
```

[Back to Behavior and Stubbing](mockito-behavior-and-stubbing)

[Back](/mockito-crafting-code) to Main Page
