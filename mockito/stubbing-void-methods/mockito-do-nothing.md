---
layout: default
---

# Mockito Stubbing Void Methods - doNothing()

### Example 1

Let's get the following example that is verifying if the delete() method was called in the test

```java
public class MockitoStubbingVoidMethodsUsingDoNothingMethodTest {

	@Test
	public void shouldVerifyIfTheMethodWasCalled() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.delete();

		verify(userDatabase).delete();
	}

}
```

Now imagine that we can't have this method being called twice. Let's test this scenario in the next example

### Example 2

Here we are worrying about calling the method **twice**. Notice that we are using the **Mockito.times(1)** method
just to get our intention clear, but you can **omit** it as we saw in [number of interactions](mockito-interactions/mockito-number-of-interactions)

```java
public class MockitoStubbingVoidMethodsUsingDoNothingMethodTest {

	@Test
	public void shouldVerifyIfTheMethodWasCalledEvenIfItWasCalledTwice() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.delete();
		userDatabase.delete();

		verify(userDatabase, times(1)).delete();
	}

}
```    

Let's get a better (or worse) problem with this test.

Imagine now that we must worry about the method being called twice, but we would like to throw an Exception
only when the second called is made.

Let's resolve it in the next example

### Example 3

Here we must worry about the method being called in the second time. It's time to use the **Mockito.doNothing()** method!

This method will say to Mockito:

- Hey Mockito, please, **don't do nothing** in the first method call!

Let's see!

```java
public class MockitoStubbingVoidMethodsUsingDoNothingMethodTest {

	@Test
	public void shouldDoNothingInTheFirstMethodCall() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		//valid just for the first method call
		doNothing().doThrow(new UnsupportedOperationException()).when(userDatabase).delete();

		userDatabase.delete();
		userDatabase.delete();
	}

}
```

The test will throws an **UnsupportedOperationException** because the second call should throws it.

doNothing() in this case is really useful in stubbing consecutive calls :)

### Example 4

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

[Back to Stubbing void methods](stubbing-void-methods)

[<- Back to home](/)
