---
layout: default
---

# Mockito Ordering - Verification in Order with Multiple Mocks

### Example 1

In this example we are verifying if the methods were called in the desired order but in this case
we are using 2 mocked objects

```java
public class MockitoVerificationInOrderTest {

    @Test
	public void shouldVerifyTheOrderBasedOnTwoMockedObjects() throws Exception {
		UserDatabase firstUserDatabase = mock(UserDatabase.class);
		UserDatabase secondUserDatabase = mock(UserDatabase.class);

		firstUserDatabase.findNameById(10L);
		secondUserDatabase.findNameById(10L);

		InOrder inOrder = inOrder(firstUserDatabase, secondUserDatabase);

		inOrder.verify(firstUserDatabase).findNameById(10L);
		inOrder.verify(secondUserDatabase).findNameById(10L);
	}

}
```

As you can see, it is very similar to [verify single mocks](mockito-particular-order-single-mock).

### Example 2

In this example, the test will fail because we are calling the **secondUserDatabase** object first than
**firstUserDatabase** object

```java
public class MockitoVerificationInOrderTest {

	@Test
	public void shouldFailWhileTryingToVerifyTheOrderBasedOnTwoMockedObjects() throws Exception {
		UserDatabase firstUserDatabase = mock(UserDatabase.class);
		UserDatabase secondUserDatabase = mock(UserDatabase.class);

		secondUserDatabase.findNameById(10L);
		firstUserDatabase.findNameById(10L);

		InOrder inOrder = inOrder(firstUserDatabase, secondUserDatabase);

		inOrder.verify(firstUserDatabase).findNameById(10L);
		inOrder.verify(secondUserDatabase).findNameById(10L);
	}

}
```

[Back to Verification in Order](mockito-particular-order-with-multiple-mocks)

[<- Back to home](/)
