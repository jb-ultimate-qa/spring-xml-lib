# spring-xml-lib

A library jar with Spring XML files only. The test project [spring-xml-configs-import-multimodule](https://github.com/jb-ultimate-qa/spring-xml-configs-import-multimodule) imports these files with `<import resource>` to check the import resolution from a library jar in IntelliJ IDEA.

## Use

```xml
<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>

<dependency>
    <groupId>com.github.jb-ultimate-qa</groupId>
    <artifactId>spring-xml-lib</artifactId>
    <version>1.0</version>
</dependency>
```

## Content

| File | Beans | Used to check |
|---|---|---|
| `META-INF/qa-lib/lib-context.xml` | `libBean1`, `libBean2`. Imports `extra/lib-extra1.xml` by a relative path. | a concrete `classpath:` import, a relative import inside the jar |
| `META-INF/qa-lib/extra/lib-extra1.xml` | `libExtraBean1` | a `classpath*:` Ant pattern |
| `META-INF/qa-lib/extra/lib-extra2.xml` | `libExtraBean2` | a `classpath*:` Ant pattern |
| `META-INF/qa-lib/lib-a.xml`, `lib-b.xml` | `libQBeanA`, `libQBeanB` | the `?` wildcard (`lib-?.xml`) |
| `META-INF/qa-lib/lib-ab.xml` | `libQBeanAB` | the `?` wildcard must not match it |
| `qa-my-beans.xml` | `suffixBean` | `classpath:my-beans.xml` must not match it by the name suffix |

All beans use `java.util.ArrayList`, so the jar has no classes.

## Release

Create a tag, for example `1.0`. JitPack builds the jar from the tag on the first request.
