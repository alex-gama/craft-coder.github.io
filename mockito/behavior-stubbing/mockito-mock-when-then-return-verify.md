---
layout: default
---

# Mockito - Basic usage of when() and thenReturn() methods

### Example 1

This example is showing us how to Stub a method. Stub here means the you will create a fake behavior based on your rule.

In out scenario, we are asking for Mockito:

- Hey Mockito, please, when the method **findNameById()** is called with the value 25, **then return** the name "Craft Coder - Google Guava"

As you can see, we taught the Mockito what we are excepting for when the method findNameById is called

```java
public class MockitoStubsTest {

	@Test
	public void shouldStubTheMethodAndIndicatesToMockitoWhatShouldHappenWhenTheMethodIsCalledWithSpecificValue() throws Exception {
		UserDatabase userDatabase = Mockito.mock(UserDatabase.class);

		when(userDatabase.findNameById(25L)).thenReturn("Craft Coder - Google Guava");

		String userName = userDatabase.findNameById(25L);

		assertThat(userName, equalTo("Craft Coder - Google Guava"));
	}

}

```

### Example  2

As you can see in this example, we didn't teach to Mockito what we will expect when the method is called with the value 19

We just taught to Mockito about the value 25, therefore **Mockito** will say for you:

- Hey, I have no idea what I need to do with the value 19! So, I will return a null value for you :(

```java
public class MockitoStubsTest {

	@Test
	public void shouldStubTheMethodAndIndicatesToMockitoWhatShouldHappenWhenTheMethodIsCalledWithSpecificValueVerifyingTheWrongValue() throws Exception {
		UserDatabase userDatabase = Mockito.mock(UserDatabase.class);

		when(userDatabase.findNameById(25L)).thenReturn("Craft Coder - Google Guava");

		String userName = userDatabase.findNameById(19L);
		System.out.println(userName); //Yes, null value :(

		assertThat(userName, not(equalTo("Craft Coder - Google Guava")));
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
