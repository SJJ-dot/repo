### 添加存储库
- 项目根目录build.gradle添加存储库
```groovy
allprojects {
    repositories {
        ...
        maven {
            url "https://raw.githubusercontent.com/lTBeL/repo/master/repository"
        }
    }
}
```
- [okhttp http-logging](https://github.com/lTBeL/okhttp-logging)
>http请求日志。增加字符集检测功能，针对部分接口header没返回contenttype导致日志乱码
```groovy
dependencies {
    ...
    implementation 'com.sjianjun:okhttp-logging:0.0.1'
    //自行添加 必须的依赖项，避免版本冲突 
    implementation "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
    implementation 'com.squareup.retrofit2:retrofit:2.6.1'
    implementation 'com.google.code.gson:gson:2.8.6'
}
```
- [字符集检测](https://github.com/lTBeL/okhttp-logging)

网上copy的代码。具体来源已经忘记了。主要使用的第三方的jar包
```groovy
dependencies {
    ...
    implementation 'com.sjianjun:charset-detector:0.0.1'
}
```

```
- [retrofit数据格式化](https://github.com/lTBeL/okhttp-logging)
```groovy
dependencies {
    ...
    implementation 'com.sjianjun:retrofit-converter:0.0.1'
    //自行添加 必须的依赖项，避免版本冲突 
    implementation 'com.squareup.retrofit2:retrofit:2.6.1'
    implementation 'com.google.code.gson:gson:2.8.6'
}
```

- [android运行时请求权限](https://github.com/lTBeL/RTPermission)
```groovy
dependencies {
    ...
    implementation 'com.sjianjun:permission-request:1.1.4'
    //自行添加 必须的依赖项，避免版本冲突 
    compileOnly 'com.android.support:support-annotations:28.0.0'
    compileOnly "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
}
```

- [rxjava取消订阅封装](https://github.com/lTBeL/rxjavautils)

```groovy
dependencies {
    ...
    implementation 'com.sjianjun:rxjava-dispose:1.2.0'
}
```

- [RxJava协程调度器](https://github.com/lTBeL/RxJavaCoroutineScheduler)

```groovy

android{
    ...
    packagingOptions{
        ...
        exclude "META-INF/proguard/coroutines.pro"
    }
}

dependencies {
   ...
    implementation('com.sjianjun:rxjava-coroutine-scheduler:0.0.4')
    ...
}
```


### 第三方的依赖包
#### 字符集检测使用的第三方库（原地址使用gradle始终加载不成功）
```groovy
implementation 'com.sjianjun.ext:chardet:0.0.1'
```

### 以下的库在jcenter仓库
```groovy
//日志工具，打印行号，写入磁盘
implementation 'com.sjianjun:aLog:1.2.2'

//将对象转换为表单或者get请求参数
implementation 'com.sjianjun:retrofitlib:0.0.1'

implementation 'com.sjianjun:serialize:1.0.1'
```
### 第三方库
- [Android 权限请求(https://github.com/yanzhenjie/AndPermission)](https://github.com/yanzhenjie/AndPermission)

- [Flexbox for Android](https://github.com/google/flexbox-layout)
