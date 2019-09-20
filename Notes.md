<center><font color='blue' size='15'>Front end interview</font></center>
### CSS

##### BFC原理解析与应用

​		**块级格式化上下文**（Block Formatting Context，BFC）是Web页面的可视化CSS渲染部分，它是块级元素布局出现的区域，也是浮动层元素进行交互的区域，该区域是独立存在的，即BFC内部元素与外部元素之间不会相互影响。

​		**BFC能够解决的问题**

1. 解决浮动定位

2. 解决外边距合并

3. 清除浮动

4. 自适应多栏布局

5. ......

   ​	**BFC创建方式**

1. html元素或者包含html的元素

2. 设置浮动属性的元素（display:none除外）

3. 设置绝对定位属性的元素（absolute或者fixed）

4. display为inline-block、table-cell、table-caption的元素

5. 设置overflow属性的元素（visible除外）

6. 弹性盒子（flex布局）

7. 栅栏布局元素（grid布局）

   ​	**BFC约束规则**

- 内部Box会在垂直方向上一个接一个的放置

- 垂直方向上的距离由margin决定（或者：处于同一个BFC的两个相邻Box的margin会发生重叠（塌陷），与方向无关）

- 每个元素的左外边距与包含块的左边界接触（从左到右），即使浮动元素也是如此。（说明BFC中子元素不会超出他的包含块，而position为absolute的元素可以超出他的包含块边界）

- BFC的区域不会与float的元素区域重叠

- <font color='hotpink'>计算BFC的高度时，浮动子元素也要参与计算</font>

- BFC就是页面上的一个隔离的独立容器，容器里面的子元素和外部元素之间不会相互影响

  ​	**BFC的应用**

1. 解决外边距合并

   ```html
   <!-- before：两个p元素处在同一BFC区域 -->
   <style>
       p{
           width:100px;
           height:100px;
           margin:20px;
           text-align:center;
           line-height:100px;
           background-color:lime;
       }
   </style>
   <body>
       <p>top</p>
       <p>bottom</p>
   </body>
   ```

   ![before](https://github.com/heiye-vn/Question-of-the-day---front-end-interview/blob/master/BFC/before.png)

   ```html
   <!-- after：让处在同一BFC区域的p元素处于不同的BFC区域 -->
   <style>
       div{
           position:absolute;	/* 让div成为BFC区域 */
       }
   </style>
   <body>
       <p>top</p>
       <div><p>bottom</p></div>
   </body>
   ```

   ![](https://github.com/heiye-vn/Question-of-the-day---front-end-interview/blob/master/BFC/after.png)

2. 解决浮动定位（让浮动元素与周围元素等高）

```html
<!-- before -->
<style>
        #box{
            margin: 50px;
            background-color:#888;
            border: 1px solid red;
        }
        .float{
            float: left;
            width: 200px;
            height: 200px;
            background-color:lime;
        }
    </style> 
<div id="box">
        <div class="float">浮动元素</div>
        <div>未浮动元素</div>
 </div>
```

![](https://github.com/heiye-vn/Question-of-the-day---front-end-interview/blob/master/BFC/before2.png)

```html
<!-- after -->
<style>
        #box{
            margin: 50px;
            background-color:#888;
            border: 1px solid red;
            overflow:hidden;		/* 创建BFC */
        }
        .float{
            float: left;
            width: 200px;
            height: 200px;
            background-color:lime;
        }
    </style> 
<div id="box">
        <div class="float">浮动元素</div>
        <div>未浮动元素</div>
 </div>
```

![](https://github.com/heiye-vn/Question-of-the-day---front-end-interview/blob/master/BFC/after2.png)
