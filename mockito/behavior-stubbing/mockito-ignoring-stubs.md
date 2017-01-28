---
layout: default
---

# Mockito Stubs - Ignoring Stubs

### Example 1

Before we get into the Ignoring Stubs Mockito feature, let's remember how to check if the Mocked object has no more interactions at some point of the test.

In this example, we created two mocks for UserDatabase class and we stubbed those mocks, as you can see in the code below:

```java
public class IgnoringStubsTest {

	@Test
	public void shouldIndicateThatNoMoreInteractionsHasBeenMadeInTheMockedUserDatabaseObject() throws Exception {
		UserDatabase userDatabase1 = mock(UserDatabase.class);
		UserDatabase userDatabase2 = mock(UserDatabase.class);

		when(userDatabase1.findNameById(1L)).thenReturn("A");
		when(userDatabase2.findNameById(1L)).thenReturn("B");
		when(userDatabase1.findNameById(2L)).thenReturn("C");

		//We have 3 interactions here
		System.out.println(userDatabase1.findNameById(1L));
		System.out.println(userDatabase2.findNameById(1L));
		System.out.println(userDatabase1.findNameById(2L));

		verify(userDatabase1).findNameById(1L);
		verify(userDatabase2).findNameById(1L);
		verify(userDatabase1).findNameById(2L);

		verifyNoMoreInteractions(userDatabase1);
		verifyNoMoreInteractions(userDatabase2);
	}

}
```

As you can see in the code above, we use the verifyNoMoreInteractions from Mockito Framework. What is that for?

We use the verifyNoMoreInteractions method when we would like to guarantee that no more interactions has been made in the mocked object, just the interactions that were checked with the verify() method

In this example, we did the following verifications:

- verify(userDatabase1).findNameById(1L);
- verify(userDatabase2).findNameById(1L);
- verify(userDatabase1).findNameById(2L);

Therefore, 3 verifications has been made in the mocked objects. In the next example, we will remove one of the verify() methods to see what will happen

### Example 2

In this example we remove (actually is was commented :P) the third verification, therefore we have now 2 verifications.

But as you can see, we are using the following code:

- ```java
System.out.println(userDatabase1.findNameById(2L))
 ```

Yes, we'are now verifying 2 interactions but we had 3 interactions with the mocks. In this situation, our code will fail

```java
public class IgnoringStubsTest {

	@Test
	public void shouldIndicateThatNoMoreInteractionsHasBeenMadeInTheMockedUserDatabase2() throws Exception {
		UserDatabase userDatabase1 = mock(UserDatabase.class);
		UserDatabase userDatabase2 = mock(UserDatabase.class);

		when(userDatabase1.findNameById(1L)).thenReturn("A");
		when(userDatabase2.findNameById(1L)).thenReturn("B");
		when(userDatabase1.findNameById(2L)).thenReturn("C");

		System.out.println(userDatabase1.findNameById(1L));
		System.out.println(userDatabase2.findNameById(1L));

		//This is the accused of the crime
		System.out.println(userDatabase1.findNameById(2L));

		verify(userDatabase1).findNameById(1L);
		verify(userDatabase2).findNameById(1L);
//		verify(userDatabase1).findNameById(2L); Here we stopped to verify the userDatabase1 object

		//will fail here, since we stopped to verify the userDatabase1
		verifyNoMoreInteractions(userDatabase1);
		verifyNoMoreInteractions(userDatabase2);
	}

}
```

### Example 3

In this example we used the ignoreStubs() method from Mockito. Now we are asking for Mockito:

- Hey Mockito, I would like to ignore a non verification in the stubbed userDatabase1 object

Now, Mockito will check if **there is no more interactions** in our stubbed object and will just check it without check if

```java
public class IgnoringStubsTest {

	 */
	@Test
	public void shouldIgnoreTheStubbedObject() throws Exception {
		UserDatabase userDatabase1 = mock(UserDatabase.class);
		UserDatabase userDatabase2 = mock(UserDatabase.class);

		when(userDatabase1.findNameById(1L)).thenReturn("A");
		when(userDatabase2.findNameById(1L)).thenReturn("B");
		when(userDatabase1.findNameById(2L)).thenReturn("C");

		System.out.println(userDatabase1.findNameById(1L));
		System.out.println(userDatabase2.findNameById(1L));

		//This is the accused of the crime - This is another interaction and should be verified by Mockito
		System.out.println(userDatabase1.findNameById(2L));

		verify(userDatabase1).findNameById(1L);
		verify(userDatabase2).findNameById(1L);

		//We stopped the verification
		//verify(userDatabase1).findNameById(2L);

		//Will not fail, since we are ignoring the stub
		verifyNoMoreInteractions(ignoreStubs(userDatabase1)); //will notfail here, since we had 2 interactions with the userDatabase1
		verifyNoMoreInteractions(userDatabase2);
	}

}

```

**Auxiliar UserDatabase class**

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

[<- Back to home](/)
