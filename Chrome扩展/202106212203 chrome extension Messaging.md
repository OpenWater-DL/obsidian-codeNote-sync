1. background  to  content.







2. popup to content
要点1：发送信息的方法。（在sketch.js里）
chrome.tabs.sendMessage(tabs[0].id, msg);
这个函数可以发送message到content.js里。发送的目的地是第一个参数代表的tab的content，内容是第二个参数msg。

要点2：获取tab的方法

chrome.tabs.query(params,gotTabs);
这是查询的函数。可以根据params参数所描述的选择条件（写成jason对象），去查询出需要的tab，然后得到的结果作为参数传入gotTabs这个function中。


```js
      let params = {
        active: true,
        currentWindow: true
      }

        chrome.tabs.query(params,gotTabs);
		
```

下例就用tabs代表查询出来的结果，它被作为参数传入了gotTabs这个function里。所以在gotTabs里的chrome.tabs.sendMessage()才能认可tabs[0]是一个tab对象，以此获得的id才是有效的。
```js

let params = {

active: true,

currentWindow: true

}

  

chrome.tabs.query(params,gotTabs);    

function gotTabs(tabs) {
  console.log("got tabs");
  console.log(tabs);

//send a message to the content script

let message = userinput.value();

let msg = {
txt: userinput.value()  
}
chrome.tabs.sendMessage(tabs[0].id, msg);
  
}

```

要点3：接受信息的方法
（在conent.js里）
chrome.runtime.onMessage.addListener(gotMessage);
这个函数也是个异步函数。当监听到有东西时，就会得到3个参数，这3个参数会传入括号里的function里执行。

```
chrome.runtime.onMessage.addListener(gotMessage);

function gotMessage(message, sender, sendResponse) {
    console.log(message);
	
    let paragraphs = document.getElementsByTagName('p')
	
    for (elt of paragraphs) {
        elt.innerHTML = message.txt;
    }


}

```


