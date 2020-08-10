# css 页面布局与网格 , 浮动

## 1.布局的介绍
- 固定布局
- 弹性布局
- 流动布局: 指页面的元素会按照比例缩放但是,元素之间的比率保持不变
  
## 2.创建灵活的页面布局demo
### 1.float布局
- 使用float
- 内部元素使用min-height属性,以免子元素超出父元素,父元素不能撑开
  ![](img/%E5%88%9B%E5%BB%BA%E5%88%97.png)
### 2.流式空距
- border-box 当设置外边距,所有列的总宽度大于100%就会发生错乱的现象
  ```css
  .col {
        float: left;
        box-sizing: border-box;
        min-height: 100px;
        outline: 1px solid #666;
        /* 布局会乱,因为加上了外边距,所有列的总宽度超过了100% */
        margin: 0 0.9% 1.375em;
      }
  ```
  ![](img/%E5%B8%83%E5%B1%80%E9%94%99%E4%B9%B1.png)
**解决办法:**
- 抵消最外侧的空距
  ```css
    .row {
        margin: 0 -0.9%;
      }
  ```
  ![](img/%E8%B4%9Fmargin.png)
  这种方法是依据: 
  没有特定宽度的非浮动块级元素,会在左右负外边距的情况下扩展其宽度
- 设置空距的替代方案:padding
  em单位是相对于文本的大小,放大文本会改变,而百分比与宽度有关
  ```css
   .col {
        float: left;
        box-sizing: border-box;
        min-height: 100px;
        outline: 1px solid #666;
        padding: 0 0.9% 1.375%;
      }
  ```
- 文字过长换行 
  ```css
  .col {
        word-wrap: break-word;
      }
  ```
## 浮动布局缺陷,锯齿效果
- 当一个浮动元素中的列过长时就会出现锯齿,

  flex 布局实现等高,flex:1 ->对多余的或者缩放的空间进行分配
![](img/%E9%94%AF%E9%BD%BF%E6%95%88%E6%9E%9C.png)

- 用inline-block 代替浮动
  ![](img/%E6%B5%AE%E5%8A%A8%E4%BD%BF%E5%90%8E%E8%BE%B9%E7%9A%84%E5%85%83%E7%B4%A0%E4%BD%8D%E7%BD%AE%E5%8F%98%E5%8C%96.png)

  ```css
   .row-wrapping {
        font-size: 0;
        margin: 0 -11px;
        margin: 0 -0.6875rem;
      }
      .row-wrapping > * {
        float: none;
        vertical-align: top;
        display: inline-block;
        font-size: 16px;
        font-size: 1rem;
      }
  ```
  ![](img/%E8%A1%8C%E5%86%85%E5%9D%97%E5%85%83%E7%B4%A0.png)
## 浮动
  - 浮动之后的文本会形成环绕,将浮动元素占据得空间留出来.其他除了文本的元素该怎么布局怎么布局,就当浮动元素不存在一样,有的甚至会覆盖.
  ![](img/%E6%B5%AE%E5%8A%A8%E7%95%99%E7%A9%BA%E9%97%B4.png)
  - 阻止文字环绕的效果,给文字所在的盒子清除浮动
    ```css
    .clear-float {
        clear: both;
      }
    ```
  ![](img/clear-float.png)
  - 父元素高度塌陷-BFC
    ```css
    .row:after {
        content: "";
        display: block;
        clear: both;
      }
    ```
- 网格布局(二维布局:可以跨行)
  ![](img/%E7%BD%91%E6%A0%BC%E5%B8%83%E5%B1%80.png)

用于表示列宽的单位:fr(fraction of available space)

repeat函数:repeat(5,1fr) -> 1fr 1fr 1fr 1fr 1fr


```css
/* 2行4列,行高300培训,4列等 */
.wrapper{
  display : grid;
  grid-template-rows: 300px 300px;
  grid-template-columns:1fr 1fr 1fr 1fr;
  /* grid-template-columns:repeat(4,1fr); */
}
```

由于网格轨道在DOM中并没有特定的元素表示,所以不能通过max-width或者min-width之类的属性来为它们指定大小,使用minmax()函数->minmax(4em,1fr)

```css
/* 简写:前边士行的定义,后边是列的定义,用'/'隔开 */
.wrapper{
  display : grid;
  grid-template: auto minmax(4em,1fr) minmax(4em,1fr)/repeat(5,1fr);
}
```
----
# 响应式布局

只创建一个能适配多种设备的网站:响应式网站

