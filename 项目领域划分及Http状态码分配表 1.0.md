# 项目领域划分及Http状态码分配表 1.0

> # 说明
> - 状态码是一组由“0~9，a~z”组成的6位字符串，分为三级（第一位、第二三位、第四至第六位）
> - 第一级：第一位 表示 **业务领域** 【0~9、a~z】
> - 第二级：第二、三位 表示 **服务**  【00~99】
> - 第三级：第四五六位 表示 **状态码** 【100~599遵循默认值，600~999开发自定义】
> - 新建项目按业务领域（第一级状态码）分类，第二级定义项目名称及服务状态码
>
> ```java
>   //示例
>   # 103401  -> 人资在线测评，未授权（请求要求身份验证）
>   # x01202  -> 隐号拨打基础服务，服务器已接受请求，但尚未处理。
>   # z04503  -> 平台架构-消息中心，服务不可用（由于超载或停机维护）
> ```
>
> ---

## 第一级说明
状态码|说明|缩写|备注
-|-|-|-
0|成功||例 0
1|人力资本（简称：人资）|`HCD`|人力资本部：<font color=orange>**H**</font>uman <font color=orange>**C**</font>apital <font color=orange>**D**</font>epartment
2|培训教育（简称：培训）|`TME`|培训教育部：<font color=orange>**T**</font>raining <font color=orange>**M**</font>inistry of <font color=orange>**E**</font>ducation
3|财务|`GAD`|财务部：<font color=orange>**G**</font>eneral<font color=orange>**A**</font>ccounting <font color=orange>**D**</font>epartment
4|行政|`ADM`|行政部：<font color=orange>**Adm**</font>inistration Department
5|置业|`BRD`|置业部：<font color=orange>**Br**</font>oker <font color=orange>**D**</font>epartment
6|权证|`PRD`|权证部：<font color=orange>**Pr**</font>operty <font color=orange>**D**</font>epartment
7|业务拓展（简称：市场）|`BED`|业务拓展部：<font color=orange>**B**</font>usiness<font color=orange>**E**</font>xpending <font color=orange>**D**</font>epartment
8|企业文化宣传（简称：宣传）|`CPD`|企业文化宣传部：<font color=orange>**C**</font>orporate Culture <font color=orange>**P**</font>ropaganda <font color=orange>**D**</font>epartment
9|运营|`OPD`|运营部：<font color=orange>**Op**</font>eration <font color=orange>**D**</font>epartment
a|法务|`LAD`|法律事务部：<font color=orange>**L**</font>egal <font color=orange>**a**</font>ffairs <font color=orange>**D**</font>epartment
<font color=green>b~m</font>|<font color=green>预留领域</font>||<font color=green>b至m，为其他领域预留号码</font>
n|网络科技（简称：网络）|`NTD`|网络技术部：<font color=orange>**N**</font>etWorks <font color=orange>**T**</font>echnology <font color=orange>**D**</font>epartment
<font color=green>o~v</font>|<font color=green>预留领域</font>||<font color=green>o至v，为其他领域预留号码</font>
w|对外网站与应用（简称：外部）|`WEB`|面向千家以外人群的产品（如：企业宣传网站、在线发布房源小程序、过户进度查询等）
x|平台设施-公共服务|`PUB`|公共服务：<font color=orange>**Pub**</font>lic Service
y|平台设施-基础服务|`BAS`|基础服务：<font color=orange>**Bas**</font>ic services
z|平台设施-平台架构|`UPA`|统一平台架构：<font color=orange>**U**</font>niversal <font color=orange>**P**</font>latform <font color=orange>**A**</font>rchitecture

