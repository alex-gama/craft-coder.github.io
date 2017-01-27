---
layout: default
---

# Mockito Stubbing Void Methods - doThrow() method

### Example 1

If you have a void method that should be tested throwing an exception? But wait! How can we stub a void method with
Mockito?

Let's try to stub in the common way?

```java
public class MockitoStubbingVoidMethodsUsingDoThrowMethodTest {

	@Test
	public void shouldTryToThrowsAnExceptionWhenTheMethodIsCalled() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

        //This code will not even compile
		when(userDatabase.delete()).thenThrow(new RuntimeException());
	}

}
```

You can't do that! It will not even compile! You will receive the following error message

```bash
The method when(T) in the type Mockito is not applicable for the arguments (void)
```

Let's fix that in the next example

### Example 2

Now it's time to fix the previous example! Now we are using the **Mockito.doThrow()** method
to stub the void method and everything is ok now \o/

```java
public class MockitoStubbingVoidMethodsUsingDoThrowMethodTest {

    @Test
	public void shouldThrowsAnExceptionWhenTheMethodIsCalled() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		doThrow(new RuntimeException()).when(userDatabase).delete();
	}

}

```

### Example 3

Just to extend the previous example, we can stub the void method and ask to Mockito to create
a **new instance** of the Exception in each method invocation

```java
public class MockitoStubbingVoidMethodsUsingDoThrowMethodTest {

    @Test
	public void shouldThrowsAnExceptionWhenTheMethodIsCalledCreatingANewInstanceOfTheException() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		doThrow(RuntimeException.class).when(userDatabase).delete();
	}

}
```

[Back to Stubbing void methods](stubbing-void-methods)

[Back to the Main Page](/mockito-crafting-code)
