# Maven Cheatsheet

## Basic Commands

```bash
# Clean build artifacts
mvn clean

# Compile source code
mvn compile

# Run tests
mvn test

# Package application
mvn package

# Install to local repository
mvn install

# Deploy to remote repository
mvn deploy

# Clean and install
mvn clean install

# Skip tests
mvn install -DskipTests

# Skip test compilation
mvn install -Dmaven.test.skip=true
```

## Lifecycle Commands

```bash
# Validate project
mvn validate

# Compile sources
mvn compile

# Compile test sources
mvn test-compile

# Run tests
mvn test

# Package JAR/WAR
mvn package

# Integration tests
mvn verify

# Install to local repo
mvn install

# Deploy to remote repo
mvn deploy
```

## Dependency Management

```bash
# Display dependency tree
mvn dependency:tree

# Display dependency tree (verbose)
mvn dependency:tree -Dverbose

# Resolve dependencies
mvn dependency:resolve

# Copy dependencies to directory
mvn dependency:copy-dependencies

# Analyze dependencies
mvn dependency:analyze

# List all dependencies
mvn dependency:list
```

## Plugin Commands

```bash
# Run specific plugin goal
mvn exec:java -Dexec.mainClass="com.example.Main"

# Run with arguments
mvn exec:java -Dexec.mainClass="com.example.Main" -Dexec.args="arg1 arg2"

# Compile with specific Java version
mvn clean compile -Dmaven.compiler.source=11 -Dmaven.compiler.target=11

# Run Spring Boot application
mvn spring-boot:run

# Build Docker image
mvn dockerfile:build

# Generate site documentation
mvn site
```

## Multi-Module Projects

```bash
# Build specific module
mvn install -pl module-name

# Build module and dependencies
mvn install -pl module-name -am

# Build from specific directory
mvn install -f path/to/pom.xml

# Reactor options
mvn install -rf :module-name  # Resume from module
mvn install -pl :module-name  # Build only module
```

## Profiles

```bash
# Activate profile
mvn install -Pprofile-name

# Activate multiple profiles
mvn install -Pprofile1,profile2

# List active profiles
mvn help:active-profiles

# Show effective POM
mvn help:effective-pom

# Show effective settings
mvn help:effective-settings
```

## Debugging and Troubleshooting

```bash
# Run with debug output
mvn -X install

# Run with error output
mvn -e install

# Offline mode
mvn -o install

# Update snapshots
mvn -U install

# Check for updates
mvn versions:display-dependency-updates
mvn versions:display-plugin-updates

# Show Maven version
mvn -version
```

## Common Options

```bash
# Quiet mode
mvn -q install

# Batch mode (non-interactive)
mvn -B install

# Thread count
mvn -T 4 install

# Fail fast
mvn -ff install

# Also make (-am), also make dependents (-amd)
mvn install -am -amd
```

## Repository Management

```bash
# Clean local repository cache
mvn dependency:purge-local-repository

# Download sources
mvn dependency:sources

# Download javadoc
mvn dependency:resolve -Dclassifier=javadoc

# Update parent version
mvn versions:update-parent

# Update dependencies
mvn versions:use-latest-versions
```

## Useful Aliases

```bash
# Quick build
alias mci='mvn clean install'
alias mcit='mvn clean install -DskipTests'
alias mcp='mvn clean package'
alias mct='mvn clean test'

# With skip tests
alias mcis='mvn clean install -DskipTests'
```
