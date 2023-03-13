# Android 暗黑模式

在 Android 和 iOS 平台上，暗黑模式叫深色模式。

Android 深色模式设置：https://developer.android.com/guide/topics/ui/look-and-feel/darktheme?hl=zh-cn

## 一、系统默认的暗黑模式

在 Android 10 (API 级别 29) 及更高版本中提供深色主题背景，开发者只需要设置暗黑模式就可以了，不需要额外设置颜色、图片、资源文件。

### 1、设置暗黑模式

使用系统提供的暗黑主题

```
<style name="AppTheme" parent="Theme.AppCompat.DayNight">
```

MaterialComponent 的深色主题背景

```
<style name="AppTheme" parent="Theme.MaterialComponents.DayNight">
```

### 2、强制暗黑模式

```
android:forceDarkAllowed="true"
```



## 二、自定义的暗黑模式

### 1、当前页面暗黑模式

在需要深色模式的 Activity 页面，设置 **localNightMode**后，注意 Activity 的生命周期会触发 2次：

```kotlin
// 深色模式
delegate.localNightMode = AppCompatDelegate.MODE_NIGHT_YES

// 明亮模式（非深色模式）
delegate.localNightMode = AppCompatDelegate.MODE_NIGHT_NO
```



如果不想 Activity 的生命周期会触发 2次，设置 Activity的 configChanges 为 uiMode。按照官方文档的说法：

> 当某个 Activity 声明它会处理配置变更时，系统会在出现主题背景变更时调用该 Activity 的 onConfigurationChanged() 方法。

但是，实际开发中（红米手机），并没有触发onConfigurationChanged() 。

```
<activity
    android:name="com.test.example.MainActivity"
    android:configChanges="uiMode"
/>
```



设置暗黑模式的资源，在资源文件夹命名上加 **-night**

| 默认模式         | 暗黑模式               |
| ---------------- | ---------------------- |
| values           | values-night           |
| drawable         | drawable-night         |
| drawable-xxhdpi  | drawable-night-xxhdpi  |
| drawable-xxxhdpi | drawable-night-xxxhdpi |
| mipmap-hdpi      | mipmap-night-hdpi      |



Tips：实际开放中，设置 Activity 的深色模式，如果 View 是通过动态 addView 到当前页面，深色模式并没有生效，只有在 Xml 中的View才生效。



### 2、设置应用级别暗黑模式

```kotlin
// 开启暗黑模式
AppCompatDelegate.setDefaultNightMode(AppCompatDelegate.MODE_NIGHT_YES)

// 关闭暗黑模式
AppCompatDelegate.setDefaultNightMode(AppCompatDelegate.MODE_NIGHT_NO)
```

这种模式需要重新创建 Activity，才可以生效

### 3、WebView 暗黑模式

#### 第一种方式

引入：

```
implementation 'androidx.webkit:webkit:1.2.0'
```

设置暗黑模式：

```
// 开启暗黑模式
WebSettingsCompat.setForceDark(webSetting, WebSettingsCompat.FORCE_DARK_ON);	

// 关闭暗黑模式
WebSettingsCompat.setForceDark(webSetting, WebSettingsCompat.FORCE_DARK_OFF);
```

不过这种方式，有兼容问题，这和WebView的版本有关，WebView版本独立于Android版本。



#### 第二种方式

通过 WebView 的 API 实现。

```
//强制开启暗黑模式
mWebView.getSettings().setForceDark(WebSettings.FORCE_DARK_ON);

// 关闭暗黑模式
mWebView.getSettings().setForceDark(WebSettings.FORCE_DARK_OFF);
```

