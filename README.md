# Failsafe Helper Library

Failsafe is a lightweight, zero-dependency library for handling failures in Java 8+. It works by intercepting failures and
performing recovery logic via configurable strategies.

This helper library aims to streamline the process of handling failures and offering a more user-friendly interface for
developers to handle failures in Java.

## Table of Contents

- [Installation](#installation)
- [Usage Examples](#usage-examples)
    - [Handling Failures with Retries](#handling-Failures-with-Retries)
    - [Handling Failures with Fallback](#handling-Failures-with-Fallback)

## Installation

To use this Failsafe Utility library in your project, add below Maven dependency to your `pom.xml` file. Make sure to use the
latest version available. This project is deployed to both
the [Maven Central Repository](https://central.sonatype.com/artifact/io.github.rohit-walia/failsafehelper) and the
[GitHub Package Registry](https://github.com/rohit-walia?tab=packages&repo_name=failsafe-helper).

```xml

<dependency>
    <groupId>io.github.rohit-walia</groupId>
    <artifactId>failsafe-helper</artifactId>
    <version>${failsafe-helper.version}</version>
</dependency>
```

## Usage Examples

#### Handling Failures with Retries

Below examples demonstrate how you can use this library for retrying logic on failure. This is especially useful in automated
testing projects where you want to improve the reliability of your tests by wrapping test steps in a retry callback.
Common use cases: login, search and find operations, etc.

```Java
void retryOnFailureExamples() {
  RetryAgain.once(() -> {
    // code here. If it fails, it will retry once before throwing error
  });

  RetryAgain.onceWithDelay(() -> {
    // code here. If it fails, it will retry once, with a 3-second delay, before throwing error
  }, 3);

  RetryUntil.attemptLimit(() -> {
    // code here. If it fails, it will retry twice before throwing error
  }, 2);

  RetryUntil.attemptLimitWithDelay(() -> {
    // code here. If it fails, it will retry twice, with a 3-second delay, before throwing error
  }, 2, 3);
}
```

See [test](failsafehelper\src\test\java\org\failsafe\failsafe\retry) for more examples.

#### Handling Failures with Fallback

Below examples demonstrate how you can use this library for fallback logic on failure. This is especially useful in cases
where you want to fallback to secondary logic if the primary logic fails.

```Java
void fallbackOnFailureExamples() {
  FallbackTo.logger(() -> {
    // primary code here.
  }, "This message will be logged if the primary code throws an exception or error.");
}
```

# Dependencies

### JUnit5

This project uses [JUnit5](https://junit.org/junit5/docs/current/user-guide/) for testing. Tests can be
found [here](failsafehelper/src/test/java/org/failsafe/failsafe).

### Lombok

This project uses lombok to decrease boilerplate code.

### Failsafe

Failsafe is the failure handling and retry library used in this project. See [here](https://failsafe.dev/)
for more information.