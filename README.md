# 技能分析平台

?> 彩豚智能技能分析平台是面向智能音箱技能开发者的技能统计服务平台。此平台集成了多种功能，包括技能分析、意图分析、用户分析以及语料分析等功能。在这个平台上你不仅仅可以看报表，还可以看见实时的技能调用数据。你可以访问 [https://data.caitun.com](https://data.caitun.com "彩豚智能技能分析平台") 来开始使用技能分析平台。

## 支持平台

?> 我们现在支持10个平台的技能统计，分别是小米水滴平台、京东Alpha开发平台、天猫精灵开放平台、百度Dueros开放平台、Google Actions 开放平台、Amazon Alexa 开放平台、苹果Homepod 开放平台、猎户OS开放平台、腾讯开放平台、思必驰开放平台。

**更多平台将会陆续增加**

## 请求地址
> https://data.caitun.com/api/bot/reports

请求地址必须使用https的方式

## Method
> POST

需使用HTTP 的 POST 方法提交请求

## Headers

> Content-Type: application/json

> Authorization: Bearer `<Your Access Token>`

其中 `Content-Type` 支持两种形式，分别是 `application/json` 和 `application/x-www-form-urlencoded`, `Authorization` 里面的`<Your Access Token>`需要用`API Token` 替换，`API Token` 可以在技能统计平台创建。`API Token` 创建之后，用户需要自己单独保存起来，彩豚技能分析平台并不会保留一份。

## 参数

参数的JSON格式举例：
```json
{
    "skill": "nWA5W",
    "intent": "Launch",
    "platform": "xiaomi",
    "user_id": "dev022",
    "slots": {
        "Number": "100",
        "Name": "张三"
    }
}
```

|    参数名    |   类型  |   必须  |  示例  |   说明   |
| ----------- | ------  |: ------------:|  ----  | ------- |
|    skill    |  string |    &nbsp;&nbsp;&nbsp;是&nbsp;&nbsp;&nbsp;        | nWA5W  | 技能编号，可以前往技能统计平台查看  |
|    intent   |  string |    &nbsp;&nbsp;&nbsp;是&nbsp;&nbsp;&nbsp;        | Launch | 意图名称或者编号，可以前往技能统计平台查看 |
|  platform   |  string |  &nbsp;&nbsp;&nbsp;是&nbsp;&nbsp;&nbsp;      | xiaomi | 所属技能平台名称，可以从下面文档中查找到各个平台对应的值 |
|   user_id   |  string |    &nbsp;&nbsp;&nbsp;否&nbsp;&nbsp;&nbsp;        | dev001 | 用户的ID，可以是技能平台提供的也可以说自己的创建的唯一ID |
|   slots   |  JSONObject    |    &nbsp;&nbsp;&nbsp;否&nbsp;&nbsp;&nbsp;   | {} | 对象结构中的Key 为槽位名称，值为用户通过智能音箱输入的文字 |


## 技能平台名列表

|    平台名称      |     参数值    |
|----------------|---------------|
|   小米水滴平台   |     xiaomi    |
|   京东Alpha开发平台   |     alpha    |
|   天猫精灵开放平台   |     tmall    |
|   百度Dueros开放平台   |     dueros    |
|   Google Actions 开放平台   |     google    |
|   Amazon Alexa 开放平台   |     amazon    |
|   苹果Homepod 开放平台   |     apple    |
|   猎户OS开放平台   |     orion    |
|   思必驰开放平台   |     dui    |
|   腾讯开放平台   |     tencent    |

**发送技能统计请求的时候，请求参数platform 需要用上面的参数值进行代替**

# 示例程序

## Javascript Demo

```javascript
var request = require("request");

var options = {
    method: 'POST',
    url: 'https://data.caitun.com/api/bot/reports',
    headers: {
        Authorization: 'Bearer <Your Access Token>',
        'Content-Type': 'application/json'
    },
    body: {
        skill: 'nWA5W',
        intent: 'Launch',
        platform: 'xiaomi',
        user_id: 'dev022',
        slots: {
            Number: '100',
            Name: '张三'
        }
    },
    json: true
};

request(options, function(error, response, body) {
    if (error) throw new Error(error);

    console.log(body);
});

```

## C# Demo
```csharp
var client = new RestClient("https://data.caitun.com/api/bot/reports");
var request = new RestRequest(Method.POST);
request.AddHeader("Authorization", "Bearer <Your Access Token>");
request.AddHeader("Content-Type", "application/json");
request.AddParameter("", "{\"skill\": \"nWA5W\", \"intent\": \"Launch\", \"platform\": \"xiaomi\", \"user_id\": \"dev022\", \"slots\": {\"Number\": \"100\", \"Name\": \"张三\"}}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

## PHP Demo
```php
<?php

$request = new HttpRequest();
$request->setUrl('https://data.caitun.com/api/bot/reports');
$request->setMethod(HTTP_METH_POST);

$request->setHeaders(array(
  'Authorization' => 'Bearer <Your Access Token>',
  'Content-Type' => 'application/json'
));

$request->setBody('{"skill": "nWA5W", "intent": "Launch", "platform": "xiaomi", "user_id": "dev022", "slots": {"Number": "100", "Name": "张三"}}');

try {
  $response = $request->send();

  echo $response->getBody();
} catch (HttpException $ex) {
  echo $ex;
}
```

## Java Demo

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\"skill\": \"nWA5W\", \"intent\": \"Launch\", \"platform\": \"xiaomi\", \"user_id\": \"dev022\", \"slots\": {\"Number\": \"100\", \"Name\": \"张三\"}}");
Request request = new Request.Builder()
  .url("https://data.caitun.com/api/bot/reports")
  .post(body)
  .addHeader("Content-Type", "application/json")
  .addHeader("Authorization", "Bearer <Your Access Token>")
  .build();

Response response = client.newCall(request).execute();
```

## Python Demo

```python
import requests

url = "https://data.caitun.com/api/bot/reports"

payload = "{\"skill\": \"nWA5W\", \"intent\": \"Launch\", \"platform\": \"xiaomi\", \"user_id\": \"dev022\", \"slots\": {\"Number\": \"100\", \"Name\": \"张三\"}}"
headers = {
    'Content-Type': "application/json",
    'Authorization': "Bearer <Your Access Token>"
}

response = requests.request("POST", url, data=payload, headers=headers)

print(response.text)
```

## Golang Demo
```go
package main

import (
    "fmt"
    "strings"
    "net/http"
    "io/ioutil"
)

func main() {

    url := "https://data.caitun.com/api/bot/reports"

    payload := strings.NewReader("{\"skill\": \"nWA5W\", \"intent\": \"Launch\", \"platform\": \"xiaomi\", \"user_id\": \"dev022\", \"slots\": {\"Number\": \"100\", \"Name\": \"张三\"}}")

    req, _ := http.NewRequest("POST", url, payload)

    req.Header.Add("Content-Type", "application/json")
    req.Header.Add("Authorization", "Bearer <Your Access Token>")

    res, _ := http.DefaultClient.Do(req)

    defer res.Body.Close()
    body, _ := ioutil.ReadAll(res.Body)

    fmt.Println(res)
    fmt.Println(string(body))

}
```

## Ruby Demo
```ruby
require 'uri'
require 'net/http'

url = URI("https://data.caitun.com/api/bot/reports")

http = Net::HTTP.new(url.host, url.port)

request = Net::HTTP::Post.new(url)
request["Content-Type"] = 'application/json'
request["Authorization"] = 'Bearer <Your Access Token>'
request.body = "{\"skill\": \"nWA5W\", \"intent\": \"Launch\", \"platform\": \"xiaomi\", \"user_id\": \"dev022\", \"slots\": {\"Number\": \"100\", \"Name\": \"张三\"}}"

response = http.request(request)
puts response.read_body
```

## Swift Demo
```swift
import Foundation

let headers = [
  "Content-Type": "application/json",
  "Authorization": "Bearer <Your Access Token>"
]
let parameters = [
  "skill": "nWA5W",
  "intent": "Launch",
  "platform": "xiaomi",
  "user_id": "dev022",
  "slots": [
    "Number": "100",
    "Name": "张三"
  ]
] as [String : Any]

let postData = JSONSerialization.data(withJSONObject: parameters, options: [])

let request = NSMutableURLRequest(url: NSURL(string: "https://data.caitun.com/api/bot/reports")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                    timeoutInterval: 10.0)
request.httpMethod = "POST"
request.allHTTPHeaderFields = headers
request.httpBody = postData as Data

let session = URLSession.shared
let dataTask = session.dataTask(with: request as URLRequest, completionHandler: { (data, response, error) -> Void in
  if (error != nil) {
    print(error)
  } else {
    let httpResponse = response as? HTTPURLResponse
    print(httpResponse)
  }
})

dataTask.resume()
```
