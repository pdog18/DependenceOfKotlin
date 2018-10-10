

> 来源 https://github.com/handstandsam/AndroidDependencyManagement

## 为什么要这样做？
1. 统一管理
2. 可以点击变量跳转


### 一、
在 `buildSrc` 中创建 `build.gradle.kts` 
```
plugins {
    `kotlin-dsl`
}
```

在 `buildSrc` 创建 `src/main/java/Dependencies.kt` 

```kotlin
object Versions {
// ...
    internal const val android_gradle_plugin = "3.0.1"
    internal const val constraint_layout = "1.1.3"
}

object Deps {
// ...
    const val android_gradle_plugin = "com.android.tools.build:gradle:${Versions.android_gradle_plugin}"
    const val constraint_layout = "com.android.support.constraint:constraint-layout:${Versions.constraint_layout}"
}
```


### 二、
在各种`build.gradle` 配置文件中使用
```
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath Deps.android_gradle_plugin
        classpath Deps.kotlin_gradle_plugin
    }
}
```