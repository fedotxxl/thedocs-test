# Java coding standards

## Overview
This document describes java coding standards

## General
1. Indent is 4 spaces
1. Ordering within file:
    1. file comment
    1. package statement
    1. \<blank line>
    1. import statements
    1. \<blank line>
    1. /** class/interface javadoc comment */
    1. class
    1. static member variables
    1. instance variables
    1. constructors
    1. public methods
    1. private methods
    1. inner classes

## Variable naming
Use the English-natural variable naming convention, split the words with upper case.
```
//incorrect
int idSubscriber;
String mail_key;
```
```
//correct
int subscriberId;
String mailKey;
```


## Initialization
Try to initialize local variables where they’re declared.
The only reason not to initialize a variable where it’s declared is if the initial value depends on some computation occurring first.
Don't use multiple assignments in one line. It logic can depends on context and can be confusing.

## Long classes, methods
Long methods, fat classes having too much responsibility should be avoided, since it greatly reduces general readability of code.

## Error handling
### Method argument checking (and assert-ions)
You should NOT use `assert` for checking the input parameters to methods being not-null. Instead use for example

```
if (arg1 == null) {
    throw new IllegalArgumentException("Argument arg1 was null!");
}
```

or Apache Commons Validator framework or Spring Assert class;

Because assertion exceptions are an `ErrorException` they will not be caught as you would expect a normal exception to be caught
(since according to Java standards we use `catch(Exception)` not `catch(Throwable)`) thus making them unsuitable for most uses.

### NullPointerException
Avoid throwing a `NullPointerException` - it's confusing because most people will assume that the virtual machine threw it.
Consider using an `IllegalArgumentException` instead; this will be clearly seen as a programmer-initiated exception.

### Ignoring exceptions is forbidden
Do not ignore exceptions:
```
//incorrect
} catch (Exception e) {
    e.printStackTrace();
}
```
More info - "Effective Java" by Joshua Bloch, chapter on exception handling and in particular Item 47.

### Cause exceptions preserved
i.e. do:

```
} catch (MyLowLevelException e) {
    throw new SystemNamedException("error happened doing my low level stuff", e);
}
```

or:

```
} catch (MyLowLevelException e) {
    throw (RuntimeException)new RunTimeException("error happened doing my low level stuff").initCause(e);
}
```

Only the most specific Exception possible caught.
Do not use `catch(Exception e)`, but `catch(FileNotFound e)`, etc.

### System.exit()
If an error occurs anywhere in your program, throw an exception.
There should be only one place in the program that catches all the exceptions and does a System.exit(),this is usually the main() method.
If you are exiting because of an error use exit(errorCode) where errorCode != 0.

## Testing
Use [spock-framework](https://github.com/spockframework/spock) to implement your unit/integration tests.
Test should be located in the test directory (e.g. `/src/test/groovy/`) in the same package as the class.
Test class name should follow the convention: `${testingClassName}Test` or `${testingClassName}Spec`.

## Logging, println, printStackTrace
The system should have absolutely no `println`, `Exception.printStackTrace` -s in it.
Instead use methods from logger if you need to record a message.
There are a lot of logging frameworks in Java world. You should use API of [SLF4J](http://www.slf4j.org/) project

## Misc
### Always override hashCode() when overriding equals()
This is standard required-Java-practice, see 'Effective Java' by Joshua Bloch Item 8.

### toString()
Only use `.toString()` for debugging purposes.
It's really bad idea to return some VALUE from the object through toString().
It's better to define method like `getValue()` (`getName()`, `getCode()`, etc.) and use it instead of implicit `toString()` call in constructions like the following:

```
UserName username;
DomainName domain;

// Wrong\!
username + "@" + domain

//Use instead
username.getName() + "@" + domain.getName()
```

### Empty methods
The format of empty methods is as follows, the comment needs to clearly note the method is a no-op and why.

```
/** * This method is a no-op as this class is not interested in foo events. */
void foo(){ }
```
## Javadoc
In best cases your code should be readable / understandable without any comments.
Use Javadoc to describe complex classes / methods which are hard to understand from reading the source code.
>Do not comment obvious things !

```
//incorrect

/**
    @return name of the project
*/
public String getName() {
    return name;
}
```

### Class Javadoc
Classes should have Javadoc which describes the main purpose of the class in a few words.

### Method Javadoc
Public methods should have Javadoc.

### @param, @return
Any non-obvious method parameters and return values need to be documented.