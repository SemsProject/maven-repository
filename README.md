SEMS Maven Repository
=====================

This is the [SEMS](http://sems.uni-rostock.de) maven repository, containing all libraries and tools produced
within the SEMS project, along with 3rd party libraries, which might be required to build some of the tools or libraries.
This repository contains two branches:

  * **[releases](https://github.com/SemsProject/maven-repository/tree/releases)** containing all stable releases
  * **[snapshots](https://github.com/SemsProject/maven-repository/tree/snapshots)** containing all test and unstable builds

License
-------

Since this repository contains a wide variety of projects, please refer to the actual project repositories for
detailed license and usage information.


Using this Maven Repository
---------------------------

To allow Maven to automatically fetch the SEMS libraries just add following lines to your `pom.xml`

```xml
<repositories>
    <repository>
        <id>sems-maven-repository-releases</id>
        <name>SEMS Maven Repo</name>
        <url>https://raw.github.com/SemsProject/maven-repository/raw/releases</url>
        <layout>default</layout>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
    </repository>

    <repository>
        <id>sems-maven-repository-snapshots</id>
        <name>SEMS Maven Repo</name>
        <url>https://raw.github.com/SemsProject/maven-repository/raw/snapshots</url>
        <layout>default</layout>
        <releases>
            <enabled>false</enabled>
        </releases>
    </repository>
</repositories>
```


Deploying to this Repository
----------------------------

To deploy to this Maven repository you first of all need access to this git repository,
further you need to have ssh access to GitHub configured.

Next integrate following lines into your `pom.xml`:
```xml
<pluginRepositories>
    <!-- synergian wagon-ssh -->
    <pluginRepository>
        <id>synergian-repo</id>
        <url>https://raw.github.com/synergian/wagon-git/releases</url>
    </pluginRepository>
</pluginRepositories>

<distributionManagement>
    <downloadUrl>https://raw.github.com/SemsProject/maven-repository/raw/</downloadUrl>
    <snapshotRepository>
        <uniqueVersion>true</uniqueVersion>
        <id>sems-maven-repository</id>
        <name>SEMS Maven Release Repository</name>
        <url>git:releases://git@github.com:SemsProject/maven-repository.git</url>
        <layout>default</layout>
    </snapshotRepository>

    <repository>
        <uniqueVersion>true</uniqueVersion>
        <id>sems-maven-repository</id>
        <name>SEMS Maven Snapshot Repository</name>
        <url>git:snapshots://git@github.com:SemsProject/maven-repository.git</url>
        <layout>default</layout>
    </repository>
</distributionManagement>

<build>
    <extensions>
        <!-- enable deployment via git -->
        <extension>
            <groupId>ar.com.synergian</groupId>
            <artifactId>wagon-git</artifactId>
            <version>0.3.0</version>
        </extension>
    </extensions>
    <!-- ... -->
</build>
```
