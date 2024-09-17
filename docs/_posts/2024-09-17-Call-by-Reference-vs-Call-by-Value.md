---
layout: post
title: "Is Java 'pass-by-reference' or 'pass-by-value'?"
date:   2024-09-17 11:27:16 +0600
categories: java
---
## Is Java "pass-by-reference" or "pass-by-value"?

When writing programs in Java, we often need to pass arguments into methods. This brings up one of the most frequent questions among developers: Does Java pass parameters **by reference** or **by value**? At first glance, it might seem that Java passes parameters "by reference," but that's not the case. Java **always** uses **"pass-by-value"**, although this can be confusing, especially when working with objects.

## What is "pass-by-value"?

First, let's define what "pass-by-value" means. This is when a method receives a **copy** of the value of the variable passed to it. So, any changes made inside the method **do not affect the original variable**.

For example:
```java
public class Example {
    public static void main(String[] args) {
        int x = 5;
        modifyValue(x);
        System.out.println(x);  // Output: 5
    }

    public static void modifyValue(int x) {
        x = 10;
    }
}
```

Here, the value of `x` inside the `modifyValue` method is changed to 10, but in the `main` method, the variable `x` remains 5. Why? Because a **copy** of the value of x was passed to the `modifyValue` method.

## What about objects?

Now let's deal with objects, as this is where most of the confusion arises. When we pass an object to a method, a **copy of the reference** to the object is passed, not the object itself. And this is a key point.

Let's say we have the following Cat class:

```java
class Cat {
    String name;

    Cat(String name) {
        this.name = name;
    }
}

public class Example {
    public static void main(String[] args) {
        Cat myCat = new Cat("Whiskers");
        modifyCat(myCat);
        System.out.println(myCat.name);  // Output: Fluffy
    }

    public static void modifyCat(Cat cat) {
        cat.name = "Fluffy";  // Modifying the object’s field
    }
}
```

In this example, although we passed a **copy of the reference** to the `myCat` object, we were able to change its internal state — the name. This happens because the **copy of the reference** points to the same object in memory as the original variable. However, if we tried to reassign the reference inside the method, the original object would remain unaffected:

```java
public static void modifyCat(Cat cat) {
    cat = new Cat("Tom");  // Reassigning the reference
}
```

In this case, the object’s name in main would still be "Whiskers" because reassigning the reference only affects the local copy of the reference inside the method.


## Why is this important?

Understanding that Java **always** passes by value helps avoid confusion and mistakes when working with methods, especially when modifying the state of objects. Many think that Java passes objects by reference, but this is technically incorrect. In reality, Java passes a **copy of the reference** to the object.


## Conclusion

Java is always **"pass-by-value"**. However, when working with objects, Java passes a **copy of the reference** to the object, which can create the illusion of "pass-by-reference." It's important to remember that changes inside the method can affect the state of the object, but not the reference itself.
