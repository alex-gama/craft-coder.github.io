---
layout: default
---

### Optional.fromNullable

**Example 1**

Sometimes you don't know if the object is null or not. Get the following situation:

```java
class Payment {

	public Optional<User> getUserFromDatabase() {
		User user = getFromDatabase(); //could be null or not

		return Optional.of(user);
	}

	private User getFromDatabase() {
		return null; //ok, weird, but just to show you the case :)
	}

}
```

Notice that the **getUserFromDatabase()** method does not know if there is an User or not. In that case, you can't just use **Optional.of()** because you might get a Nullable user and your code will broke when you call the **Optional.get()** method.

**Example 2**

Instead of just use the **Optional.of()** method you could use the **Optional.fromNullable()** method as you can see below

```java
class Payment {

	public Optional<User> getUserFromDatabase() {
		User user = getFromDatabase(); //could be null or not

		return Optional.fromNullable(user); //now it is better :)
	}

	private User getFromDatabase() {
		return null; //ok, weird, but just to show you the case :)
	}

}
```

[<- Back to Guava](../../google-guava)

[<- Back to home](/)