## 第二级说明
状态码|说明|所属领域|项目名|项目地址|备注
-|-|-|-|-|-
**==1==**|**==人资==**|人力资本|||`招聘/入职/调岗/离职/辞退/复职/人员分配/职级晋升`
100|人资领域项目集合|人力资本|`人资领域的项目集合预留`
101|人资招聘|人力资本|HCD_recruitment||
102|简历（含测评）|人力资本|HCD_curriculum_vitae||原102+103（HCD_resume【简历】+HCD_assessment【在线测评】）|
103||人力资本|||
104|人资隐号|人力资本|HCD_hidden_call||原项目地址：https://hr.hiddencall.allhome.com.cn
105|人资报表|人力资本|HCD_report||
106|人资助手|人力资本|HCD_assistant||
**==2==**|**==培训==**|培训教育|||`培训组织/会议组织/培训签到/培训考核/培训资料管理/直播管理/讲师管理/转化率分析`
200|培训领域项目集合|培训教育|`培训领域的项目集合预留`
201|活动助手|培训教育|TME_activity_assistant||会务，活动助手概念升级
**==3==**|**==财务==**|财务|||`报销管理/请款/发放工资/置业收,退,转向管理/成本利润核算[总]/工资核算`
300|财务领域项目集合|财务|`财务领域的项目集合预留`
301|财务报帐|财务|GAD_report_accounts||
**==4==**|**==行政==**|行政|||`置业检查/物资管理/卷宗管理`
400|行政领域项目集合|行政|`行政领域的项目集合预留`
401|考勤|行政|ADM_check_attendance||
**==5==**|**==置业==**|置业|||`房源采集/房源发布/房源跟进管理/楼盘库管理/客源采集/客源跟进管理/成交管理/成租管理/人员管理`
500|置业领域项目集合|置业|`置业领域的项目集合预留`
501|经纪人考试|置业|BRD_exam||
502|置业隐号|置业|BRD_hidden_call||原项目地址：https://miniapp.hiddencall.allhome.com.cn/?
503|所有权核验|置业|BRD_ownership_query||
**==6==**|**==权证==**|权证|||`快件业务/高评/代办过户/代办贷款/代签合同/代纳房契税/权证财务管理`
600|权证领域项目集合|权证|`权证领域的项目集合预留`
**==7==**|**==业务拓展（简称：市场）==**|市场|||`市场拓展/市场监管与发现/市场统计数据分析`
700|业务拓展（市场）领域项目集合|市场|`业务拓展（市场）领域的项目集合预留`
**==8==**|**==企业文化宣传（简称：宣传）==**|宣传|||`渠道统计分析/宣传计划管理/宣传效果统计分析`
800|企业文化宣传（宣传）领域项目集合|宣传|`企业文化宣传（宣传）领域的项目集合预留`
801|电子明信片|宣传|CPD_electronic_postcard
802|企业宣传网站|宣传|CPD_company_site
**==9==**|**==运营==**|运营|||`市场分析/运营监管/成本利润分析[总]`
900|运营领域项目集合|运营|`运营领域的项目集合预留`
901|千家MIS-BI篇|运营|OPD_statistical_analysis
**==a==**|**==法务==**|法务|||`业务办理风险评估/法律纠纷统计/法律风险统计/扣罚统计/解决法律纠纷`
a00|法务领域项目集合|法务|`法务领域的项目集合预留`
**==b~m==**|**==预留区==**||||
b~m|`预留区域`|`预留区域`|||
**==n==**|**==网络科技（简称：网络）==**|网络|||`人员档案管理/资源管理/项目管理`
n00|网络领域项目集合|网络|`网络领域的项目集合预留`
n01|资源管理|网络|NTD_resources||包括图书管理、设备管理、办公用品管理等
n02|项目管理|网络|NTD_project||包括：GitLab检查情况的录入，统计（按项目、按人员），支持选取里程碑，自动获取数据生成然尽图，支持统计各人员在时间段内的项目从属
**==o~v==**|**==预留区==**||||
o~v|`预留区域`|`预留区域`|||
**==x==**|**==平台设施-公共服务==**|平台设施-公共服务|||
x00|平台设施-公共服务|公共服务|`预留`
x01|隐号拨打（基础服务)|公共服务|PUB_HiddenCall||原项目地址：https://hiddencall.allhome.com.cn
x02|人脸识别|公共服务|PUB_FaceRecognition||原项目地址：https://face.allhome.com.cn
x03||公共服务||
x04|税费、贷款计算器|公共服务|PUB_Calculator||原X03（税费计算器）与原X04（贷款计算器）合并为“X04（税费、贷款计算器）”
x05|绘制图形|公共服务|PUB_DrawingGraphics
x06|全景看房|公共服务|PUB_HousePanorama
x07|记事本|公共服务|PUB_CommonNotepad
x08|房源验证|公共服务|PUB_HousingSourceVerify
x09|产权核验服务|公共服务|platform_PUB_property_verification||？？
x10|语音转文字|公共服务|PUB_VoiceToText
x11|人脸识别在线服务|公共服务|PUB_FaceRecognitionOnline
x12|Java公共Jar包|公共服务|PUB_FrameWork_Java
x13|集团网电话号码管理|公共服务|PUB_GroupNetworkTelNum_Java
**==y==**|**==平台设施-基础服务==**|平台设施-基础服务|||
y00|平台设施-基础服务|基础服务|`预留`
y01|权限|基础服务|platform_BAS_permission
y02|组织机构|基础服务|BAS_orgnization||升级合并到人源库项目中
y03|鉴权授权中心|基础服务|BAS_AuthenticationAuthorization
y04|安全包|基础服务|BAS_safety
y05|前端组件库|基础服务|BAS_QUI
y06|人源库|基础服务|BAS_HumanSourceLibrary
y07|短信网关|基础服务|BAS_SMSGateway
y08|房客源库|基础服务|BAS_HousingCustomer_Library
y09|手机号码段归属地查询|基础服务|BAS_phone_arrtibution
Y10|鉴权授权钥匙扣|基础服务|BAS_Keychain|https://git.allhome.com.cn/Platform/BAS/BAS_Authentication_Authorization/BAS_Keychain|鉴权授权中心（Y03）项目的子项目，调用人脸识别服务
**==z==**|**==平台设施-平台架构==**|平台设施-平台架构|||
z00|平台设施-平台架构|平台架构|`预留`
z01|服务注册/发现|平台架构|platform_UPA_eureka
z02|网关服务|平台架构|platform_UPA_gateway
z03|日志服务|平台架构|platform_UPA_log
z04|消息中心|平台架构|platform_UPA_message_center
z05|认证中心|平台架构|platform_UPA_authentication_center
z06|资源服务-图片|平台架构|platform_UPA_resources
z07|cap分布式事务|平台架构|platform_UPA_cap||原项目地址：https://cap.allhome.com.cn

