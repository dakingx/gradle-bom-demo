# Environment
- JDK 17
- Gradle 8.2.1
- Kotlin 1.8.0

# Process

Publish BOM

```shell
$ cd bom-producer
$ ./gradlew :common-bom:publishReleasePublicationToMavenLocal
```

Back to root directory

```shell
$ cd ..
```

Check bom-consumer-kt project's dependencies

```shell
$ cd bom-consumer-kt
$ ./gradlew -q :app:dependencies --configuration compileClasspath
```

```
compileClasspath - Compile classpath for compilation 'main' (target  (jvm)).
+--- org.jetbrains.kotlin:kotlin-stdlib-jdk8:1.8.0
|    +--- org.jetbrains.kotlin:kotlin-stdlib:1.8.0
|    |    +--- org.jetbrains.kotlin:kotlin-stdlib-common:1.8.0
|    |    \--- org.jetbrains:annotations:13.0
|    \--- org.jetbrains.kotlin:kotlin-stdlib-jdk7:1.8.0
|         \--- org.jetbrains.kotlin:kotlin-stdlib:1.8.0 (*)
+--- tech.daking.mobile:common-bom:0.0.1-SNAPSHOT
|    \--- org.apache.httpcomponents.client5:httpclient5:5.2 (c)
\--- org.apache.httpcomponents.client5:httpclient5 -> 5.2
     +--- org.apache.httpcomponents.core5:httpcore5:5.2
     +--- org.apache.httpcomponents.core5:httpcore5-h2:5.2
     |    \--- org.apache.httpcomponents.core5:httpcore5:5.2
     \--- org.slf4j:slf4j-api:1.7.36
```

Check dependency 'httpclient5'

```shell
$ ./gradlew -q :app:dependencyInsight --dependency httpclient5 --configuration compileClasspath
```

```
org.apache.httpcomponents.client5:httpclient5:5.2 (by constraint)
  Variant compile:
    | Attribute Name                     | Provided | Requested    |
    |------------------------------------|----------|--------------|
    | org.gradle.status                  | release  |              |
    | org.gradle.category                | library  | library      |
    | org.gradle.libraryelements         | jar      | classes      |
    | org.gradle.usage                   | java-api | java-api     |
    | org.gradle.dependency.bundling     |          | external     |
    | org.gradle.jvm.environment         |          | standard-jvm |
    | org.gradle.jvm.version             |          | 8            |
    | org.jetbrains.kotlin.platform.type |          | jvm          |

org.apache.httpcomponents.client5:httpclient5:5.2
\--- tech.daking.mobile:common-bom:0.0.1-SNAPSHOT
     \--- compileClasspath

org.apache.httpcomponents.client5:httpclient5 -> 5.2
\--- compileClasspath
```

Check dependency 'moshi-kotlin'

```shell
$ ./gradlew -q :app:dependencyInsight --dependency moshi-kotlin --configuration compileClasspath
```

```
No dependencies matching given input were found in configuration ':app:compileClasspath'
```
