---
theme: seriph
class: text-center
highlighter: shiki
lineNumbers: false
background: https://source.unsplash.com/collection/94734566/1920x1080
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: false
transition: slide-left
title: Welcome to Slidev
---

# 摩登 CSS

Modern，Fancy，Newest

---

# css 的发展

--引入模块化之前

CSS 只有级别（level）的概念没有版本的概念，比如 CSS3 就是 CSS level 3，CSS2 就是 CSS level 2，每个级别都以上一个级别为基础。

CSS1、CSS2（以及 CSS2.1）在当时都是一个大而全的规范，出现了很多问题

后来，W3C 进一步完善了规范制定流程，要求每个规范都要经过以下五个阶段：

- 工作草案（WD，Working Draft）
- 最终工作草案（LC/LCWD，Last Call Working Draft）
- 候选推荐（CR，Candidate Recommendation）
- 提议推荐（PR，Proposed Recommendation）
- 推荐标准（REC，Recommendation）

---

随着 CSS 特性越来越多，越来越复杂，CSS 规范的篇幅也越来越长，这就给勘误和进一步升级带来了极大不便。于是，CSS 工作组决定从 CSS2.1 之后开始采取模块化的路线，从此以后，CSS 就进入了 Level 3。

![Remote Image](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/f5f4b50fc13b448e9025489deed4e1e8~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

---

## 1.@Property

它允许开发者显式地定义他们的 CSS 自定义属性，允许进行属性类型检查、设定默认值以及定义该自定义属性是否可以被继承。

```css{all|1-3|4-8|all}
:root {
  --whiteColor: #fff;
}
@property --whiteColor {
  syntax: "<color>";
  inherits: false;
  initial-value: #fff;
}
p {
  color: (--whiteColor);
}
```

- syntax： 类型（length，number，color，url 等等）
- inherits: 是否可继承
- initial-value：初始值

---

## Cases

- 渐变色过渡 https://codepen.io/Chokcoco/pen/eYgyWLB?editors=1100
- 饼图动画 https://codepen.io/Chokcoco/pen/QWdqMvo

---

## 2.@supports

检测浏览器是否支持该语法，如果不支持可以向下兼容

```css
@supports () {
  /* CSS rules here */
}
```

经典用法

```css{1-3|4-8}
.main{
  display:flex;
}
@supports (display: grid) {
  .main {
    display: grid;
  }
}
```

---

## 3.@container

容器查询，类似 media query，可以实时匹配指定容器元素的尺寸，基于不同尺寸范围，对内部设置特定样式

用法

定义容器，container-name + container-type

```css{1|2-3}
.card-container {
  container-name: name;
  container-type: inline-size;
  container: name/inline-size
}
```

查询

```css
@container name (max-width: 850px) {
  /* CSS rules here */
}
```

https://codepen.io/shadeed/pen/ExZEEjZ

---

## 4.scroll snap

CSS Scroll Snap 是 CSS 中一个独立的模块，可以让网页容器滚动停止的时候，自动平滑定位到指定元素的指定位置，包含 scroll-*以及 scroll-snap-*等诸多 CSS 属性。

|                                   |                   |
| --------------------------------- | ----------------- |
| 作用在滚动容器上                  | 作用在定位子项上  |
| scroll-snap-type/scroll-snap-stop | scroll-snap-align |

https://codepen.io/tutsplus/pen/qpJYaK

---

## 5.conic-gradient,radial-gradient

conic-gradient 角向渐变
https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/conic-gradient
radial-gradient 径向渐变
https://developer.mozilla.org/en-US/docs/Web/CSS/gradient/radial-gradient

---

## 6.aspect-ratio

直接设置元素宽高比

麻烦手法

```css{1-8|9-17}
:root {
    --wwidth: 100vw;
    --hheight: calc(var(--wwidth) / 2);
}
.box {
    width: var(--wwidth);
    height: var(--hheight);
}
.outer{
  width: 100%;
  padding-bottom: 50%;
  position: relative;
}
.inner{
  position:absolute;
  inset:0;
}
```

---

简单手法

```css
.box {
  aspect-ratio: 2/1;
}
```

---

## 7.filter,backdrop-filter

- filter：该属性将模糊或颜色偏移等图形效果应用于元素。
- backdrop-filter： 该属性可以让你为一个元素后面区域添加图形效果（如模糊或颜色偏移）。 它适用于元素背后的所有元素，为了看到效果，必须使元素或其背景至少部分透明。

https://codepen.io/Chokcoco/pen/WNjebrr

---

## 8.is,where selector

- :is() CSS 伪类函数将选择器列表作为参数，并选择该列表中任意一个选择器可以选择的元素。:is() 的优先级是由它的选择器列表中优先级最高的选择器决定的
- :where() 和 is 类似。区别:where() 的优先级总是为 0

CSS 选择器的一个非常大的特点就在于组合嵌套。:is 和 :where 也不例外，因此，它们也可以互相组合嵌套使用。

```css
/* 组合*/
:is(h1,h2) :where(.test-a, .test-b) {
  text-transform: uppercase;
}
/* 嵌套*/
.title:where(h1, h2, :is(.header, .footer)) {
  fo
```

---

## 9. has selector

has 的诞生，填补了在之前 CSS 选择器中，没有核心意义上真正的父选择器的空缺。

```html
<div>
  <p>div -- p</p>
</div>
<div>
  <p class="g-test-has">div -- p.has</p>
</div>
<div>
  <p>div -- p</p>
</div>
```

```css
div:has(.g-test-has) {
  border: 1px solid #000;
}
```

https://codepen.io/Chokcoco/pen/poaJjwm

---

## 10.accent-color

accent-color 属性可以在不改变浏览器默认表单组件基本样式的前提下重置表单组件的颜色

https://code.juejin.cn/pen/7085562391907270690

---

# Thanks

<style>
  h1{
    display:flex;
    height:100%;
    justify-content:center;
    align-items:center;
  }
</style>

---
