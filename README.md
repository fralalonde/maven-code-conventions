# maven-code-conventions ![pyramid](https://github-studio.bnc.ca/raw/LALF004/maven-code-quality/master/logo.png)

Plugins
- [impsort-maven-plugin](https://code.revelc.net/impsort-maven-plugin/)
- [formatter-maven-plugin](https://code.revelc.net/formatter-maven-plugin/)
- [maven-checkstyle-plugin](https://maven.apache.org/plugins/maven-checkstyle-plugin/)
- [javac](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/javac.html)

How
- [Eclipse](https://help.eclipse.org/neon/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2Freference%2Fpreferences%2Fjava%2Fcodestyle%2Fref-preferences-formatter.htm) 
- [IntelliJ](https://plugins.jetbrains.com/plugin/6546-eclipse-code-formatter)
- Maven:
```
mvn formatter:format
mvn net.revelc.code:impsort-maven-plugin:sort
```

Automatic
```
mvn -Dcode.format=auto package 
```
Permanent
```
export MAVEN_OPTS=-Dcode.format=auto
```

## Multi-module project
To enable rules per submodule, create a link in each module to the root rule files: 
```
ln -s ../formatter.xml validated
ln -s ../checkstyle.xml validated
```
Or use actual copies to allow custom rules per module (preferably don't).

Alternately, forcibly enable rules for all submodules by changing the value of the `checkstyle.rules` and `formatter.rules` 
in the root POM to point to the rule file at the root of the project.
```
<formatter.rules>../formatter.xml</formatter.rules>
<checkstyle.rules>../checkstyle.xml</checkstyle.rules>
```
This method will not work if the top project also has an `src` folder that needs to be validated (as in this example project). 
You may try using parametric recursive variations of this method if the project has multiple layers of submodules.

