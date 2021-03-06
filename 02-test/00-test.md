### 分析比较 `opacity: 0`、`visibility: hidden`、`display: none` 优劣和适用场景
共同点：都是让元素不可见
`opacity: 0` :
- 在渲染树占据空间，内容不可见，可以点击
- 修改元素会造成重绘，性能消耗较少
- 场景：可以跟`transition`搭配
- 继承：会被子元素继承，但子元素并不能通过 `opacity: 1` 来取消隐藏
`visibility: hidden`：
- 在渲染树占据空间，内容不可见，不可点击
- 修改元素只会造成本元素的重绘，性能消耗较少，读屏器会读取`visibility: hidden`元素的内容
- 场景：显示不会导致页面结构发生变动，不会撑开
- 继承：会被子元素继承，子元素可以通过设置 `visibility: visible;` 来取消隐藏
`display: none`：
- 不在渲染树中占据空间，内容不可见，不可点击
- 修改元素会造成文档回流，读屏器不会读取`display: none`元素的内容，性能消耗较大
- 场景：显示出原来这里不存在的结构，用于改动较小的场景
- 继承：不会被子元素继承，毕竟子类也不会被渲染

### 已知如下代码，如何修改才能让图片宽度为 `300px` ？注意下面代码不可修改。
```html
<img src="1.jpg" style="width:480px!important;">
```
设置css属性：
- `max-width`
```css
img {
  max-width: 300px;
}
```
- `transform`
```css
img {
  transform: scale(0.625);
}
```
- `box-sizing` + `padding`
```css
img {
  box-sizing: border-box;
  padding: 90px;
}
```
- `zoom`
```css
img {
  zoom: 0.625;
}
```