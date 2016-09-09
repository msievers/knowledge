---
title: docker-compose
keywords: docker docker-compose
sidebar: knowledge_sidebar
permalink: docker-compose.html
folder: knowledge
---

## Mac

## Ubuntu

### Prerequisites

* [Docker](setup_docker.html)

### Example

```yml
 1  version: '2'
 2  volumes:
 3   pgdata-volume:
 4     driver: local
 5
 6  services:
 7    postgres:
 8      image: "postgres:9.5"
 9      ports:
10        - "5432:5432"
11      volumes:
12        - pgdata-volume:/var/lib/postgresql/data
13
14    redis:
15      image: redis
16      ports:
17        - "6379:6379"
```

## Links
* [https://www.linux.com/learn/docker-volumes-and-networks-compose](https://www.linux.com/learn/docker-volumes-and-networks-compose)
* [http://stackoverflow.com/questions/36011595/docker-named-volumes-vs-doc-data-only-containers](http://stackoverflow.com/questions/36011595/docker-named-volumes-vs-doc-data-only-containers)

{% include links.html %}
