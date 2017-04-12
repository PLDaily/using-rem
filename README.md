## rem布局详解

### dpi
在页面中设置一个div宽度为300px，以iphone6为例，手机宽度的物理像素(即手机实物大小)375px，但其dpi为2，所以它的实际页面宽度为750px，div在实际页面中占的宽度为600px。所以iPhone6中显示更为清晰。
如果是设置图片宽度，设置宽度为300px的图片在实际页面中占宽度为600px，所以需要用二倍图。   

### 设置根元素font-size
```javascript
(function (doc, win) {
    var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function () {
            var clientWidth = docEl.clientWidth;
            if (!clientWidth) return;
            if(clientWidth>=750){
                docEl.style.fontSize = '100px';
            }else{
                docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
            }
        };

    if (!doc.addEventListener) return;
    win.addEventListener(resizeEvt, recalc, false);
    doc.addEventListener('DOMContentLoaded', recalc, false);
})(document, window);

```
设计稿以750px宽度作图，当屏幕宽度大于750px时取font-size为100px，当其小于750px时，则根据该屏幕与750px的比值进行计算。
根元素默认取fon-size为100px是为了方便计算。

### 使用rem
由于设计稿的宽度为750px，该标注的px值便是我们css中需要书写的px值，只需将其除以100便可以得到rem值。