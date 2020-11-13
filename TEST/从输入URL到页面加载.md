# 从输入URL到页面加载

https://dailc.github.io/2018/03/12/whenyouenteraurl.html

![img](https://cdn.nlark.com/yuque/0/2020/svg/1537754/1595340593070-85fb22de-c8a2-4283-bf0f-5007faa536b2.svg)

1. DNS查询

DNS查询就是查找网址对应IP地址的过程

DNS查询的过程：

浏览器缓存 --- 操作系统缓存 --- 本地host文件 --- 路由器缓存 --- ISP DNS缓存 --- 顶级DNS服务器/根DNS服务器

![image](https://cdn.nlark.com/yuque/0/2020/png/1537754/1595336208075-f8d09347-2f37-4538-8b19-46748ad40644.png?x-oss-process=image%2Fresize%2Cw_1500)





1. TCP连接

- TCP建立连接 三次握手

![image](https://cdn.nlark.com/yuque/0/2020/webp/1537754/1595336688351-8f5d2ffd-1fed-42d5-b6cf-e01a9cf7bc8c.webp)

- TPC连接释放 四次挥手

![image](https://cdn.nlark.com/yuque/0/2020/webp/1537754/1595336834630-d18dbca2-e192-442f-9957-2ac76ce8302d.webp)

1. HTTP请求
2. 页面渲染

- 解析HTML，构建DOM树
- 解析CSS，生成CSS规则树
- 合并DOM树和CSS规则，生成render树