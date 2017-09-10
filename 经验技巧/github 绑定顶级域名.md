# github 绑定顶级域名

说明：该页面翻译至[官方文档：Setting up an apex domain](https://help.github.com/articles/setting-up-an-apex-domain/)
绝对可靠！

---

绑定一个顶级域名，比如`example.com`，你必须在你的dns解析服务商中配置一个`ALIAS`,`ANAME`,`A`record 。

> Tip: 如果你在配置上述dns解析服务时候遇到困难，请与你的dns服务商取得联系。他们会帮助你确认你的域名是否已经正确连接（他们才不会管咧）



> Warning:



## 配置一个`ALIAS`或者`ANAME`记录

1. 确保你已经在你的github page 中已经添加了一个自定义域名。
2. 联系你的DNS解析服务商去来知道如何设置`ALTAS`或者`ANAME`记录（谁会告诉你！）
3. 新建一个`ALIAS` 或者`ANMAE` 记录把你的**顶级域名**指向Github Pages 服务。你的DNS改变最多需要一天来在整个网络中更新
4. ​

