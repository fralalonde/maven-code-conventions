# maven-code-conventions ![pyramid](logo.png)

# Rationale
- Strong formatting discipline makes better diffs, clearer pull requests.
- Use the same tools across IDE, CLI and CI to format and validate code.
- Rules are defined locally, per project. Decentralization for low coupling and minimal management overhead.

# Plugins
- [impsort-maven-plugin](https://code.revelc.net/impsort-maven-plugin/)
- [formatter-maven-plugin](https://code.revelc.net/formatter-maven-plugin/)
- [maven-checkstyle-plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/)

# IDE Integration
- [Eclipse formatter settings](https://help.eclipse.org/latest/topic/org.eclipse.jdt.doc.user/reference/preferences/java/codestyle/ref-preferences-formatter.htm)
- [Adapter for Eclipse Code Formatter in IntelliJ](https://plugins.jetbrains.com/plugin/6546-adapter-for-eclipse-code-formatter)

Maven 3.6.3+ running on JDK 21+ is required by the current plugins and Checkstyle version. The project still compiles Java 8 source. The IntelliJ adapter bundles its own Eclipse formatter version, so Maven validation is authoritative if IDE output differs.

# Usage

Possible values of the `code.format` Maven property:
- `validate` fails the build if source code fails style or formatting checks (default).
- `auto` reformats source files and sorts imports during the build.
- `off` skips formatting, import sorting, and Checkstyle.

Transient usage example
```
mvn package
mvn -Dcode.format=auto package
mvn -Dcode.format=off package
```

Persistent usage example
```
export MAVEN_OPTS="${MAVEN_OPTS} -Dcode.format=auto"
```


# Configuration
Override parent configuration for single module:
```
    <properties>
        <formatter.rules>${project.basedir}/formatter.xml</formatter.rules>
        [...]
        <checkstyle.rules>checkstyle.xml</checkstyle.rules>
    </properties>
```

Exclude a module from formatting or checkstyle
```
    <properties>
        <formatter.skip>true</formatter.skip>
        [...]
        <checkstyle.skip>true</checkstyle.skip>
    </properties>
```

# Project README.md template
Include and adapt the remaining text in your project's README #Developer section:

## Coding conventions
This project enforces coding conventions during the Maven build.
Rules are found in the `checkstyle.xml` and `formatter.xml` files.

Formatting uses Eclipse JDT through the formatter Maven plugin. IntelliJ users may use the [Adapter for Eclipse Code Formatter](https://plugins.jetbrains.com/plugin/6546-adapter-for-eclipse-code-formatter) plugin with the same `formatter.xml` file.

Maven formatting behavior can be controlled through the `code.format` system property:
- `validate` (default) fails the build if source code fails style or formatting checks.
- `auto` reformats source files and sorts imports during the build.
- `off` skips formatting, import sorting, and Checkstyle temporarily.

Example
```
mvn -Dcode.format=auto package
```

Import sorting is not checked by default because IDE import ordering may differ. The `auto` profile runs impsort, or it can be invoked directly with `mvn net.revelc.code:impsort-maven-plugin:1.13.0:sort`.
