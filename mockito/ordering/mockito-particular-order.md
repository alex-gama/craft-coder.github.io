---
layout: default
---

# Mockito Ordering - Verification in Order with Single Mocks

### Example 1

Sometimes you must verify if the methods in your mocked object were called in the correct order.
In this first example, we will just verify if the methods were called but without worrying about
the ordering that the methods were called

```java
public class MockitoVerificationInOrderTest {

	@Test
	public void shouldVerifyIfTheMethodsWereCalledButCallingWithTheValue10First() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.findNameById(20L);

		verify(userDatabase).findNameById(10L);
		verify(userDatabase).findNameById(20L);
	}

}
```

Notice that we verified if the findNameById(10L) method was called with the value 10. Here the order of the
verify methods does not matter, since Mockito will not watch that.

In the next example, we will **try** to verify if the methods were called in the desired order

### Example 2

Trying to verify if the methods were called in the desired order

```java    
public class MockitoVerificationInOrderTest {

	@Test
	public void shouldVerifyIfTheMethodsWereCalled() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.findNameById(20L);

		verify(userDatabase).findNameById(20L);
		verify(userDatabase).findNameById(10L);
	}

}
```

As you can see, the test will pass! Yes, will pass because Mockito does not know that it must be verified
keeping in mind the ordering. Here we just change the order that the verify method will be called

Mockito introduced the **verification in order** that we will see in the next example

### Example 3

In this example we will use the **Mockito.inOrder()** method and will pass through it the mocked object.

Let's see:

```java
public class MockitoVerificationInOrderTest {

	@Test
	public void shouldVerifyIfTheMethodsWereCalledInOrder() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.findNameById(20L);

		InOrder inOrder = inOrder(userDatabase);

		inOrder.verify(userDatabase).findNameById(10L);
		inOrder.verify(userDatabase).findNameById(20L);
	}

}
```

As you can see, now we are not using the Mockito.verify() method and instead of that we are using the
**inOrder.verify()** that will verify the mocked object taking into consideration the ordering that the methods were called :)

### Example 4

In this example, the test will fail since we are expecting to have the verification in order

```java
public class MockitoVerificationInOrderTest {

	@Test
	public void shouldFailBecauseTheMethodsWereCalledInDifferentOrder() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(20L);
		userDatabase.findNameById(10L);

		InOrder inOrder = inOrder(userDatabase);

		inOrder.verify(userDatabase).findNameById(10L); //will fail, because this method was not called first
		inOrder.verify(userDatabase).findNameById(20L);
	}

}
```

**UserDatabase utility class**

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

[Back to Verification in Order](mockito-particular-order-single-mock)

[<- Back to home](/)
