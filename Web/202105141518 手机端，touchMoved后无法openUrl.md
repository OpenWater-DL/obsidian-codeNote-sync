原因 手机的浏览器有安全机制，会防止弹窗。

	safari 回调中window.open无法执行
safari无法在callback中执行window.open,其安全机制将其阻挡了。

解决办法： 不弹窗，改成直接当前页面跳转。

