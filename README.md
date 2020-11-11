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

