# ssl-boot

Patched JDK internal class `sun.security.ssl.Record` in order to reduce default SSL input buffer.

This patch reduces default buffer size from 16K to 8K.

## Rational

Since JDK doesn't have a memory pool built-in, it allocates a fix-sized buffer for every TLS connection as input buffer. The default size of the buffer is 16KB, which leads to significant heap memory footprint when you have a large number of secure connections.

## Usage

Checkout this repository and find module for your JDK version.

Build the module with

```
mvn install
```

Find generated jar package in `target`. To use this patched version, you will need to prepend the package to **bootstrap classpath**:

```
-Xbootclasspath/p:ssl-boot-<jdk-version>-<version>.jar
```

Then benefit.
