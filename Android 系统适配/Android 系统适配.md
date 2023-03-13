# Android 系统适配

## Android 开发版本参数

在 build.gradle 文件下：

```
android {
    compileSdkVersion 33
    buildToolsVersion '33.0.1'

    defaultConfig {
        applicationId "com.test.example"
        minSdkVersion 21
        targetSdkVersion 33
        versionCode 1
        versionName 1.0.0
    }
}
```



Android 应用开发主要关注：

- **minSdkVersion**：当前App支持最低的 Android 系统
- **targetSdkVersion**：支持到 Android 什么系统版本的 API，一般系统兼容都是设置这个，比如 Android 5.0
- compileSdkVersion：编译的时候，会通过这个检查 API 的行为规范
- buildToolsVersion：
- versionCode：版本号，每次发布新版本需要+1，不然无法升级
- versionName：版本号名称，用于App展示当前什么版本的，升级版本的时候使用



## Android 系统版本号

[Android 系统版本号](https://developer.android.com/guide/topics/manifest/uses-sdk-element?hl=zh-cn#ApiLevels)



