---
icon: creative
title: 精品开源项目
---
## Java 的高性能缓存库

![123](https://xiaolongcoder.oss-cn-beijing.aliyuncs.com/imgs/Java2Top/java/k202304192328446.png)

借鉴了 Guava 和 ConcurrentLinkedHashMap 的设计经验，青出于蓝而胜于蓝的 Java 本地缓存库，拥有更高的缓存命中率和更快的读写速度。

```java
LoadingCache<Key, Graph> graphs = Caffeine.newBuilder()
    .maximumSize(10_000)
    .expireAfterWrite(Duration.ofMinutes(5))
    .refreshAfterWrite(Duration.ofMinutes(1))
    .build(key -> createExpensiveGraph(key));
```

> https://github.com/ben-manes/caffeine