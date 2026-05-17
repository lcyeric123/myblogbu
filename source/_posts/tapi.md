---
title: 劉叡翻译 API 开发文档
date: 2026-05-17 20:30:00
tags: [API,翻译接口]
categories: 开发文档
---

# 劉叡翻译 API 开发文档
版本：V1.0

## 基础信息
接口域名：https://translate.ericse.bond
请求方式：GET
传输协议：HTTPS

## 接口地址
```http
GET https://translate.ericse.bond/api/translate
```
 
请求参数
 
```json
  
{
  "text": "待翻译文本",
  "from": "源语言代码",
  "to": "目标语言代码"
}
```
 
语言代码对照表

```plaintext
  
zh      中文
en-us   美式英语
en-gb   英式英语
ja      日语
ko      韩语
fr      法语
de      德语
ru      俄语
es      西班牙语
pt      葡萄牙语
it      意大利语
ar      阿拉伯语
th      泰语
vi      越南语
id      印尼语
ms      马来语
hi      印地语
tr      土耳其语
pl      波兰语
nl      荷兰语
sv      瑞典语
fi      芬兰语
da      丹麦语
no      挪威语
el      希腊语
cs      捷克语
hu      匈牙利语
ro      罗马尼亚语
uk      乌克兰语
bg      保加利亚语
he      希伯来语
fa      波斯语
 
```
成功响应示例
 
```json
  
{
  "status": 200,
  "request_time": "2026/5/17 20:00:00",
  "original_text": "hello",
  "original_language": "美式英语",
  "target_language": "中文",
  "translation": "你好"
}
 
```
错误响应格式
 
空文本请求
 
```json
  
{"status":400,"request_time":"2026/5/17 20:00:00","msg":"翻译内容不能为空"}
 
```
服务异常
 
```json
  
{"status":500,"request_time":"2026/5/17 20:00:00","msg":"翻译服务异常"}
```
 
代码调用示例
 
Python
 
```python
  
import requests

url = "https://translate.ericse.bond/api/translate"
params = {
    "text": "hello world",
    "from": "en-us",
    "to": "zh"
}
result = requests.get(url, params=params)
print(result.json())
 
```
JavaScript 前端
 
```javascript
  
fetch("https://translate.ericse.bond/api/translate?text=hello&from=en-us&to=zh")
.then(res => res.json())
.then(data => {
    console.log(data.translation)
})
 
```
Node.js
 
```javascript
  
const axios = require("axios");
async function translate() {
    const res = await axios.get("https://translate.ericse.bond/api/translate", {
        params: {
            text: "hello",
            from: "en-us",
            to: "zh"
        }
    })
    console.log(res.data)
}
translate()
```
 
Java
 
```java
  
import java.net.HttpURLConnection;
import java.net.URL;
import java.io.BufferedReader;
import java.io.InputStreamReader;

public class TranslateApi {
    public static void main(String[] args) throws Exception {
        String apiUrl = "https://translate.ericse.bond/api/translate?text=hello&from=en-us&to=zh";
        URL url = new URL(apiUrl);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("GET");
        BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
        String line;
        while ((line = reader.readLine()) != null) {
            System.out.println(line);
        }
        reader.close();
    }
}
```
 
PHP
 
```php
  
<?php
$text = "hello";
$from = "en-us";
$to = "zh";
$api = "https://translate.ericse.bond/api/translate?text={$text}&from={$from}&to={$to}";
echo file_get_contents($api);
?>
 
 ```
Go
 
```go
  
package main

import (
	"fmt"
	"io/ioutil"
	"net/http"
)

func main() {
	resp, err := http.Get("https://translate.ericse.bond/api/translate?text=hello&from=en-us&to=zh")
	if err != nil {
		return
	}
	defer resp.Body.Close()
	body, _ := ioutil.ReadAll(resp.Body)
	fmt.Println(string(body))
}
```
 
C#
 
```csharp
  
using System;
using System.Net;

class ApiTest
{
    static void Main()
    {
        WebClient webClient = new WebClient();
        string data = webClient.DownloadString("https://translate.ericse.bond/api/translate?text=hello&from=en-us&to=zh");
        Console.WriteLine(data);
    }
}
 
```
附加说明
 
1. 接口全局开放跨域，支持任意客户端直接调用
2. 内置网页访问地址：https://translate.ericse.bond
3. 自动适配美式英语与英式英语单词拼写转换
4. 支持所有语种双向互相翻译