## 第三级说明
状态码|说明|备注
-|-|-
**==1xx==**|**临时响应**|**表示临时响应并需要请求者继续执行操作的状态代码。**
100|继续|请求者应当继续提出请求。服务器返回此代码表示已收到请求的第一部分，正在等待其余部分。
101|切换协议|请求者已要求服务器切换协议，服务器已确认并准备切换。
**==2xx==**|**成功**|**表示成功处理了请求的状态代码。**
200|成功|服务器已成功处理了请求。通常，这表示服务器提供了请求的网页。
201|已创建|请求成功并且服务器创建了新的资源。
202|已接受|服务器已接受请求，但尚未处理。
203|非授权信息|服务器已成功处理了请求，但返回的信息可能来自另一来源。
204|无内容|服务器成功处理了请求，但没有返回任何内容。
205|重置内容|服务器成功处理了请求，但没有返回任何内容。
206|部分内容|服务器成功处理了部分 GET 请求。
**==3xx==** |**重定向**|**表示要完成请求，需要进一步操作。通常，这些状态代码用来重定向。**
300 |多种选择|针对请求，服务器可执行多种操作。服务器可根据请求者（user agent）选择一项操作，或提供操作列表供请求者选择。
301 |永久移动|请求的网页已永久移动到新位置。服务器返回此响应（对 GET 或 HEAD 请求的响应）时，会自动将请求者转到新位置。
302 |临时移动|服务器目前从不同位置的网页响应请求，但请求者应继续使用原有位置来进行以后的请求。
303 |查看其他位置|请求者应当对不同的位置使用单独的 GET 请求来检索响应时，服务器返回此代码。
304 |未修改|自从上次请求后，请求的网页未修改过。服务器返回此响应时，不会返回网页内容。
305 |使用代理|请求者只能使用代理访问请求的网页。如果服务器返回此响应，还表示请求者应使用代理。
307 |临时重定向|服务器目前从不同位置的网页响应请求，但请求者应继续使用原有位置来进行以后的请求。
**==4xx==**|**客户端错误**|**这类的状态码代表了客户端看起来可能发生了错误，妨碍了服务器的处理。**
400|错误请求|服务器不理解请求的语法。
401|未授权|请求要求身份验证。对于需要登录的网页，服务器可能返回此响应。
403|禁止|服务器拒绝请求。
404|未找到|服务器找不到请求的网页。
405|方法禁用|禁用请求中指定的方法。
406|不接受|无法使用请求的内容特性响应请求的网页。
407|需要代理授权|此状态代码与 401（未授权）类似，但指定请求者应当授权使用代理。
408|请求超时|服务器等候请求时发生超时。
409|冲突|服务器在完成请求时发生冲突。服务器必须在响应中包含有关冲突的信息。
410|已删除|如果请求的资源已永久删除，服务器就会返回此响应。
411|需要有效长度|服务器不接受不含有效内容长度标头字段的请求。
412|未满足前提条件|服务器未满足请求者在请求中设置的其中一个前提条件。
413|请求实体过大|服务器无法处理请求，因为请求实体过大，超出服务器的处理能力。
414|请求的 URI 过长|请求的 URI（通常为网址）过长，服务器无法处理。
415|不支持的媒体类型|请求的格式不受请求页面的支持。
416|请求范围不符合要求|如果页面无法提供请求的范围，则服务器会返回此状态代码。
417|未满足期望值|服务器未满足"期望"请求标头字段的要求。
**==5xx==**|**服务器错误**|**这些状态代码表示服务器在尝试处理请求时发生内部错误。这些错误可能是服务器本身的错误，而不是请求出错。**
500|服务器内部错误|服务器遇到错误，无法完成请求。
501|尚未实施|服务器不具备完成请求的功能。例如，服务器无法识别请求方法时可能会返回此代码。
502|错误网关|服务器作为网关或代理，从上游服务器收到无效响应。
503|服务不可用|服务器目前无法使用（由于超载或停机维护）。通常，这只是暂时状态。
504|网关超时|服务器作为网关或代理，但是没有及时从上游服务器收到请求。
505|HTTP 版本不受支持|服务器不支持请求中所用的 HTTP 协议版本。
