> ## 千家Web标准库使用说明文档

- [简介](#1-简介)  
- [安装](#2-安装)  
- [引用](#3-引用)  
- [使用介绍](#4-使用介绍)  

> #### 1. 简介

为提高现有工作开发效率，能够更加的规范化各个项目代码情况，开发web端标准库，针对各个项目中常用方法进行封装，以达到代码规范化初步效果。

> #### 2. 安装

web端标准库上传到公司内部管理仓库中，若想使用npm安装使用，需要先将下载源指向公司内部地址：

```
//  私有仓库
npm config set registry http://39.106.145.141:9000/repository/node-public/
//  公共仓库
npm config set registry http://registry.npmjs.org/
```

安装：

```
npm install --save-dev common
```

cdn引用

```
<script src="https://qjsl.allhome.com.cn/index.js"></script>

externals: {
    "common": 'QjMethod'
}
```

> #### 3. 引用

安装完成之后需要在项目中正常引用

```
import common from "common";
```

由于现版本功能不完善提供的东西不是太多，包括内容：

1. middleware - Vue中间件
2. Request - axios二次封装
3. ControlToken - 控制token的设置与获取(统一登录)
4. ProxyIframe - 跨页面通信(统一登录)

> #### 4. 使用介绍

介绍各个模块的使用方法：

> middleware

```
import {middleware} from "common";
Vue.use(middleware);
```

middleware中包含V-by指令，用于统一登录按钮权限，v-by:

```html
<el-button v-by:arg="['123']" limit="123">导出</el-button>
```

方法：

```JavaScript
let a = {a:1};
//  目前只有深度拷贝对象方法
let o = this.$Qj.cloneDeep(a);
```

> Request

使用：

*.js

```JavaScript
import {Request} from "common";
import api1 from "@/api/a2.js";

//  默认参数
//      第一个参数axios配置
//      当前环境变量
//      项目名称
let request = new RequestFactory({
    baseURL: "http://192.168.10.200:8010/api"
},"development","domes");

//  拦截器
request.interceptors({
    request:(config) => {
        return config;
    },
    response:(config) => {
        let {data} = config;
        if(data.StatusCode && data.StatusCode !== 200) return Promise.reject(data);
        return data.Model;
    },
    error:error => {
        return Promise.reject(error.data);
    }
})

//  添加数据
request.add("api1",api1);

//  创建
let a1 = request.create("api1");

//  发起请求
a1.getHead({
    param:["head"],
    query:{
      b:132132
    },
    data:{
      a:1321231
    }
}).then((res) => {
console.log(res);
})
```

a2.js

```JavaScript
const apiArr = [
  {
    url:"/list/tabel",
    method:"get",
    defaultData:{
      a:1
    },
    name:"getHead"
  }
];

export default apiArr;
```

> ControlToken

setToken 仅限 `globalToken`和`token`

```JavaScript
let controlToken = new ControlToken();
controlToken.setToken("globalToken","23211321312121");
console.log(controlToken.getToken());
```

> ProxyIframe

父应用：

```JavaScript
import {ProxyIframe} from "common";

const globalPath = new Map([
    ['development', {
        domain: "qj.com",
        portal: "http://wrp.qj.com"
    }],
    ['lan', {
        domain: "qj.com",
        portal: "http://wrp.qj.com"
    }],
    ['pred', {
        domain: "allhome.com.cn",
        portal: "https://dmis.allhome.com.cn"
    }],
    ['production', {
        domain: "allhome.com.cn",
        portal: "https://mis.allhome.com.cn"
    }]
])

//  生产环境变量
const env = process.env.NODE_ENV;
//  实例化代理
const proxyIframe = new ProxyIframe({env,type:"prent"});
//  对比token
//  子应用更新token时,对比token是否发生改变,未改变重写cookie
let contrastToken = "";
//  正在写入token...
let cookieWriteing = null;

!function proxyInit() {
    proxyIframe.solve(globalPath);
    proxyIframe.run("globalToken", () => {
        //  正在写入token...,并且有对照token
        if (cookieWriteing && contrastToken) return contrastToken;
        //  有token返回token
        if (cookieToken) return cookieToken;
    }, val => {
        if (!val) return
        //  没有对照token或者token发生改变,写入token
        if (!contrastToken || (contrastToken != val)) {
            //  更新cookie中...
            cookieWriteing = setTimeout(() => {
                clearTimeout(cookieWriteing);
                cookieWriteing = null;
            }, 1000)
            //  写入token
            contrastToken = val;
        }
    });
}();
```

子应用：

```JavaScript
import {ProxyIframe} from "common";
const globalPath = new Map([
    ['development', {
        domain: "qj.com",
        portal: "http://wrp.qj.com"
    }],
    ['lan', {
        domain: "qj.com",
        portal: "http://wrp.qj.com"
    }],
    ['pred', {
        domain: "allhome.com.cn",
        portal: "https://dmis.allhome.com.cn"
    }],
    ['production', {
        domain: "allhome.com.cn",
        portal: "https://mis.allhome.com.cn"
    }]
]);
const env = process.env.NODE_ENV;
const proxyIframe = new ProxyIframe({env,type:"child"});
proxyIframe.solve(globalPath);
proxyIframe.run("token",
                () => parent.window.globalToken,
                val => parent.window.globalToken = val);
```

> ### 导出excel

```JavaScript
import {DownExcel} from "common";
let downExcel = new DownExcel({
    //  表头数据
    head,
    //  导出数据
    data:res,
    //  data数据中所需要导出数据的字段
    key:"data",
    //  文件名称
    fileName:"Exportsuccess",
    //  导出数据表头所需导出数据的字段
    headKey:"headerFirst",
    //  合并单元格信息
    merge:{
        //  头部信息
        head:[
            ['部门', null, null, '其它信息']
        ],
        //  合并单元格
        info:[
            // 设置A1-C1的单元格合并
            {
                //  开始
                //  r：第几行
                //  c：第几个单元格
                s: {r: 0, c: 0}, 
                //  结束
                //  r：第几行
                //  c：合并到第几个单元格，从0开始
                e: {r: 0, c: 2}
            },
            {
                s:{r:0, c:3},
                e:{r:0, c:11}
            }
        ]
    }
}).
downExcel().    //  开始导出
then(() => {
    console.log("导出成功");
})；
```

> ### 异步队列同步请求

```JavaScript
AsyncWhile(() => {
  return // 条件
}, async () => {
    //  请求
}).then((res) => {
    //  请求成功    res为数据集合
}).catch((error) => {
    //  其中有数据请求错误
    //  error错误信息
});
```

> ### 常用正则

```JavaScript
//  存在对象中
import {collectionRegExp} from "common";
//  ticketDeal  chinese
//  为函数
chinese("0,50") //  0-50的个中文字符
```

> ### 常用校验方法

```JavaScript
//  存放一些常用的校验方法
import {testMethod} from "common";
```

> ### 原型添加方法

```JavaScript
import {mountNumber,
        mountArray,
        mountString} from "common";
mountNumber();
//  数字查用方法
//  changeToChinese 转中文 ****元
//  micrometer  添加千分符
//  numberToChinese 数字转大写
mountArray();
//  数组常用方法
//  checkEl 查找元素
//  checkIndex 获取index
//  plan    数组占总数值的百分比是多少
//  sort    排序
mountString();
//  常用校验方法
//  mountTrim   去除空格
//  passwordCheck   密码强度校验
//  常用校验方法 例如："1380013800".isPhone();
```

> ### 单例

```JavaScript
import {Singleton} from "common";
let singleton = new Singleton();
//  存储
singleton.createInstance("需要创建的实例","s实例名称","...参数");
//  创建
singleton.getInstance("$_requestFactory");
```

