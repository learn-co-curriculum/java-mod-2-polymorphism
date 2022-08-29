# Polymorphism

## Learning Goals

- Review the definition of polymorphism
- Explain how polymorphism works in Java

## What is Polymorphism?

Polymorphism is the last pillar of object-oriented programming that we need to
address. As a review, polymorphism is the ability to take on many forms and is
usually achieved through inheritance and interfaces in Java. Polymorphism helps
reduce complexity by having objects share certain behaviors and allow for
overriding methods.

## Runtime Polymorphism

As we mentioned, we usually see polymorphism appear when we talk about
inheritance and interfaces. So let's take a look at an example and go back to
our `Animal` class:

```java
package com.flatiron.animal;

public abstract class Animal {
    private String name;

    public String getName() { 
        return name; 
    }
    public void setName(String name) { 
        this.name = name; 
    }

    public void eat() {
        System.out.println("Yum! I like to eat!");
    }

    public abstract void makeSound();
}
```

As we know, when we have an `abstract` method, we have to override it and put
its implementation in the child classes. The `makeSound()` method is a perfect
example since each animal makes a different sound. The `makeSound()` method is
extended into multiple objects and has many forms of results. The `Cat` object,
for example, goes "Meow!" whereas the `Parrot` object goes "Squawk!" but they
both use the method `makeSound()`. This concept of method overriding is a type
of polymorphism that we usually refer to as **runtime polymorphism**. This is
because when the method is called, it is resolved at runtime and will then
call the appropriate overridden method.

We should also remember that method overriding is not limited to abstract
methods. In child classes, we can override other methods too, like we did with
the `Cat` class:

```java
package com.flatiron.animal;

public class Cat extends Animal implements Pet {
    private boolean isDeclawed;

    public Cat() {
        super();
        this.isDeclawed = false;
    }

    public boolean getIsDeclawed() { 
        return isDeclawed; 
    }
    public void setIsDeclawed(boolean isDeclawed) { 
        this.isDeclawed = isDeclawed; 
    }

    public void useLitter() {
        System.out.println("I just used the litter - I'm a clean cat!");
    }

    @Override
    public void eat() {
        super.eat();
        System.out.println("I like to eat cat food!");
    }

    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }

    @Override
    public void petAnimal() {
        System.out.println("I'm a happy cat! I love pets!");
    }
}
```

Notice in the `Cat` class, we have overridden the `eat()` method and the
`petAnimal()` method. The `eat()` method we inherited from the `Animal` class
and decided to make it more specific to how a `Cat` eats. The `petAnimal()`
method is from the interface, `Pet`, and acts much like an abstract method where
the implementation also needs to be included in any classes that implement the
`Pet` interface. Both of these examples of method overriding are also examples
of runtime polymorphism.

## Compile-Time Polymorphism

Don't cats make more than one sound? Can't they purr as well? Let's add another
method to our `Cat` class and also call it `makeSound()` but with a parameter
so, we can specify the certain sound:

```java
@Override
public void makeSound() {
    System.out.println("Meow!");
}

public void makeSound(String sound) {
    System.out.println(sound);    
}
```

Having two methods with the same name but different parameter lists is called
**method overloading**. Like method overriding, there are some rules that we
must follow when we overload methods:

- The method names must be the same.
- The method names must have a different parameter list.
- The methods can have a different return type.
- The access level can vary.

Now if we want, we can call the `makeSound()` method with either no parameters
or a `String` parameter:

```java
public class AnimalDriver {
    public static void main(String[] args) {
        Cat myCat = new Cat();
        myCat.makeSound();
        myCat.makeSound("Purr");
    }
}
```

The above would have the following output:

```plaintext
Meow!
Purr
```

Method overloading is also known as **compile-time polymorphism** because the
method is resolved when we compile the code.
