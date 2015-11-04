some note about requests
===

cookies:
---
urlparse.urlparse(url,scheme,allow_fragments)
urlparse 返回一个ParseResult的类,里面有url,scheme等可以获取url的各个部分的内容。
Morsel类 ： 用于表示Cookie中每一项数据的属性而抽象的类。这些属性包括：expires, path, comment, domain, max-age, secure, version等等.RCF2109
cookiejar.update(cookies)...


session:
---
request有两种状态，第一种是普通队形没法发送，需要先prepare_request，转化为可发送的字串。


