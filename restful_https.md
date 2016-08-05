# 通过 HTTPS 使用云巴 RESTful API

## 为什么使用 HTTPS
1. 防止内容被篡改、窃取；
2. 防止 AppKey、 SecretKey 泄露；
3. HTTPS 是发展趋势，[美国已要求所有政府网站在2016年底前完成全站https部署](https://www.whitehouse.gov/blog/2015/06/08/https-everywhere-government)。

## 如何使用
仅需要将 RESTful API 的 URL 由 http://rest.yunba.io:8080 更换为 https://rest.yunba.io 即可。

例如进行一次 Publish 请求可以通过下面的 curl 指令完成：
```bash
$ curl -l -H "Content-type: application/json" -X POST -d '{"method":"publish", "appkey":"XXXXXXXXXXXXXXXXXXXXXXX", "seckey":"sec-XXXXXXXXXXXXXXXXXXXXXXXXXXXXX", "topic":"news", "msg":"good news"}' https://rest.yunba.io
```

更多示例可参考 [RESTful API 的文档](https://github.com/yunba/docs/blob/master/restful_Quick_Start.md)，仅需要将文档中的 http://rest.yunba.io:8080 替换为  https://rest.yunba.io 即可。
