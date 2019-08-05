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

## Multi-module
Install
```
find . -depth 2 -type d -name src | xargs -I {} mkdir {}/lint
find . -depth 3 -type d -name lint | xargs -I {} ln -s ../../../formatter.xml {}/formatter.xml
find . -depth 3 -type d -name lint | xargs -I {} ln -s ../../../checkstyle.xml {}/checkstyle.xml
```
