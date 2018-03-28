---
title: Android Retrofit
date: 2018-01-13
tags:
- Android
- Retrofit
- 网络请求
categories:
- Android
---
### Retrofit
#### 入门
##### Retrofit将你的HTTP API变成一个Java接口
```
public interface GitHubService{
     @GET("users/{user}/repos")
      Call<List<Repo>> listRepos(@Path("user") String user);
}
```
##### Retrofit类生成一个GitHubService接口的实现
```
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://api.github.com/")
    .build();

GitHubService service = retrofit.create(GitHubService.class);
```
##### 调用GitHubService可以同步或异步访问远程的服务器
```
Call<List<Repo>> repos = service.listRepos("octocat");
```
##### 使用注解描述HTTP请求
* 支持URL参数的替换和Query
* 对象转换成请求体
* 多类型的请求体和文件上传
#### API 说明
在接口方法上注解，并说明这个请求需要的参数。
#### 请求方法
每一个方法必须有一个HTTP注解提供请求方法（GET、POST等）和相对的URL。有五个内置注解：GET,POST,PUT,DELETE和HEAD.在注解中指定子资源的相对URL.你也可以
在URL中添加问号参数。
```
@GET("users/list?sort=desc")
```
#### URL操作
可以在请求的URL中使用参数和块动态的更新。一个替换块是一个使用{}包含的字符数字字符串。相应的参数必须使用@path注解。
```
@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId);
```
#### 也可以添加Query参数
```
@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId, @Query("sort") String sort);
```
#### 复杂的query参数组合可以使用一个map
```
@GET("group/{id}/users")
Call<List<User>> groupList(@Path("id") int groupId, @QueryMap Map<String, String> options);
```
#### 可以使用一个@body注解的对象作为HTTP请求的请求体
```
@POST("users/new")
Call<User> createUser(@Body User user);
```
##### The object will also be converted using a converter specified on the Retrofit instance. If no converter is added, only RequestBody can be used.
#### FORM和MULTIPART
##### 也可以使用form-encoded和mutipart方法
##### 在方法上添加@FormUrlEncoded可以发送Form-encoded数据，每一个键值对可使用@Field注解名字和这个对象提供的值
```
@FormUrlEncoded
@POST("user/edit")
Call<User> updateUser(@Field("first_name") String first, @Field("last_name") String last);
```
##### 在方法上添加@Multipart注解来使用Multipart请求，Parts使用@Part注解
```
@Multipart
@PUT("user/photo")
Call<User> updateUser(@Part("photo") RequestBody photo, @Part("description") RequestBody description);
```
##### Multipart的parts使用实现RequestBody的Retrofit的转换器实现他们自己的序列化
####  HEADER操作
##### 你可以使用@Headers设置静态的头方法
```
@Headers("Cache-Control: max-age=640000")
@GET("widget/list")
Call<List<Widget>> widgetList();

@Headers({
    "Accept: application/vnd.github.v3.full+json",
    "User-Agent: Retrofit-Sample-App"
})
@GET("users/{username}")
Call<User> getUser(@Path("username") String username);
```
##### 注意headers不会相互覆盖，所有的headers都包含在请求里面
##### 请求头可以使用@Header注解动态更新，@Header必须提供相应的参数，如果值为null这个header被忽略。否则这个值将调用toString方法并被使用。
```
@GET("user")
Call<User> getUser(@Header("Authorization") String authorization)
```
##### 可以使用okhttp的interceptor（拦截器）将headers加入到每一个请求中
#### SYNCHRONOUS VS. ASYNCHRONOUS（同步和异步对比）
##### Call实例可以同步或异步执行。每一个实例只能用一次，如果需要重复使用可以使用clone()方法创建一个新的实例在使用。
##### 在Android中回调执行在主线程，在JVM中回调发生在执行HTTP请求的相同线程中。
#### CONVERTERS转换器
##### 默认情况Retrofit只可以将HTTP请求体反序列化为Okttp的ResponseBody类型，他只能接受@body注解的RequestBody
##### Converters可以添加支持其他类型。提供6个兄弟模块适配常用的序列化库
* Gson: com.squareup.retrofit2:converter-gson
* Jackson: com.squareup.retrofit2:converter-jackson
* Moshi: com.squareup.retrofit2:converter-moshi
* Protobuf: com.squareup.retrofit2:converter-protobuf
* Wire: com.squareup.retrofit2:converter-wire
* Simple XML: com.squareup.retrofit2:converter-simplexml
* Scalars (primitives, boxed, and String): com.squareup.retrofit2:converter-scalars
##### 这是一个GitHubService接口使用GsonConverterFactory工厂类实现Gson反序列化的实例
```
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://api.github.com")
    .addConverterFactory(GsonConverterFactory.create())
    .build();

GitHubService service = retrofit.create(GitHubService.class);
```
#### 自定义转换器
##### 创建一个继承Converter.Factory的类传一个实例构建你的适配器。
#### Maven
```
<dependency>
  <groupId>com.squareup.retrofit2</groupId>
  <artifactId>retrofit</artifactId>
  <version>2.3.0</version>
</dependency>
```
#### Gradle
```
compile 'com.squareup.retrofit2:retrofit:2.3.0'
```
#### PROGUARD混淆
```
# Platform calls Class.forName on types which do not exist on Android to determine platform.
-dontnote retrofit2.Platform
# Platform used when running on Java 8 VMs. Will not be used at runtime.
-dontwarn retrofit2.Platform$Java8
# Retain generic type information for use by reflection by converters and adapters.
-keepattributes Signature
# Retain declared checked exceptions for use by a Proxy instance.
-keepattributes Exceptions
```