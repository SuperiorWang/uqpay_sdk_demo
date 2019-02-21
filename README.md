# 手机支付控件接入指南(v1.0)
    
#### 1、 引用sdk库方法
* project的 `build.gradle`文件中增加如下代码：
  ```xml
    allprojects {
        repositories {
            maven { url "https://jitpack.io" }
        }
    }
   ```
* module的 `build.gradle`文件中增加maven:
  ```xml
    implementation 'com.github.SuperiorWang:uqpay_sdk_android:v1.0'
   ```

* `AndroidManifest.xml`文件中添加权限:
  ```xml
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.CHANGE_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
    <uses-permission android:name="android.permission.NFC" />
    <uses-feature android:name="android.hardware.nfc.hce"/>
    <uses-permission android:name="org.simalliance.openmobileapi.SMARTCARD" />
    ```
 
#### 2、 使用到的接口函数
  ```java
    //启动支付控件的接口
    UQPaySDK.startPay(Activity activity, String orderInfo, String mode);
    
    //检查手机 pay 状态的接口
    UQPaySDK.getSEPayinfo(Context context, UPQuerySEPayInfoCallback callback);
    
    //检查是否安装银联 Apk 的接口
    UQPaySDK.checkInstalled (Context context);
  ```
  
#### 3、支付流程：
>   **(1)用户在客户端中点击购买商品，客户端发起订单生成请求到商户后台;**

>   **(2)商户后台收到订单生成请求后，按照《手机控件支付产品接口规范》组织并推送 订单信息至银联后台;**

>   **(3)银联后台接收订单信息并检查通过后，生成对应交易流水号(即 TN)，并回复交 易流水号至商户后台(应答要素:交易流水号等);** 

>   **(4)商户后台接收到交易流水号，将交易流水号返回给客户端;** 

>   **(5)客户端通过交易流水号(TN)调用支付控件;**

>   **(6)用户在支付控件中输入相关支付信息后，由支付控件向银联后台发起支付请求;** 

>   **(7)支付成功后，银联后台将支付结果通知给商户后台;** 

>   **(8)银联将支付结果通知支付控件;** 

>   **(9)支付控件显示支付结果并将支付结果返回给客户端;**
   
#### 4、测试账号：


> 测试账号一：
``` 
    招商银行借记卡:6226090000000048 
    手机号:18100000000
    密码:111101 
    短信验证码:123456(先点获取验证码之后再输入)
     证件类型:01 身份证
    证件号:510265790128303 
    姓名:张三
```

> 测试账号二：
``` 
    华夏银行借记卡: 6226388000000095
    手机号: 18100000000 
    cvn2:248
    有效期:1219 
    短信验证码:123456(先点获取验证码之后再输入) 
    证件类型:01 身份证
    证件号:510265790128303 
    姓名:张三
```
    
    
#### 放在最后
> **Android 平台 SDK 主要适用于 Android 2.3 及以上版本的终端设备**

