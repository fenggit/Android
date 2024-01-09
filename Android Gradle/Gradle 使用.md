# Gradle 使用

在 Android Project 中， 在 gradle.properties 文件中，配置 key value，在其他模块的 build.gradle 中可以直接使用



gradle.properties

```
isNeedModule=false
```



settings.gradle

```
if (!isNeedModule.toBoolean()) {
    include ':TestModule'
}
```



TestModule(子module)的build.gradle

```
if (isNeedModule.toBoolean()) {
    //... 
}
```

