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

And commons-compress 1.28.0-SNAPSHOT will be selected; this is how Maven 3 always worked.

## Improved in Maven 4

Use Maven 4,0.0-rc-4 and perform following steps:
1. edit POM to be release (remove -SNAPSHOT from version)
2. nuke local `rm -R local` (if not first run)
2. execute Maven4 as this:
```
$ mvn -V -s settings.xml -Dmaven.repo.local=local package -Dmaven.session.versionFilter=s
```

And commons-compress 1.27.1 will be selected due "contextual snapshot filter" (if graph parent is not snapshot,
child from range cannot be snapshot either).
