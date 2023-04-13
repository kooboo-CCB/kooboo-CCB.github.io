# JavaScript 工作集

## 纯 js 实现图片懒加载

**目的：** 当图片进入可视区域内去加载图片，且处理加载失败，封装成指令

> 实现思路是当 img 的 src 没有值的时候,浏览器不会请求对应图片,只要当 img 进入可视范围时,动态的给 img 标签的 url 赋值就可以实现图片懒加载.

```html
<body>
  <div style="height: 1000px; background-color: aliceblue;">content</div>
  <div style="height: 1000px; background-color: aliceblue;">content</div>
  <!-- 测试:让img元素超出屏幕显示范围,可以增加height高度 -->
  <img src="" alt="" />
  <!-- 测试容器 -->
</body>
```

主要实现的 API：[IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/IntersectionObserver)

```js
//img元素
let img = document.querySelector("img");
// 图片连接
let imgSrc = "https:xxxxxxx";
// 默认图片 , 在图片加载失败的时候加载默认图片
let defaultImg = "https:xxxxxxxxxx";

LazyLoading(img, imgSrc, defaultImg);

function LazyLoading(el, src, defaultSrc) {
  if (!el && !src) {
    return "require params el and src";
  }
  const observer = new IntersectionObserver(
    ([{ isIntersecting }]) => {
      if (isIntersecting) {
        observer.unobserve(el);
        el.onerror = () => {
          if (defaultSrc) {
            el.src = defaultSrc;
          }
        };
        el.src = src;
      }
    },
    {
      threshold: 0.01,
    }
  );
  observer.observe(el);
}
```

#### 服务器渲染时如何处理？

?> 当图片的数据是在服务器渲染的时候, 可以将原本设置 img 标签 的 `src` 的操作改为设置成 `_src` 或其它名称，在监听到图片进入可视范围的时候，动态的取元素对应的 `attribute` 的值，将其赋值给图片的 `src` 即可

?> 此工具还可以衍生多种功能函数，例如完成需求： `当元素进入可视范围内时，为元素的XXX进行赋值`

## 元素进入可视范围时，添加指定 class

```html
<div k-for="item in 20">
  <div
    style="height: 100px;width: 100px; background-color: aliceblue;"
    class="item"
  >
    content
  </div>
</div>
```

```js
let divs = document.querySelectorAll(".item");
divs.forEach((div, index) => {
  // 当元素进入可是范围的时候,根据索引为元素添加 item1 / item2 ....的类名
  addVisibleClassOnScroll(div, `item${index}`);
});

function addVisibleClassOnScroll(el, className) {
  const observer = new IntersectionObserver(
    ([{ isIntersecting }]) => {
      if (isIntersecting) {
        if (Array.isArray(className)) {
          el.classList.add(...className);
        } else {
          el.classList.add(className);
        }
        observer.unobserve(el);
      }
    },
    {
      threshold: 0.01,
    }
  );
  observer.observe(el);
}
```

> 这个函数可以搭配 `tailiwnd` 或者其它一些 `动画CSS库` (大多依靠 class 实现) 来实现 `dom` 进入可视范围之后 执行动画的需求

## Vue-Router kooboo-lite 版

> **目的:** 改变页面的路径但不刷新页面且想通过路径的参数请求一些指定的数据
