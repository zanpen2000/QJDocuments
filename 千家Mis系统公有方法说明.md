> ## Mis系统公有方法说明

由于原有MIS·至哲系统存在过多缺陷，故而对其进行重写，由于子项目对其依赖性较大，需要用到MIS系统中的一些公有方法，使用文档对MIS系统暴露的公有方法进行说明。

> globalLogout - 退出登录方法（未作更改）

使用场景：用户token过期时使用或需要退出登录时使用。

示例：

```
//  无参
parent.window.globalLogout();
```

> globalOpenChildApp - 打开新标签

使用场景：需要在MIS系统中打开新标签。

示例：

```JavaScript
//  参数
//  类型：Object
//  参数说明：
//  {
//      code:344, //	必传,项目code
//      name:"房屋产权查询",//	必传,见说明
//      url:"https://dosq.allhome.com.cn"//	必传，打开页面连接
//  }

let arg = {
    code:344,
    name:"新房应收单 - FG20200101",
    url:"https://dosq.allhome.com.cn"
}
parent.window.globalOpenChildApp(arg);
```

> globalOpenWindow - 打开新窗口（未作更改）

使用场景：在Mis系统中打开一个新的窗口，该窗口与Mis分开。

示例：

```javaScript
//  参数
//  url：string     必传，需要打开的url
//  option：object  非必传
//      align：stirng | 窗口Y坐标位置，start|center|end可选参数，默认值，center
//      justify：string | 窗口X坐标位置，start|center|end可选参数，center
//      width：number | 窗口宽度
//      height：number | 窗口高度
//      fixedTop：boolean | 顶部固定，默认值 false
//      resizable：boolean | 是否允许手动调整窗口大小，默认值 true
//  native：string  非必传，使用原生配置
parent.window.globalOpenWindow("http://www.baidu.com");
```

> $printPage - 打印（未作更改）

使用场景：需要打印页面

示例：

```JavaScript
//  参数
//  webUrl：string
parent.window.$printPage("http://www.baidu.com");
```

> $saveDialog - 下载文件（未作更改）

使用场景：需要导出文件，如Excel

```javascript
//  参数
//  baseCode：string    必传，导出文件base码
//  fileType：string    必传，导出文件类型 excel | image
//  fileName：string    必传，导出文件名称
parent.window.$saveDialog("baseCode","image","新房应收单-20200109");
```

> $loading - 全局loading

使用场景：该loading在MIS系统中全屏展示

```javascript
//  使用方法与element-ui的loading方法一致
let obj = {
    lock: true,
    text: 'Loading',
    spinner: 'el-icon-loading',
    background: 'rgba(0, 0, 0, 0.7)'
};
parent.window.$loading(obj);
```

> $shell - 打开本地文件

使用场景：用户上传文件时，还没有上传到oss时，用户点击文件，通过File获取到本地路径，打开用户电脑中对应的文件

```javascript
parent.window.$saveDialog("这里是url");
```

> openRemoteFile - 打开方法

当用户想查看上传的文件时，此时文件已经上传到oss需要通过该方法静默下载到用户本地之后(Downloads文件夹，默认路径不能更改)，下载完成之后自动打开文件。

```javascript
parent.window.openRemoteFile("这里是url");
```
