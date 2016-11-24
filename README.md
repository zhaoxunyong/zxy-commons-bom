maven/gradle第3方依赖包统一管理
===============
### JDK版本
jdk 1.8+

### gradle版本
gradle 2.14+

### 统一在父项目中引入：
#### maven:
```xml
	<dependencyManagement>
		<dependencies>
			<dependency>
	          <groupId>com.zxy</groupId>
	          <artifactId>zxy-commons-bom</artifactId>
	          <version>${zxy_commons_bom_version}</version>
	          <type>pom</type>
	          <scope>import</scope>
	        </dependency>
		</dependencies>
	</dependencyManagement>
```

#### gradle:
```html
buildscript {
    repositories {
        maven {
            url groupUrl
        }
    }
    dependencies {
        classpath "io.spring.gradle:dependency-management-plugin:0.6.0.RELEASE"
    }
}

dependencyManagement {
    imports {
        mavenBom "com.zxy:zxy-commons-bom:${zxy_commons_bom_version}"
    }
}
```

### 子项目只需要这样引入即可：
#### maven:
```xml
	<dependency>
		<groupId>com.google.guava</groupId>
		<artifactId>guava</artifactId>
	</dependency>
```

#### gradle:
```html
compile 'com.google.guava:guava'
```

这样能做到所有引用的项目不用指定版本号，所依赖的第3方组件版本号都在zxy-commons-bom项目中统一管理。

### 发布到maven仓库：
#### 环境配置：
```html
	修改gradle.properties：
	#snapshot地址
	snapshotsUrl=
	#release地址
	releaseUrl=
	#用户名
	username=
	#密码
	password=
```

#### 安装到本地maven仓库
```html
	./gradlew publishToMavenLocal
```

#### 上传到maven服务器
```html
    ./gradlew publish
```

# 联系方式:
- QQ:
442336467
- 微信:
zhaoxunyong
- email:
zhaoxunyong@qq.com