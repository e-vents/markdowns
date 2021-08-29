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