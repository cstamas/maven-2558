Reproducer for https://github.com/apache/maven/issues/2558

```
$ rm -R local     <- if subsequent run
$ mvn -V -s settings.xml -Dmaven.repo.local=local package
```

And inspect logs:

```
Downloading from central: https://repo.maven.apache.org/maven2/org/apache/commons/commons-compress/maven-metadata.xml
Downloading from apache-snapshot: https://repository.apache.org/content/repositories/snapshots/org/apache/commons/commons-compress/maven-metadata.xml
```

