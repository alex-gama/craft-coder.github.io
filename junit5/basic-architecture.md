---
layout: default
---

# JUnit 5 and its new life's philosophy

JUnit 5 was born basically from the JUnit Lambda project.

JUnit 5 has a new concept in mind: It was built based on several modules, using 3 sub-projects.

This is a result of a new thought:

- Allows applications to extend JUnit functionalities

- Be a foundation for launching testing frameworks on the JVM

- Allows the creation of composed annotations (yes, we will talk about it later)

- New awesome annotations

- Supports tests written in JUnit 3 and JUnit 4, now named as Vintage versions

Let's talk about this 2 sub-projects a bit more

### JUnit and its 3 Sub-Projects

JUnit 5 is divided into 3 main sub-projects

- JUnit Platform

- JUnit Jupiter

- JUnit Vintage

**JUnit Platform**

This sub project becomes to be the guy that will allows many applications to launch its own way to build a testing framework. Awesome!

JUnit Platform defines the **TestEngine** API that will allows that a Gradle or Maven plugin can be built for example.

This new **TestEngine** interface will enable us to write a discovery and execution ways for a particular programming model.

Long story short, JUnit Platform contains the **Engine API** and provides a **huge API** to tools and frameworks

**JUnit Jupiter**

JUnit brings to us a new philosophy of how to write and extend tests. JUnit Jupiter sub-project is the combination of the new JUnit 5 programming and extension module.

So, for example, imagine that you would like to create a Mockito extension to write your tests in a particular way. You'll be able to do that by using JUnit Jupiter and its interfaces and annotations, like @ExtendWith.

Let's go further?

Jupiter is divided into modules, the [jupiter-api](https://github.com/junit-team/junit5/tree/master/junit-jupiter-api) and [jupiter-engine](https://github.com/junit-team/junit5/tree/master/junit-jupiter-engine)

JUnit Jupiter API contains all the annotations, assertions, tags, etc. For example, in this module we can find the [AssertTrue](https://github.com/junit-team/junit5/blob/master/junit-jupiter-api/src/main/java/org/junit/jupiter/api/AssertTrue.java) and [BeforeEach](https://github.com/junit-team/junit5/blob/master/junit-jupiter-api/src/main/java/org/junit/jupiter/api/BeforeEach.java) annotations

JUnit Jupiter Engine implements the main JUnit Engine API, that...you know what? Yes, implements the JUnit Platform.

**JUnit Vintage**

As you may guess, JUnit Vintage is the sub-project to enable us to write or be compatible with previous JUnit versions 3 and 4.

Notice here that this is a challenge, since the programming model has changed. JUnit Vintage will use the JUnit Platform Engine to be able to run this previous versions.

Let's go a little deeper again?

As I said, Vintage implements the Platform API. Did you remember that this new Platform has an Engine called TestEngine? As you can see in the code, [Vintage implements](https://github.com/junit-team/junit5/blob/master/junit-vintage-engine/src/main/java/org/junit/vintage/engine/VintageTestEngine.java) the TestEngine interface and its contract, for example implementing the **discovery** and **execute** methods.

**Java required version**

Yes, JUnit 5 will only allow you to use it if you're using Java 8


[<- Back to home](/)
