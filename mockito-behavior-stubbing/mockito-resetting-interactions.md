---
layout: default
---

# Mockito - Reseting Mock Interactions


### Example

**Wait**! Before you try to use the **reset()** method from Mockito, keep in mind that its use **indicates a code smell** and probably will show you that you're testing too much in the same test.

Before more warnings, let's see the example!

In this example we:

- Mocked the UserDatabase class and we interacted with its method **findNameById()** twice.
- We used the Mockito verify() method to check if the findNameById() method was called

After that, we would like to **reset ALL interactions** that has been made in the Mocked object.

We use the **reset()** method. Notice that the verify() method **will not work** after we call the reset() method since all interactions that has been made was lost


```java
public class ResettingMockTest {

	@Test
	public void shouldResetAMock() throws Exception {
		UserDatabase userDatabase = mock(UserDatabase.class);

		userDatabase.findNameById(10L);
		userDatabase.findNameById(12L);

		verify(userDatabase).findNameById(10L);
		verify(userDatabase).findNameById(12L);

		reset(userDatabase);

		verify(userDatabase).findNameById(10L);
		verify(userDatabase).findNameById(12L);
	}

}
```

**Warning** is coming again!

As you can see, the **reset()** method normally show us that the test is testing too much and **we should split** the test into another one.

If you reset you test, probably you would like to use the mocked object again to verify another behavior! This new behavior should be put in another test, keeping your tests with **focus and with single behavior**

Again to be annoying: This could be a sign of **poor test**. Be concerned about it!

[Back to Behavior and Stubbing](mockito-behavior-and-stubbing)

[Back](/mockito-crafting-code) to Main Page
