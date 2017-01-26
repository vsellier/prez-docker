# Build like a ci

## Initialization

### Read the CI images documentations
### Init the aliases as declared in the CI image documentation
### Clone the platform-ui project
```
# git clone git@github.com:exoplatform/platform-ui.git
```

## Different build environments

```
# jdk8mvn32
jdk8mvn32 -v
Apache Maven 3.2.5 (12a6b3acb947671f09b81f49094c53f426d8cea1; 2014-12-14T17:29:23+00:00)
Maven home: /usr/share/maven
Java version: 1.8.0_92, vendor: Oracle Corporation
Java home: /usr/lib/jvm/java-1.8.0_92-oracle-x64/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "4.9.4-moby", arch: "amd64", family: "unix"
``` 

```
# jdk7mvn30 
Apache Maven 3.0.5 (r01de14724cdef164cd33c7c8c2fe155faf9602da; 2013-02-19 13:51:28+0000)
Maven home: /usr/share/maven
Java version: 1.7.0_79, vendor: Oracle Corporation
Java home: /usr/lib/jvm/java-1.7.0_79-oracle-x64/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "4.9.4-moby", arch: "amd64", family: "unix"
```

```
# which jdk8mvn32
jdk8mvn32 () {
  docker run --rm -v $(pwd):/srv/ciagent/workspace -v ~/.m2/repository:/home/ciagent/.m2/repository -v ~/.m2/settings.xml:/home/ciagent/.m2/settings.xml exoplatform/ci:jdk8-maven32 $*
}
# which jdk7mvn32
jdk7mvn32 () {
  docker run --rm -v $(pwd):/srv/ciagent/workspace -v ~/.m2/repository:/home/ciagent/.m2/repository -v ~/.m2/settings.xml:/home/ciagent/.m2/settings.xml exoplatform/ci:jdk7-maven32 $*
}
```

## Build a project

```
# git clone git@github.com:exoplatform/platform-ui.git$
...
# cd platform-ui
# jdk8mvn32 compile
[INFO] ------------------------------------------------------------------------
[INFO] Reactor Summary:
[INFO]
[INFO] eXo PLF:: Platform-UI .............................. SUCCESS [  3.111 s]
[INFO] eXo PLF:: Platform UI - Skin ....................... SUCCESS [  7.272 s]
[INFO] eXo PLF:: skin add-on packaging .................... SUCCESS [  4.059 s]
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 15.660 s
[INFO] Finished at: 2017-01-26T16:54:33+00:00
[INFO] Final Memory: 29M/990M
[INFO] ------------------------------------------------------------------------

```
