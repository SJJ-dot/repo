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

### 列表
- okhttp http请求日志。增加字符集检测功能，针对部分接口header没返回contenttype导致日志乱码
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
- 示例代码
```
    val test = Retrofit.Builder()
        .baseUrl("http://www.xbiquge.la")
        .client(
            OkHttpClient
                .Builder()
                .connectTimeout(10, TimeUnit.SECONDS)
                .writeTimeout(10, TimeUnit.SECONDS)
                .readTimeout(10, TimeUnit.SECONDS)
                .addInterceptor(HttpLoggingInterceptor {
                    Log.e(it)
                }.setLevel(HttpLoggingInterceptor.Level.BODY))
                .build()
        )
        .addConverterFactory(ScalarsConverterFactory.create())
        .addCallAdapterFactory(RxJava2CallAdapterFactory.createWithScheduler(CoroutineScheduler.IO))
        .build()
```
#### 字符集检测
网上copy的代码。具体来源已经忘记了。主要使用的第三方的jar包
```groovy
dependencies {
    ...
    implementation 'com.sjianjun:charset-detector:0.0.1'
}
```
- 示例代码
```
String charsetStr = CharsetDetector.detectCharset(buffer.inputStream());
```
#### retrofit类型转换，增加字符集检测功能
```groovy
dependencies {
    ...
    implementation 'com.sjianjun:retrofit-converter:0.0.1'
    //自行添加 必须的依赖项，避免版本冲突 
    implementation 'com.squareup.retrofit2:retrofit:2.6.1'
    implementation 'com.google.code.gson:gson:2.8.6'
}
```
- 示例代码
```
    val test = Retrofit.Builder()
        .addConverterFactory(GsonCharsetCompatibleConverter.create())
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
//运行时权限请求
implementation 'com.sjianjun:permissionUtil:1.1.3'
//将对象转换为request body
implementation 'com.sjianjun:retrofitlib:0.0.1'
//rx请求取消封装
implementation 'com.sjianjun:rxutils:1.0.5'
implementation 'com.sjianjun:scheduler:0.0.4'
implementation 'com.sjianjun:serialize:1.0.1'
```
### 第三方库收集
[Android 权限请求(https://github.com/yanzhenjie/AndPermission)](https://github.com/yanzhenjie/AndPermission)
