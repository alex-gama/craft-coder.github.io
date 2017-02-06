---
layout: default
---

# Java 8 - Default Methods

Hey! In this article we will look at what default methods are, why it was born and how we can use them

So, the first question is, why default methods in Java 8?

### Why did Oracle create Default Methods?

Let's take a cup of coffee and try to think as an [Oracle Rock-Star Engineer](http://www.businessinsider.com/oracle-rock-star-engineers-2016-3/#scott-albrecht-rewriting-the-it-playbook-3)...

What can we do if we need to create a method inside an Interface? Let's say that I would like to create another method inside in one of the most, used, loved Interface in the Java World: **List**

**Alternative 1**

It's easy. Let's create the method, break the interface List and force everybody to use the new Java 8.

Hmm, does not sounds great..

**Alternative 2**

So, we would create a new way to add new methods in interfaces without breaking it.

For example, Oracle would like to add the **sort()** method in the List interface.

```java
public interface List<E> extends Collection<E> {

	//Method created in Java 8
	default void sort(Comparator<? super E> c) {
        Object[] a = this.toArray();
        Arrays.sort(a, (Comparator) c);
        ListIterator<E> i = this.listIterator();
        for (Object e : a) {
            i.next();
            i.set((E) e);
        }
    }
}
```

This was the way that Oracle found to put another method inside an existing interface. Oracles creates **Default Methods!**

### Default Method Basic Structure

**Default Method** is just a method with the **default** keyword. As you may notice, the **sort()** method from List interface is starting by the default keyword.

In this case, the compiler will enable us to implement the Interface without worrying about the new method. Awesome right?

Are you doubting me?

Ok! Let's create our own default method!

### Creating a Default Method

Imagine that we have a **PaymentService** class that is responsible to...you know...take payments!

```java
interface PaymentService {

	double retrieveDefaultFees();

}
```

Now we have a class to implement the Interface above

```java
class PayPalPaymentService implements PaymentService {

	@Override
	public double retrieveDefaultFees() {
		return 10.9;
	}

}
```

As you can see, we must implement the **retrieveDefaultFees** method, since we are implementing the interface. It is a contract to follow!

Let's create a test to check it?

```java
public class DefaultMethodTest {

	@Test
	public void shouldRetrieveTheDefaultFees() throws Exception {
		PaymentService service = new PayPalPaymentService();

		double fees = service.retrieveDefaultFees();

		assertThat(fees, equalTo(10.9));
	}

}
```

Now, as an Oracle Rock-Star Engineer, we would like to put a new method but without breaking down all Payment providers in the World, like PayPal in our example.

We should use a **Default Method**!

```java
interface PaymentService {

	double retrieveDefaultFees();

	default double send(double value) {
		System.out.println("Sending the value: " + value);

		return value;
	}

}
```

As you can see, the default method is using the **default** keyword and our class **PayPalPaymentService** is working properly and does not worry about the new method.

We can even call the default method if we want.

```java
public class DefaultMethodTest {

	@Test
		public void shouldInvokeTheDefaultMethodFromPaymentService() throws Exception {
			PaymentService paymentService = new PayPalPaymentService();

			//Calling the default method send()
			double valueSent = paymentService.send(20);

			assertThat(valueSent, equalTo(20.0));
		}

}		
```

Great!

That's it! I hope that it could be helpful you to you!



[<- Back to home](/)
