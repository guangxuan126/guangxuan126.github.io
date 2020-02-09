---
title: 微信小程序开发之ACCESS_TOKEN的调用
date: 2019-08-30 19:02:10
tags:
  - public
  - tutorials
---

在微信开发和微信小程序开发中，很多时候如果我们并不能直接调用一些后台 API，如果想要使用这些 API 就必须在请求时附带一个`access_token`.

## access_token

在小程序中，`access_token` 是小程序全局唯一后台接口调用凭据，调用绝大多数后台接口的时候都需要使用。

在公众号开发中，公众号调用各个接口的时候必须使用`access_token`。

所以开发者需要进行妥善保存。`access_token`的有效期目前是2个小时，需要定时刷新，重复获取将导致上次获取的`access_token`失效。为了保证`access_token`的安全性，后端 API 将不能通过小程序内的 [wx.request](https://developers.weixin.qq.com/miniprogram/dev/api/network/request/wx.request.html) 调用，即`api.weixin.qq.com`不能配置为服务器域名。开发者应在后端服务其使用`getAccessToken`获取`access_token` ，并调用相关 API。



## getAccessToken

详细请参考 [微信官方文档-auth.getAccessToken](https://developers.weixin.qq.com/miniprogram/dev/api-backend/open-api/access-token/auth.getAccessToken.html)



#### 请求地址

```
GET https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=APPID&secret=APPSECRET
```



#### 请求参数

|    属性    |  类型  | 默认值 | 必填 | 说明                                                         |
| :--------: | :----: | :----: | :--: | ------------------------------------------------------------ |
| grant_type | string |        |  是  | 填写 client_credential                                       |
|   appid    | string |        |  是  | 小程序唯一凭证，即 AppID，可在「[微信公众平台](https://mp.weixin.qq.com/) - 设置 - 开发设置」页中获得。 |
|   secret   | string |        |  是  | 小程序唯一凭证密钥，即 AppSecret，获取方式同 appid           |



#### 返回值

Object 返回的 JSON 数据包

| 属性         | 类型   | 说明                                           |
| ------------ | ------ | ---------------------------------------------- |
| access_token | string | 获取到的凭证                                   |
| expires_in   | number | 凭证有效时间，单位：秒。目前是7200秒之内的值。 |
| errcode      | number | 错误码                                         |
| errmsg       | string | 错误信息                                       |



#### 返回数据示例

- 正常返回

  ```json
  {"access_token": "ACCESS_TOKEN","expires_in":7200}
  ```

- 错误时返回

  ```json
  {"errcode":40013,"errmsg":"invalid appid"}
  ```




#### access_token 的存储与更新

- `access_token` 的存储至少要保留512个字符空间；
- `access_token` 的有效期目前为2小时，需定时刷新，重复获取将导致上次获取的 `access_token` 失效；
- 建议开发者使用中控服务器同意获取和刷新 `access_token`，其他业务逻辑服务器所使用的 `access_token` 均来自于该中控服务器，不应该各自去刷新，否则容易造成冲突，导致 `access_token` 覆盖而影响业务；

#### 在线调试

可以使用微信 [网页调试工具]([https://mp.weixin.qq.com/debug/cgi-bin/apiinfo?t=index&type=%E5%9F%BA%E7%A1%80%E6%94%AF%E6%8C%81&form=%E8%8E%B7%E5%8F%96access_token%E6%8E%A5%E5%8F%A3%20/token&token=&lang=zh_CN](https://mp.weixin.qq.com/debug/cgi-bin/apiinfo?t=index&type=基础支持&form=获取access_token接口 /token&token=&lang=zh_CN)) 调试接口



## 使用PHP来刷新和存储 access_token

首先我的思路是这样的：

![](https://i.loli.net/2019/08/31/A3ZD4S8flzortG2.png)

建立一个可以被请求到的 PHP 文件，当小程序需要用到 `access_token` 时，先进行这个获取请求，获取到 `access_token` 之后，再配合其他服务端API进行其他业务操作。



以下是部分代码：

```php
function getAccessToken(){
    $appid="APPID";
    $appsecret = "APPSECRET";
    //文件存储
    $data=json_decode(get_php_file("access_token.php"));
    if($data->expire_time<time()){
        $url="https://api.weixin.qq.com/cgi-bin/token?grant_type=client_credential&appid=".$appid."&secret=".$appsecret;
        $res=json_decode(httpGet($url));
        $access_token=$res->access_token;
        if($access_token){
            $data->expire_time=time()+7000;
            $data->access_token=$access_token;
            set_php_file("access_token.php",json_encode($data));
        }
    }else{
      $access_token=$data->access_token;
    }
    return $access_token;
  }
```



这样，通过存储 `access_token` 和判断时间的方式来实现对 `access_token` 的获取、存储、刷新和调用。



&&

end