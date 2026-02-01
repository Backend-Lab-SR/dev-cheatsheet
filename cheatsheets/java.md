# Java Cheatsheet

## Compilation and Execution

```bash
# Compile Java file
javac MyClass.java

# Run Java program
java MyClass

# Compile with classpath
javac -cp ".:lib/*" MyClass.java

# Run with classpath
java -cp ".:lib/*" MyClass

# Compile multiple files
javac *.java

# Run with specific JVM options
java -Xmx512m -Xms256m MyClass
```

## JAR Operations

```bash
# Create JAR file
jar cvf myapp.jar *.class

# Create executable JAR with manifest
jar cvfm myapp.jar MANIFEST.MF *.class

# Extract JAR file
jar xvf myapp.jar

# List JAR contents
jar tf myapp.jar

# Run JAR file
java -jar myapp.jar
```

## Maven Integration

```bash
# Compile with Maven
mvn compile

# Run with Maven
mvn exec:java -Dexec.mainClass="com.example.MyClass"

# Package and run
mvn package && java -jar target/myapp.jar
```

## Debugging

```bash
# Enable remote debugging
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 MyClass

# Enable JVM debugging flags
java -XX:+PrintGCDetails -XX:+PrintGCTimeStamps MyClass

# Heap dump
jmap -dump:format=b,file=heap.bin <pid>
```

## Classpath Management

```bash
# Set classpath
export CLASSPATH=/path/to/classes:/path/to/lib.jar

# Check classpath
echo $CLASSPATH

# Find class in classpath
find . -name "*.class" | grep MyClass
```

## Process Management

```bash
# Find Java processes
jps -l

# Show Java process details
jps -v

# Kill Java process
kill <pid>

# Force kill
kill -9 <pid>
```

## JVM Monitoring

```bash
# JVM info
java -version

# Show JVM options
java -XX:+PrintFlagsFinal -version | grep -i heap

# Thread dump
jstack <pid>

# Memory info
jstat -gc <pid> 1000
```

## Common JVM Flags

```bash
# Heap size
-Xmx2g          # Maximum heap size
-Xms1g          # Initial heap size

# Garbage collection
-XX:+UseG1GC    # Use G1 garbage collector
-XX:+UseParallelGC  # Use parallel GC

# Debugging
-Xdebug
-Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005

# Logging
-Xlog:gc*:file=gc.log
```
