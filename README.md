# rem 布局的 3 中方式

## 设计稿 750，640 1rem=100px 基准值一般都是 100px

## 当前屏幕的宽度(vm)/设计稿的宽度 = 要求的动态屏幕的 font-size/100

### 方法一：

function setRem(design) {
//1 获取当前屏幕的宽度
var width = window.innerWidth;

    if (width > 640) {
      width = 640;
    }
    if (width < 320) {
      width = 320;
    }

    //动态设置rem的值
    document.querySelector("html").style.fontSize =
      (width / design) * 100 + "px";

}

setRem(640);

//检测屏幕宽度变化，实时动态设置
window.onresize = function() {
setRem(640);
};

### 方法二：

html {
//设置根字体大小单位为 vw，页面元素的尺寸单位都设为 rem，搭配 vw 和 rem，可实现布局根据视口变化而变化
font-size: calc(（100vw / 设计稿的宽度）*100);
// 同时，通过 Media Queries 限制根元素字体最大最小值
@media screen and (min-width: 640px) {
font-size: calc(（100vw / 640）*100);
}
@media screen and (max-width: 320px) {
font-size: calc(（100vw / 320）\*100);
}
}

### 方法三：

@media screen and (min-width: 640px) {
html {
font-size: 100px;
}
}
/_ 诺基亚 _/
@media screen and (max-width: 639px) and (min-width: 480px) {
html {
font-size: 75px;
}
}

/_ ip6/7/8p _/
@media screen and (max-width: 479px) and (min-width: 414px) {
html {
font-size: 64.6875px
}
}

/_ ip6/7/8 _/
@media screen and (max-width: 413px) and (min-width: 375px) {
html {
font-size: 58.59375px
}
}

/_ 三星 _/
@media screen and (max-width: 374px) and (min-width: 360px) {
html {
font-size: 56.25px
}
}

/_ ip3/4/5 _/

@media screen and (max-width: 359px) {
html {
font-size: 50px
}
}
