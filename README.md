# rem 布局的 3 中方式

## 设计稿 750，640  1rem=100px 基准值一般都是 100px

## 当前屏幕的宽度(vm)/设计稿的宽度 = 要求的动态屏幕的 font-size/100

### 方法一：动态设置js

    
     // 设计稿750/640px,基准值为100px 利用测量的px大小除以100px 即可得到所需rem值
    (function () {
      remLayout();
      function remLayout() {
          // 获取屏幕宽度
          var w = document.documentElement.clientWidth;
          w = w > 640 ? 640 : w;
          w = w <= 320 ? 320 : w;
          // document.documentElement 获取到的html标签
          document.documentElement.style.fontSize = w / (750/100) + 'px'; // 750为设计稿的宽度，100为750设计稿的基准值
      }
      // resize 监听屏幕宽度变化，实时动态设置
      window.addEventListener('resize', function () {
          remLayout();
      }, false);
    })();



### 方法二：calc(（100vw / 设计稿的宽度）*100)

    html {
    
    //设置根字体大小单位为 vw，页面元素的尺寸单位都设为 rem，搭配 vw 和 rem，可实现布局根据视口变化而变化
    
    font-size: calc(（100vw / 设计稿的宽度）*100);
    
    // 同时，通过 Media Queries 限制根元素字体最大最小值
    
    @media screen and (min-width: 640px) {
    
    font-size: calc(（100vw / 640）*100);
    
    }
    
    @media screen and (max-width: 320px) {
    
    font-size: calc(（100vw / 320）*100);
    
    }
    
    }
    
 
### 方法三：媒体查询

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
