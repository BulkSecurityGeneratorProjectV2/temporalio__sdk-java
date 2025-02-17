# Temporal Test Workflow Server

This module includes an in-memory Temporal testing service implementation. It is
not intended to be used directly but rather by programming against the
`TestWorkflowEnvironment` interface in the `temporal-testing` module.

In addition to being consumed as a library by JVM-based languages, this module
can be built into a standalone executable and run as an independent process.

## Usage

Do not depend on this module directly, see the instructions in
[temporal-testing](../temporal-testing/README.md).

## In-memory Temporal testing service 

This service allows to run a test-only in-memory implementation of Temporal server API.

## To build a test server using GraalVM native-image

From the root of the java-sdk repo:
```
./gradlew :temporal-test-server:build
```
This will give you a native executable `build/graal/temporal-test-server`. The
executable requires a single argument: the port number on which it should
listen.

## To build a test server docker image

From the root of the java-sdk repo:
```
./gradlew :temporal-test-server:docker
```

This will result in a local image being built:
`temporalio/temporal-test-server`.

## GraalVM native-image configuration

The GraalVM native-image compiler uses the native-image.properties file and the
referenced JSON files during compilation. The JSON files are generated by
running the test server java code in a JVM configured with the [GraalVM tracing
agent](https://www.graalvm.org/reference-manual/native-image/Agent/) configured,
e.g. with the flag
`-agentlib:native-image-agent=config-output-dir=temporal-test-server/src/main/resources/META-INF/native-image/io.temporal/temporal-test-server`.
