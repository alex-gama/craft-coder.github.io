---
layout: default
---

# Mockito - Multiple Argument Matchers

### Example 1

This example is just a **warning** when we are working with [Argument Matchers](fundamental-mockito-argument-matcher).
Keep in mind that, if you started working with Argument Matcher, you must finish with it.

Let's see the example below

```java
public class MockitoArgumentMatcherTest {

    @Test
    public void shouldFailWhenWeStubTheMethodUsingAnyValueForNameAndAge() throws Exception {
        UserController userController = mock(UserController.class);

        //Yes, this will not work
        when(userController.findUserByNameAndAge(anyString(), 25L)).thenReturn("Mockito");

        //Yes, this will not work also
        String userName = userController.findUserByNameAndAge(anyString(), 25L);

        assertThat(userName, equalTo("Mockito"));
    }

}    
```

This test will fail :(

We started using the **anyString()** argument matcher in the **findUserByNameAndAge** method but we are passing
the value 25 into it. This is not allowed by Mockito!

Let's fix that in the next example

### Example 2

Now we are using Argument Matcher in **both** expected values by the findUserByNameAndAge method

```java
public class MockitoArgumentMatcherTest {

    @Test
    public void shouldStubTheMethodUsingAnyValueForNameAndAge() throws Exception {
        UserController userController = mock(UserController.class);

        when(userController.findUserByNameAndAge(anyString(), anyLong())).thenReturn("Mockito");

        String userName = userController.findUserByNameAndAge(anyString(), anyLong());

        assertThat(userName, equalTo("Mockito"));
    }

}    
```

And everything should work fine! \o/

### Example 3

The same approach must be used when we are using **verify** method. In this example, the test will fail
since we are using **anyInt()** argument matcher with the Nickname **value**

```java
public class MockitoArgumentMatcherTest {

    @Test
    public void shouldVerifyIfTheMethodWasCalledUsingAnyValueWithWrongArgumentMatchers() throws Exception {
        Users users = mock(Users.class);

        UserController userController = new UserController(users);

        userController.generateIdAndNickname();

        verify(users).saveIdWithNewNickname(anyInt(), "Nickname");
    }

}    
```

Now, let's fix the code by passing 2 argument matcher into the method

```java
public class MockitoArgumentMatcherTest {

    @Test
    public void shouldVerifyIfTheMethodWasCalledUsingAnyValueWithCorrectArgumentMatchers() throws Exception {
        Users users = mock(Users.class);

        UserController userController = new UserController(users);

        userController.generateIdAndNickname();

        verify(users).saveIdWithNewNickname(anyInt(), anyString());
    }

}    
```

**UserController utility class**

```java
class UserController {

	private Users users;

	public UserController(Users users) {
		this.users = users;
	}

	public void generateIdAndNickname() {
		int generatedValue = new Random().nextInt(10);
		users.saveIdWithNewNickname(generatedValue, "Nickname");
	}

	public String findUserByNameAndAge(String name, Long age) {
		return "Yes, I'm returning nothing :P";
	}

	public String findUserNameById(Long id) {
		if (id == 10L) {
			return "Alexandre Gama";
		}
		return "Craft Coder - Mockito";
	}

	public void generateId() {
		//we can't test it, since it is generated randomly
		int generatedValue = new Random().nextInt(10);
		users.generate(generatedValue);
	}

}
```

**Users utility class**


```java
class Users {

	public void generate(int value) {
		System.out.println("Generated value: " + value);
	}

	public void saveIdWithNewNickname(int id, String nickname) {
		System.out.println("Generated value: " + id);
		System.out.println("Generated nickname: " + nickname);
	}

}
```

[Back to Stubbing void methods](mockito-argument-matcher-main-page)

[Back to the Main Page](/mockito-crafting-code)
