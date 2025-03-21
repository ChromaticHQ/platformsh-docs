---
title: "Java"
description: Java is a general-purpose programming language, and one of the most popular in the world today. Platform.sh supports Java runtimes that can be used with build management tools such as Gradle, Maven, and Ant.
layout: single
---

{{< description >}}

## Supported versions

### OpenJDK versions:

| **Grid** | **Dedicated** |
|----------------------------------|---------------|
|  {{< image-versions image="java" status="supported" environment="grid" >}} | {{< image-versions image="java" status="supported" environment="dedicated" >}} |

{{< image-versions-legacy "java" >}}

{{% language-specification type="java" display_name="Java" %}}

## Support libraries

While it is possible to read the environment directly from your application, it is generally easier and more robust to use the [`platformsh/config-reader`](https://github.com/platformsh/config-reader-java) which handles decoding of service credential information for you.

## Support build automation

Platform.sh supports the most common project management tools in the Java ecosystem, including:

* [Gradle](https://gradle.org/)
* [Maven](https://maven.apache.org/)
* [Ant](https://ant.apache.org/)

## Other JVM languages

It’s worth remembering that the JVM by its specification [does not read Java code](https://docs.oracle.com/javase/specs/jvms/se8/html/index.html), but bytecode. So within the JVM, it’s possible to [run several languages](https://en.wikipedia.org/wiki/List_of_JVM_languages). Platform.sh supports several of them, such as Kotlin, Groovy, and Scala, so long as that language works with any build automation that Platform.sh supports.

| Article                                                      | Link                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [Kotlin and Spring](https://platform.sh/blog/2019/ready-to-have-fun-try-kotlin-and-spring/) | [Source](https://github.com/platformsh-templates/spring-kotlin) |
| [Scala and Spring](https://dzone.com/articles/spring-scala-cloud-psh) | [Source](https://github.com/platformsh-examples/scala)       |
| [Groovy and Spring](https://dzone.com/articles/spring-groovy-cloud-psh) | [Source](https://github.com/platformsh-examples/groovy)      |

## Accessing services

To access various [services](../../add-services/_index.md) with Java, see the following examples.  The individual service pages have more information on configuring each service.

{{< codetabs >}}

---
title=Elasticsearch
file=static/files/fetch/examples/java/elasticsearch
highlight=java
---

<--->

---
title=Kafka
file=static/files/fetch/examples/java/kafka
highlight=java
---

<--->

---
title=Memcached
file=static/files/fetch/examples/java/memcached
highlight=java
---

<--->

---
title=MongoDB
file=static/files/fetch/examples/java/mongodb
highlight=java
---

<--->

---
title=MySQL
file=static/files/fetch/examples/java/mysql
highlight=java
---

<--->

---
title=PostgreSQL
file=static/files/fetch/examples/java/postgresql
highlight=java
---

<--->

---
title=RabbitMQ
file=static/files/fetch/examples/java/rabbitmq
highlight=java
---

<--->

---
title=Redis
file=static/files/fetch/examples/java/redis
highlight=java
---

<--->

---
title=Solr
file=static/files/fetch/examples/java/solr
highlight=java
---

{{< /codetabs >}}

 {{< note >}}
These samples use the [Configuration Reader library](https://github.com/platformsh/config-reader-java) that Platform.sh provides. However, if your favorite Java frameworks allow you to overwrite the configurations following [The Twelve-Factor App](https://12factor.net/config) (such as Spring, Micronaut, Quarkus, Jakarta EE/MicroProfile), then as a developer you have the option to not use the library, removing the need for an additional dependency.
{{< /note >}}

## Project templates

A number of project templates for major Java applications are available on GitHub. Not all of them are proactively maintained but all can be used as a starting point or reference for building your own website or web application.

{{< repolist lang="java" >}}
