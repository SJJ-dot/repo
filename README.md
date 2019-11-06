- [okhttp http logging](https://github.com/lTBeL/repo/blob/master/README.md#okhttp-http-logging)

- [字符集检测](https://github.com/lTBeL/repo/blob/master/README.md#%E5%AD%97%E7%AC%A6%E9%9B%86%E6%A3%80%E6%B5%8B)

- [retrofit类型转换，增加字符集检测功能](https://github.com/lTBeL/repo/blob/master/README.md#retrofit%E7%B1%BB%E5%9E%8B%E8%BD%AC%E6%8D%A2%E5%A2%9E%E5%8A%A0%E5%AD%97%E7%AC%A6%E9%9B%86%E6%A3%80%E6%B5%8B%E5%8A%9F%E8%83%BD)

- [android运行时请求权限](https://github.com/lTBeL/repo/blob/master/README.md#android%E8%BF%90%E8%A1%8C%E6%97%B6%E8%AF%B7%E6%B1%82%E6%9D%83%E9%99%90)

- [rxjava取消订阅封装](https://github.com/lTBeL/repo/blob/master/README.md#rxjava%E5%8F%96%E6%B6%88%E8%AE%A2%E9%98%85%E5%B0%81%E8%A3%85)


- [第三方的依赖包](https://github.com/lTBeL/repo/blob/master/README.md#%E7%AC%AC%E4%B8%89%E6%96%B9%E7%9A%84%E4%BE%9D%E8%B5%96%E5%8C%85)

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
#### okhttp http-logging
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
#### android运行时请求权限
```groovy
dependencies {
    ...
    implementation 'com.sjianjun:permission-request:1.1.4'
    //自行添加 必须的依赖项，避免版本冲突 
    compileOnly 'com.android.support:support-annotations:28.0.0'
    compileOnly "org.jetbrains.kotlin:kotlin-stdlib-jdk7:$kotlin_version"
}
```
- 示例代码
```
```kotlin
    PermissionUtil.requestPermissions(
        context,
        arrayOf(Manifest.permission.WRITE_EXTERNAL_STORAGE, Manifest.permission.CALL_PHONE)
    ) {
        Log.e(it.isGranted())
        Log.e(it)
    }
```
#### rxjava取消订阅封装
- 添加依赖
```groovy
dependencies {
    ...
    implementation 'com.sjianjun:rxjava-dispose:1.1.0'
}
```

- 示例代码
```kotlin
class MainActivity : AppCompatActivity(),AutoDispose {

    @SuppressLint("CheckResult")
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        Log.e("test")
        Observable.just("test key")
            .delay(2000, TimeUnit.MILLISECONDS)
            .doOnDispose {
                Log.e("doOnDispose test key")
            }
            .compose(pause("test key", lifecycle))
            .subscribe {
                Log.e(it)
            }
        Observable.just("test key2")
            .delay(10000, TimeUnit.MILLISECONDS)
            .doOnDispose {
                Log.e("doOnDispose test key2")
            }
            .compose(pause("test key"))
            .subscribe {
                Log.e(it)
            }
    }
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

implementation 'com.sjianjun:scheduler:0.0.4'
implementation 'com.sjianjun:serialize:1.0.1'
```
### 第三方库
[Android 权限请求(https://github.com/yanzhenjie/AndPermission)](https://github.com/yanzhenjie/AndPermission)
