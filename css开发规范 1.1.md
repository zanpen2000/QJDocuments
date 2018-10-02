# CSS 开发规范 1.1
---

修订人 | 版本号
---|---
张金龙、狄兆璐 | 1.0
刘贵生、汪任梦 | 1.1

---
## 目录
- [一、结构与样式分离](#一、结构与样式分离)
- [二、选择器的使用](#二、选择器的使用)
- [三、注释](#三、注释)
- [四、选择器顺序](#四、选择器顺序)
- [五、书写顺序](#五、书写顺序)
- [六、抽离公用样式](#六、抽离公用样式)
- [七、文档的结构化书写](#七、文档的结构化书写)
- [八、布局方式](#八、布局方式)
- [九、字体大小适配](#九、字体大小适配)
- [十、图片和图标](#十、图片和图标)
- [十一、定位](#十一、定位)
- [十二、关于响应式的自测](#十二、关于响应式的自测)
- [十三、其他注意事项](#十三、其他注意事项)
- [（附1）不同设备的分辨率设置](#（附1）不同设备的分辨率设置)
- [（附2）自适应布局](#（附2）自适应布局)

---

### 一、结构与样式分离
1. 禁止内部引用，统一使用外接的css文件，文件名和页面名或者组件名保持一致

    ```
    例：
        首页组件：      index.vue
        对应的样式文件： index.css
    ```

[**<p align="right">>>返回目录<<</p>**](#目录)

### 二、选择器的使用
1. 无论`web端`、`小程序`，按照区块划分页面区域，顶层元素放弃使用`class`类选择器，统一使用`id`选择器
2. 最外层id和css文件名保持一致

    ```
    例：
    搜索组件的样式文件叫：search.css

    对应的HTML代码
    <div id="search">
        <div class="search-content"></div>
    </div>

    对应的css文件
    <style>
    #search {
        width: 500px;
        height: 100px;
    }
    #search .search-content {
        margin-left: 10px;
    }
    </style>

    ```

[**<p align="right">>>返回目录<<</p>**](#目录)

### 三、注释
1. 每css文件开头使用块级注释

    ```
    例：
    /* 
    *
    * @author:张三
    * @date:2018-08-08
    * @instructions:文件介绍
    *
    */
    ```
2. 每个模块加上开始和结束标记，使用单行注释

    ```
    例：
    /*头部开始*/
    header {
        width:1200px;
        height:100px;
        background-color:pink;
    }
    /*头部结束*/
    ```
3. 实现外部引用有两种方式：
    
    a. 使用link标签引用css
    ```
        <link rel="stylesheet" href="./reset.css">
    ```
    b. 使用import导入css
    ```
        import "../style/reset.css"
    ```

[**<p align="right">>>返回目录<<</p>**](#目录)

### 四、选择器顺序
1. 严格嵌套
    - 从大到小（以选择器的范围为准 
    - 从低到高（以等级上的高低为准）
    - 从先到后（以结构上的先后为准）
    - 从父到子（以结构上的嵌套为准）
2. css优先级
    - 行内 => id => class => 标签选择器
    - 禁止使用.div #id不符合选择器优先级嵌套

[**<p align="right">>>返回目录<<</p>**](#目录)

### 五、书写顺序
1. 位置属性(position, top, right, z-index, display, float等)
2. 大小(width, height, padding, margin)
3. 文字系列(font, line-height, letter-spacing, color- text-align等)
4. 背景(background, border等)
5. 其他(animation, transition等)

    ```
    例：
    .box {
        position: relative;
        left: 10px;
        top: 20px;
        z-index: 999;
        width: 200px;
        height: 100px;
        padding: 10px 10px;
        font-size: 16px;
        color: #eee;
        background-color: #ccc;
        animation: fade .3s ease;
    }
    ```

[**<p align="right">>>返回目录<<</p>**](#目录)

### 六、抽离公用样式
1. 对于经常用的属性，可以将他抽离出来，做成公共样式，页面中直接引用对应的class名即可，如`弹性盒模型`、`左右浮动`、`清除浮动`。
    ```
    例：
    左浮动
        .left {
            float:left;
        }
        
    清除浮动
        .clear:after{
            display:block;
            clear:both;
            content:"";
            visibility:hidden;
            height:0
        }
        .clear{
            zoom:1
        }
    ```
2. 对于两个不同的类，其中部分属性及属性值完全一样，可以将他抽离出来，不同的属性再作区分
    ```
    例：
    <div id="box">
        <div class="item item1"></div>
        <div class="item item2"></div>
    </div>
        
    <style>
        #box .item {
            width: 200px;
            background-color: #ccc;
            border: 1px solid #eee;
            cursor: pointer;
        }
        #box .item1 {
            height: 100px;
        }
        #box .item2 {
            height: 50px;
        }
    </style>
    ```

[**<p align="right">>>返回目录<<</p>**](#目录)

### 七、文档的结构化书写
页面CSS文档都应采用结构化的书写方式，逻辑清晰易于阅读。
```
例：
<div id=”main-menu”>
    <ul>
        <li><a href=”#” >首页</a></li>
        <li><a href=”#” >介绍</a></li>
        <li><a href=”#” >服务</a></li>
    </ul>
</div>
<style>
    #main-menu {
        width:100%;
        height:30px;
        background:url(images/mainMenu_bg.jpg) no-repeat;
    }
    #main-menu ul li {
        float:left;
        line-height:30px;
        margin-right:1px;
        cursor:pointer;
    }
</style>
```

[**<p align="right">>>返回目录<<</p>**](#目录)

### 八、布局方式
根据每个项目需求的不同，选择合适的不同的布局方式，常见的有以下几种：静态布局，流式布局，自适应布局，响应式布局，弹性布局

[**<p align="right">>>返回目录<<</p>**](#目录)

### 九、字体大小适配
我们一般的常用单位 `em`、`rem`、`px`、`%` 四种
- em：结合父元素的font-size来根据屏幕宽度适配
- rem：结合html元素的font-size来根据屏幕宽度适配
- px：结合媒体查询进行不同设备分辨率进行适配
- %：按百分比自适应布局

`注意`：慎用em （因为em会叠加计算），如果用，尽量不要用在继承属性上

[**<p align="right">>>返回目录<<</p>**](#目录)

### 十、图片和图标
1. 前景图和背景图的选择
    - 前景图`<img>`:从页面元素来说，如果是页面中的图片是作为内容出现的，比如广告图片，比如产品图片，那么这个必然是用img了，因为这个是页面元素内容。
    - 背景图`background`，修饰性的内容，在页面中可有可无。有，是为了让页面中视觉感受上更美；无，并不影响用户浏览网页获取内容。
2. 背景图适应性
    - 等比缩小图片来适应容器
    
        ```
        background-size:contain;
        ```
    - 等比扩展图片来填满容器
    
        ```
        background-size:cover;
        ```
3. 能够适应比例变化的图片
    - 严格控制宽高的图片（服务器传的图片）
    
        ```
        宽度用百分比，高度用设计图高度
        ```
    - 不需要固定高度的图片（本地图片）

4. 图标优先使用矢量图
    - Icon是矢量的，可以自由适应各种尺寸大小,不会模糊
    - 占用空间很小，250个图标的字体只有不到300K
    - Icon Font可控性更高，可以用代码去控制大小、颜色、透明度、特效等

[**<p align="right">>>返回目录<<</p>**](#目录)

### 十一、定位
设计图说明是在浏览器固定定位的，用position:fixed；未说明的不可用

[**<p align="right">>>返回目录<<</p>**](#目录)

### 十二、关于响应式的自测
1. 缩小浏览器窗口
2. 更改显示器分辨率

[**<p align="right">>>返回目录<<</p>**](#目录)

### 十三、其他注意事项
- 重置好你的样式（[reset.css](https://meyerweb.com/eric/tools/css/reset/index.html)）
- 减少浮动的使用，使用弹性和模型解决。
- 在结构内部少使用定位。
- 能用高度解决的，尽量少使用`padding`,能用`padding`解决的问题尽量少使用`margin`。
- 尽可能使用`css3`选择器解决，能用`css`解决的问题，尽量不使用`js`。
- 减少行内样式的使用，使用`数据驱动`或用`class`解决。
- 减少使用 `!important`。
- 避免层级嵌套太多，遵循能选中即可。
- 颜色使用十六进制或者RGBA，禁止使用red,black等英文。
- 能用连写的尽量用连写，如margin:10px 20px；
- 尽量少用无关紧要的div
- 不要使用内联元素（inline）
- 摒弃任何冗余结构和不使用100%设置
- 使用HTML5 Doctype和相关指南


[**<p align="right">>>返回目录<<</p>**](#目录)

---

## （附1）不同设备的分辨率设置
#### 1024显屏
```
@media screen and (max-width : 1024px) {                    
/* 样式写在这里 */          
}     
```
#### 800px显屏
```
@media screen and (max-width : 800px) {                    
/* 样式写在这里 */          
}     
```
#### 640px显屏
```
@media screen and (max-width : 640px) {                    
/* 样式写在这里 */          
}     
```
#### iPad横板显屏
```
@media screen and (max-width : 1024px) {                    
/* 样式写在这里 */          
}     
```
#### iPad竖板显屏
```
@media screen and (max-device-width: 768px) and (orientation: portrait {                    
/* 样式写在这里 */          
}     
```
#### iPhone 和 Smartphones
```
@media screen and (min-device-width: 320px) and (min-device-width: 480px) {              
/* 样式写在这里 */            
} 
```

[**<p align="right">>>返回目录<<</p>**](#目录)

## （附2）自适应布局
```
　<meta name="viewport" content="width=device-width, initial-scale=1" />
```
>viewport是网页默认的宽度和高度，上面这行代码的意思是，网页宽度默认等于屏幕宽度（width=device-width），原始缩放比例（initial-scale=1）为1.0，即网页初始大小占屏幕面积的100%。

[**<p align="right">>>返回目录<<</p>**](#目录)
