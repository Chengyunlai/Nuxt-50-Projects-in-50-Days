# 伸缩盒子
效果说明：类似抽屉，控制多个元素中的某一个元素具有伸缩性。示意如下：

![example.png](img/example.png)

**实现原理：**

主要使用了`flex`属性，初始时每个元素的 `flex`属性值都为`0.5`（一个固定值），除了首个元素。

绑定点击事件，当元素被点击时，将其`flex`属性值设置为`5`。

**原生Js详解：**

第一步：
```js
// 操作DOM，使用 querySelectorAll 查询所有 class 为 panel 的 NodeList
const panels = document.querySelectorAll('.panel');
```
第二步：
```js
// 遍历 NodeList 获取 Node 对象
panels.forEach(panel => {
    // 给每一个 Node 对象添加点击事件
    panel.addEventListener('click',()=>{
        // 先移除所有节点的 active 类
        removeActiveClasses();
        // 再给当前点击的 Node 添加 active 类
        panel.classList.add('active');
    })
})
```

```js
function removeActiveClasses(){
    panels.forEach(panel => {
        panel.classList.remove('active');
    })
}
```

核心动画 Css - transition
> 过渡可以为一个元素在不同状态之间切换的时候定义不同的过渡效果。比如在不同的伪元素之间切换，像是 :hover，:active 或者通过 JavaScript 实现的状态变化。
```
transition: all 0.5s ease;
```
对所有状态切换变换预留 `0.5`秒的过度时间，使用动画效果 `ease`