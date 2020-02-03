# maven-code-conventions ![pyramid](https://github.com/fralalonde/maven-code-conventions/blob/master/logo.png)

# Rationale
Strong formatting discipline makes better diffs, clearer pull requests.
Use the same tools across IDE, CLI and CI to format and validate code.

# Plugins
- [impsort-maven-plugin](https://code.revelc.net/impsort-maven-plugin/)
- [formatter-maven-plugin](https://code.revelc.net/formatter-maven-plugin/)
- [maven-checkstyle-plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/)

# IDE Integration
- [Eclipse](https://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Freference%2Fpreferences%2Fjava%2Fcodestyle%2Fref-preferences-formatter.htm) 
- [IntelliJ](https://plugins.jetbrains.com/plugin/6546-eclipse-code-formatter)

# Usage

Transient usage example
```
mvn -Dcode.format=[auto | off | check] package 
```

Persistent usage example
```
export MAVEN_OPTS="${MAVEN_OPTS} -Dcode.format=[auto | off | check]"
```

# Configuration
Single module POM configuration properties:
```
    <properties>
        <formatter.rules>../formatter.xml</formatter.rules>
        [...]
        <checkstyle.rules>../checkstyle.xml</checkstyle.rules>
    </properties>
```

Flat multi-module configuration
```
    <properties>
        <formatter.rules>../formatter.xml</formatter.rules>
        [...]
        <checkstyle.rules>../checkstyle.xml</checkstyle.rules>
    </properties>
```

Exclude a module from formatting
```
    <properties>
        <formatter.skip>false</formatter.skip>
        [...]
        <checkstyle.skip>false</checkstyle.skip>
    </properties>
```

Deep multi-module  or per-module configuration 
```
ln -s ../formatter.xml .
ln -s ../checkstyle.xml .
```
Or use actual copies to allow custom rules per module (preferably don't).

