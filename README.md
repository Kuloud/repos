# GPR（GitHub Packages）使用指南
## 配置全局Access Token
通过编辑 ~/.m2/settings.xml 文件以包含个人访问令牌，可以使用 Apache Maven 向 GitHub Packages 验证。 如果 ~/.m2/settings.xml 文件不存在，请新建该文件。

配置如下：
```xml
<settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0
                      http://maven.apache.org/xsd/settings-1.0.0.xsd">

  <activeProfiles>
    <activeProfile>github</activeProfile>
  </activeProfiles>

  <profiles>
    <profile>
      <id>github</id>
      <repositories>
        <repository>
          <id>central</id>
          <url>https://repo1.maven.org/maven2</url>
          <releases><enabled>true</enabled></releases>
          <snapshots><enabled>true</enabled></snapshots>
        </repository>
        <repository>
          <id>github</id>
          <name>GitHub kuloud Apache Maven Packages</name>
          <url>https://maven.pkg.github.com/kuloud/repos</url>
        </repository>
      </repositories>
    </profile>
  </profiles>

  <servers>
    <server>
      <id>github</id>
      <username>USERNAME</username>
      <password>TOKEN</password>
    </server>
  </servers>
</settings>
```

将自己的Github Username和Token进行server内容的替换，这样就可以使用自己的Github访问令牌全局的访问 kuloud/repos 下的包。

## Android Studio 配置
在工程的根目录下build.gradle对所有仓库配置kuloud/repos的maven仓
```groovy
allprojects {
    repositories {
        google()
        jcenter()
        maven {
            url 'https://maven.pkg.github.com/kuloud/repos'
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