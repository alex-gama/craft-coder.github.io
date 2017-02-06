---
layout: default
---

# Erlang Numbers

### Starting typing Erlang numbers

We know that Erlang is awesome, cool and hipster! But numbers in Erlang is not magic, they are just...yeh, numbers!

Let's type them in the shell

```erlang
1> 10.
10
2> 20.
20
3> 5 + 10.
15
4> 10 - 4.
6
5> 10 / 5.
2.0
6> 10 div 5.
2
7> 10 rem 3.
1
8>
8> 10 * 2.
```

There is work to be done here!

As you can see, numbers in Erlang is not another dimension of reality. But, a few things must be understood in the code above.

In the execution 5 for example:

```erlang
5> 10 / 5.
2.0
```

Notice that, by default, Erlang will not care if you are using **integers** or **floating point numbers** but in this case Erlang will use floating point numbers in divisions using **/**.

If you would like to work with integer-to-integer division, just indicate to Erlang your intention by using **div** operator as you should notice in the execution 6:

```erlang
6> 10 div 5.
2
```

In the execution 7, we are printing out the rest of the division - remainder - using **rem**

```erlang
7> 10 rem 3.
1
```

### Erlang Number Expressions

Ok, numbers in Erlang is not so dangerous. Let's go a little bit dive and try to see more dangerous things about number

```erlang
1> (10 - 5) * 2.
10
2> (10 - 5) / 5.
1.0
3> - (10 - 5).
```


[<- Back to home](/)
