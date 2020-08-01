# css 页面布局与网格

## 1.布局的介绍
- 固定布局
- 弹性布局
- 流动布局
  
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