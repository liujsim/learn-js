### learn-js

首先过一遍 pocket 收藏的 JS 标签内容

JS 的各种概念定义(以 MDN 为准), tips ,example 和 components

JS 的引用传递,值传递,执行环境,引用计数和 GC以及算法

JS 的那些坑

目的：熟悉 JS 常见的函数 API，完成任务时，能够快速的记起来，
站在开发者角度，想像一下完成任务需要什么 API

amd

#### 闭包
闭包是指函数有自由独立的变量

    var a = [];
    for (var i = 0; i < 10; i++) {
      a[i] = function () {
        console.log(i);
      };
    }
    a[6](); // 10




a[]() 函数中的 i 始终保持了对外部变量 i 的引用，此时循环已结束，i 的值被修改为 "10"

填坑：为了得到想要的结果，需要在每次循环中创建变量 i 的拷贝

    function iteratorFactory(i){
        a[i] = function(e){
            console.log(i)
        }
        return a[i];
    }

    var a = [];
    for (var i = 0; i < 10; i++) {
      a[i] = iteratorFactory(i)
    }
    a[1]()



#### 正则

    var pattern = /\[KWL\d{3}\]/g;
    var arrEmoji = msg.match(pattern)
    if (arrEmoji != null && arrEmoji.length > 0) {
        for (var i = 0; i < arrEmoji.length; i++) {
            msg = msg.replace(arrEmoji[i], "<img class='emojiImg' src='img/emoji/" + getJsonValue(emojiJson1, arrEmoji[i]) + "' >");
        };
    }

 注意 replace 的字符串替换和正则替换

### component

**设计原则参考 http://ant.design/docs/spec/introduce**

参照 vux 的组件图 ![vux](https://raw.githubusercontent.com/airyland/vux/master/assets/components.png)

使用 JS 开发 web 常用的组件，从实现最初的的完成功能 demo,最终目的 API 友好，可重用的组件

兼容性 IE 10 +，移动端友好

alert confirm toast popup  ToolTip Checkbox  分页  树 自动完成

1. tab 选项卡

2. Dialog 弹出层

3. 瀑布流 waterfall

4. 轮滑 swipe

5. 分页  -- [如何写一个简单的分页](http://web.jobbole.com/85405/) 

6. mvvm [利用 JavaScript 数据绑定实现一个简单的 MVVM 库](https://segmentfault.com/a/1190000004847657)

包括功能实现,和动画的过度效果

7. 懒加载  [图片延迟加载简单实现](http://yangxiaofu.com/2015/11/20/%E5%9B%BE%E7%89%87%E5%BB%B6%E8%BF%9F%E5%8A%A0%E8%BD%BD%E7%AE%80%E5%8D%95%E5%AE%9E%E7%8E%B0/)

8. 自动完成   [awesomplete](https://github.com/LeaVerou/awesomplete)

9. commonjs 和 amd 实现   https://github.com/xiaofuzi/commonJS   amd 规范: lodJS  和雨夜带刀的 seed.js

10. 省市级联 https://github.com/cnluzhang/chinaddress

11. 下拉刷新   
    http://apeatling.com/javascript-pull-to-refresh-web/
    * touchStart,touchMove touchEnd 记录下拉的距离,到达阈值后,向后台请求数据,然后 append
    * 注意下拉刷新的长度  touchStart 
    
12. 底部自动加载下一页  

```
    $(window).scroll(function() {
        if ($(document).scrollTop() + $(window).height() > $(document).height() - 100) {
            $.get(url, function(data) {
                $('#list').append(data);
            });
        }
    });
```


#### overlay

 2个 div,一个 blank ,一个 overlay
 
 blank 和 overlay 都全屏,bank 设置 background 和 opacity ,z-index ,作为底层,overlay 作为上层(z-index 控制)显示元素,


#### model 实现

功能:点击一个元素,弹出一个对话框,有关闭按钮,有一个遮罩

#### example

为验证功能的原始 demo

1. 使用 vue 做一个 base64 和图片相互转换的 demo
