---
layout: default
---

### Optional.absent

**Example**

Sometimes you need to indicate that the Optional has not a non null value. Instead of use **Optional.of(null)** or **Optional.of(nullObject)** we should use the **Optional.absent()** method.

```java
public class GoogleGuavaOptionalTest {

	@Test
	public void shouldGetAnAbsentUser() throws Exception {
		Payment payment = new Payment();

		Optional<User> user = payment.getAnAbsentUser();

		assertFalse(user.isPresent());
	}
}

class Payment {

	public Optional<User> getAnAbsentUser() {
		User user = getNullValue();
		if (user == null) {
			return Optional.absent(); //instead of use Optional.of(null)
		}
		return Optional.of(user);
	}

}
```

[<- Back to Guava](../../google-guava)

[<- Back to home](/)
