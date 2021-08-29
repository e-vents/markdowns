# Introduction
This is a summary of some advanced topics regarding programming with Java.

These topics are covered (quick access):
- [Design Patterns](#design-patterns)
- [Inheritance](#inheritance)
- [Recursion](#recursion)
- [Generics](#generics)
- [Testing](#testing)
- [Lambdas](#lambdas)
- [Streams](#streams)
- [Threads](#threads)
- [Professional Applications](#professional-applications)

Have fun!

# Design Patterns

You can classify Design Patterns into Creational Patterns, Structural Patterns, and Behavioral Patterns.

## Factory Method Pattern

This pattern is creational and also known as a **virtual constructor**. 
A factory method creates and returns objects but is not a constructor. This pattern is helpful when initialization can only partially take place in the constructor. Another use case is when we don't need a new object. The factory will detect that and will reuse objects. See ``` LocalDate.now(); ``` 

```java
public class SpeakerFactory {

  public static ISpeaker getSpeaker(Language lang) throws SpeakerException {
    switch (lang) {
      case French: return new FrenchSpeaker();
      case German: return new GermanSpeaker();
      case English: return new EnglishSpeaker();
      default:
        throw new SpeakerException("No speaker can speak such language");
    }
  }
}
```
In the above code example the factory method reaches back to the constructor methods of different classes that implement the common interface "ISpeaker". Like that, the concept "program to interfaces not implementations" can be fullfilled and we make use of the concept of polymorphism.

````java
ISpeaker speaker = SpeakerFactory.getSpeaker(Language.German);
````
## Singleton Pattern

With this pattern, which is also a creational pattern, it is possible to ensure, that exactly one instance of a class exists. This pattern is mostly used in multi-threaded and database applications. It is used in logging, cahcing, thread pools, and configuration management.

````java
public class Demonstrator {
  // static class attribute to reference the (only) instance of the class
  private static Demonstrator singleton;
  // static factory method provides the access from outside
  public static Demonstrator getInstance() {
    if (singleton == null)
      return new Demonstrator();
    return singleton;
  }
  // private constructor, preventing access from outside
  private Demonstrator() { }
}
````

## Observer Pattern

## Strategy Pattern

# Inheritance

# Recursion

# Generics

# Testing

# Lambdas

# Streams

# Threads

# Professional Applications
```java

```