# HTML
### 标题菜单
h4 包住 a
h4给分类，a给链接和显示文字。

### 作品封面结构
a包住img
```html
 <div class="item">
          <a href="hydrophilic.html">
            <img
              src="https://cdn.glitch.com/00e39e19-4bab-4dfc-81dc-21e6d212a6ab%2FHYDROPHILIC_.png?v=1582753871763"
            />
          </a>
</div>

```

# CSS
### 缓动变化过渡
```css
body {
    -webkit-transition: all 3s ease;
    transition: all 3s ease;
}
```

transition的用法：
```
【语法】
transition: 对象 时间 缓动曲线方式(ease)

如果不写对象，将对所有要发生变化的css属性应用这个过渡规则。

【实例】
transition: background 3s ease


```

transition 和 -webkit-transition 的区别？
功能上是一样的，只是为了兼容性。
-moz-,-webkit-,-o-这三个是厂商前缀，不同浏览的厂商,因为不同浏览器有不同的标准，所以为了兼容性，需要把常用的浏览器对应的厂商前缀加上。
-moz- 是火狐浏览器厂商前缀
-webkit- 是谷歌浏览器厂商前缀
-o- 是opera浏览器厂商前缀


[-webkit-transition的用法](https://www.cnblogs.com/fifteen718/p/9533923.html)：
-webkit-transition：CSS属性(none|all|属性)  持续时间  时间函数  延迟时间
