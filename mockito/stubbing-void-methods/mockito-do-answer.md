---
layout: default
---

# Mockito Stubbing Void Methods - doAnswer()

### Example

Imagine that you must stub a void method with **generic answer**

We can use the **Mockito.doAnswer()**

```java
public class MockitoStubbingVoidMethodsUsingDoAnswerMethodTest {

	@Test
	public void shouldStubAVoidMethodWithGenericAnswer() throws Exception {
		UserDatabase userDatabase = Mockito.mock(UserDatabase.class);

		doAnswer(new Answer<String>() {

			@Override
			public String answer(InvocationOnMock invocation) throws Throwable {
				Object[] arguments = invocation.getArguments();
				UserDatabase mock = (UserDatabase) invocation.getMock();
				System.out.println(mock);
				System.out.println(arguments);
				return null;
			}
		})
		.when(userDatabase).delete();

		userDatabase.delete();
	}

}
```

**UserDatabase auxiliary class**

```java
class UserDatabase {

	public String findNameById(Long id) {
		if (id == 1) {
			return "Alexandre Gama";
		}
		return "Craft Coder - Mockito";
	}

	public void delete() {
		System.out.println("Deleting the User");
	}
}
```

[Back to Stubbing void methods](stubbing-void-methods)

[<- Back to home](/)
