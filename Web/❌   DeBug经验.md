### 检查属性拼写是否正确
没有效果？感觉逻辑也没错，用别的变量去指代就没问题，用类名就不行？
![[拼写问题 20210108223138.png]]

-安装了插件 code spell checker
[中文简介](http://www.duocaichajian.com/plugin/47.html)
**忽略**
你可以在文档里指定某些忽略检查的words。
```
// cSpell:ignore zaallano, wooorrdd
// cSpell:ignore zzooommmmmmmm
const wackyWord = \['zaallano', 'wooorrdd', 'zzooommmmmmmm'\];
```
你可以创建某些自定义的短语，它也可以作为替代的建议选项。
```
// cSpell:words woorxs sweeetbeat
const companyName = 'woorxs sweeetbeat'
```