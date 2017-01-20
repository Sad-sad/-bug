:事件安卓兼容问题
安卓下swipe*的方法很难触发
这是安卓的一个老问题了.谷歌一下 类似zepto android swipe的关键字,就能发现不少.很多项目中的issue都能找到这个问题,连安卓自身项目里都有相关issue(链接要翻墙)
``` javascript
//解决方法就是在touchstart或touchmove事件中,主动调用e.preventDefault()
//1.在监听函数中调用e.preventDefault()
$('#ele_id').on('swipeLeft',function(e){
    e.preventDefault();
    //....
})

```
#### 2.移动端 HTML5 audio autoplay 失效问题
这个不是 BUG，由于自动播放网页中的音频或视频，会给用户带来一些困扰或者不必要的流量消耗，所以苹果系统和安卓系统通常都会禁止自动播放和使用 JS 的触发播放，必须由用户来触发才可以播放。
解决方法思路：先通过用户 touchstart 触碰，触发播放并暂停（音频开始加载，后面用 JS 再操作就没问题了）。
``` javascript
//解决代码：
document.addEventListener('touchstart', function () {
document.getElementsByTagName('audio')[0].play();
document.getElementsByTagName('audio')[0].pause();
});
```
#### 3.overflow 
在用 overflow-y: auto 来实现滚动的时候，ios 下会出现滚动卡顿的情况，android 一切正常。
 解决办法： -webkit-overflow-scrolling: touch
ios 下使用 overflow: hidden 会失效，
解决办法：添加 position: relative
#### 4.伪类 :active 生效
要CSS伪类 :active 生效，只需要给 document 绑定 touchstart 或 touchend 事件
```  
<style>
a {
  color: #000;
}
a:active {
  color: #fff;
}
</style>
<a herf=foo >bar</a>
<script>
  document.addEventListener('touchstart',function(){},false);
</script>
```
#### 5.消除 transition 闪屏
-webkit-transform-style: preserve-3d;
/*设置内嵌的元素在 3D 空间如何呈现：保留 3D*/
-webkit-backface-visibility: hidden;
/*（设置进行转换的元素的背面在面对用户时是否可见：隐藏）*/
#### 6.关于 iOS 与 OS X 端字体的优化(横竖屏会出现字体加粗不一等)
iOS 浏览器横屏时会重置字体大小，设置 text-size-adjust 为 none 可以解决 iOS 上的问题，但桌面版 Safari 的字体缩放功能会失效，因此最佳方案是将 text-size-adjust 为 100% 。
-webkit-text-size-adjust: 100%;
-ms-text-size-adjust: 100%;
text-size-adjust: 100%;
#### 7.不让 Android 手机识别邮箱
```
<meta content="email=no" name="format-detection" />
```
#### 8.禁止 iOS 弹出各种操作窗口
```
-webkit-touch-callout:none
```
#### 9.禁止用户选中文字
```
-webkit-user-select:none
```
#### 10.获取滚动条
```javascript
window.scrollY
window.scrollX
//比如要绑定一个 touchmove 的事件，正常的情况下类似这样(来自呼吸二氧化碳)
$('div').on('touchmove', function(){
.….code
});
//而如果中间的 code 需要处理的东西多的话，FPS 就会下降影响程序顺滑度，而如果改成这样
$('div').on('touchmove', function(){
setTimeout(function(){
//.….code
},0);
});
//把代码放在 setTimeout 中，会发现程序变快.
```
 



