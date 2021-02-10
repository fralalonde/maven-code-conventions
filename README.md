# maven-code-conventions ![pyramid](https://github.com/fralalonde/maven-code-conventions/blob/master/logo.png)

# Rationale
- Strong formatting discipline makes better diffs, clearer pull requests.
- Use the same tools across IDE, CLI and CI to format and validate code.
- Rules are defined locally, per project. Decentralization for low coupling and minimal management overhead. 

# Plugins
- [impsort-maven-plugin](https://code.revelc.net/impsort-maven-plugin/)
- [formatter-maven-plugin](https://code.revelc.net/formatter-maven-plugin/)
- [maven-checkstyle-plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/)

# IDE Integration
- [Eclipse](https://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Freference%2Fpreferences%2Fjava%2Fcodestyle%2Fref-preferences-formatter.htm) 
- [IntelliJ](https://plugins.jetbrains.com/plugin/6546-eclipse-code-formatter)

# Usage

Possible values of the `code.format` Maven property:
- `validate` fail the build if source code fails to pass style or formatting check (default). For CI, etc.
- `auto` actively reformat source files as part of compilation process. For development environment.
- `off` deactivate all formatting and checkstyle activity.

Transient usage example
```
mvn -Dcode.format=[auto | off | check] package 
```

Persistent usage example
```
export MAVEN_OPTS="${MAVEN_OPTS} -Dcode.format=[auto | off | check]"
```


# Configuration
Override parent configuration for single module:
```
    <properties>
        <formatter.rules>${project.baseDir}/formatter.xml</formatter.rules>
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
This projects enforces coding conventions at compile time.
Rules are found in the `checkstyle.xml` and `formatter.xml` files.

For portability across CLI, CI and IDE builds, formatting uses a standalone engine based on Eclipse's formatter. 
IntelliJ users may use the [Eclipse Formatter](https://plugins.jetbrains.com/plugin/6546-eclipse-code-formatter) plugin. 

Maven formatting behavior can be controlled through the `code.format` system property:
- `validate` (default) fail the build if source code fails to pass style or formatting check. For CI, etc.
- `auto` actively reformat source files as part of compilation process. For development environment.
- `off` deactivate all formatting and checkstyle activity. For temporary usage.

Example
```
export MAVEN_OPTS="${MAVEN_OPTS} -Dcode.format=[auto | off | check]"
mvn package
```

Imports sorting is not run by default due to the lack of unified mechanism between IDE and Maven.
It can be performed with `mvn impsort:sort` (code formatting must not be `off`)
