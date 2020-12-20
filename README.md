# GPR（GitHub Packages）使用指南

## Android Studio 配置全局访问令牌
1. 在根目录下local.properties添加GPR访问令牌
```
gpr.user=username
gpr.key=access token
```

2. 在工程的根目录下build.gradle全局配置kuloud/repos的maven仓库
```groovy
Properties properties = new Properties()
File propertiesFile = project.rootProject.file('local.properties')
if (propertiesFile.exists()) {
    InputStream inputStream = propertiesFile.newDataInputStream()
    properties.load(inputStream)
}

allprojects {
    repositories {
        google()
        jcenter()
        maven {
            url 'https://maven.pkg.github.com/kuloud/repos'
            credentials {
                username = properties.getProperty("gpr.user")
                password = properties.getProperty("gpr.key")
            }
        }
    }
}
```

这样在具体工程里就能使用Gradle的依赖管理，添加指定包依赖。

## 包列表
1. [permissions](https://github.com/Kuloud/permission)
  Android 动态权限管理，API 23+
```groovy
implementation 'com.kuloud.android:permissions:lastestVersion'
```