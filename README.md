redis-maven-plugin [![Build Status](https://buildhive.cloudbees.com/job/r351574nc3/job/redis-maven-plugin/badge/icon)](https://buildhive.cloudbees.com/job/r351574nc3/job/redis-maven-plugin/)
==================

Maven plugin to embed a redis-server based on the redis-protocol
project. This is an in-memory redis server. That means that when the
server shutsdown or closes, the data is no longer available.

Running with Integration Tests
====================
Just add the following plugin. The redis plugin is automatically
attached to the pre-integration-test and post-integration-test
phases. 

```
<plugin>
    <groupId>org.kualigan.maven.plugins</groupId>
    <artifactId>redis-maven-plugin</artifactId>
    <version>${redis-maven-plugin.version}</version>
</plugin>
```


Attaching to Another Phase
==================
In case (for whatever reason), you don't want your redis server
started/stopped with integration tests, here's how you would configure it.

```
<plugin>
    <groupId>org.kualigan.maven.plugins</groupId>
    <artifactId>redis-maven-plugin</artifactId>
    <version>${redis-maven-plugin.version}</version>
    <executions>
        <execution>
            <id>start-redis</id>
            <phase>generate-resources</phase>
            <goals>
                <goal>start</goal>
            </goals>
        </execution>
        <execution>
            <id>stop-redis</id>
            <phase>compile</phase>
            <goals>
                <goal>stop</goal>
            </goals>
        </execution>      
    </executions>
</plugin>
```

Running Unforked
============
Sometimes there is a need to just crank up a redis server while you're
running your project, but you're not running integration tests. For
example, maybe you're running a tomcat7 instance of your application
that requires an embedded redis server. We can do that! Or maybe
you just need a quick redis server for whatever.

Add the following to your ```$HOME/.m2/settings.xml```

```
<settings>
    <pluginGroups>
        <pluginGroup>org.kualigan.maven.plugins</pluginGroup>
    </pluginGroups>
...
...
</settings>
```

Execute the following 

```
mvn redis-server:start-no-fork
```

SNAPSHOTS
=============

The latest snapshots can be found at
[https://oss.sonatype.org/content/repositories/snapshots/org/kualigan/maven/plugins/redis-maven-plugin/]
(Sonatype Nexus SNAPSHOTS)
