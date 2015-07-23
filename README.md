# 域名需要经过授权后才能操作以下接口 #

## 获取优通uid 与工作人员联系 ##

## 获取优通key 与工作人员联系 ##

## 获取优通secret 与工作人员联系 ##

## **TOKEN算法** ##

base64(sha1(当前页面地址+UID+key+secret))  


 例子： 

**url:**`http://www.abcd.com/show.html?id=1`

**uid:**`ynhuace`

**key:**`fsdf44874s`

**secret:**`fs888fs557fsief48`

 `base64(sha1("http://www.abcd.com/show.html?id=1ynhuacefsdf44874sfs888fs557fsief48"))  `

 结果：`MzkxOTY3NjRiNWUzYTUxNGM0ZDk3ZDhjNjJiOGQ1ZmM0ODA1MTg5Nw`
 
 


## **获取通信TOKEN(临时 还是自己算出TOKEN吧)** ##

每个页面对应一个TOKEN，TOKEN是固定的可以保存到本地。请不要频繁获取TOKEN

当前页面GET请求目标  
> `http://server.ucomm.cn/tool/优通UID/优通KEY/token.json`

GET参数
* sceneid：场景ID（如使用以下字段必选此参数）
* scenemint：商户自定义数字字段（可选）
* scenemtext：商户自定义文本字段（可选）
 
例子 `http://server.ucomm.cn/tool/优通UID/优通KEY/token.json?sceneid=场景ID&scenemint=用户ID  `
验证这个场景是否属于这个用户

返回：

    {"success":true,"code":200,"token":"TOKEN"}


## 创建场景 ##

当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/addsave.json`

POST参数

* name：场景名称
* tag：标签
* file：别名
* description：场景描述
* mint:商户自定义数字字段(可选/方便商户实现自己的业务逻辑,比如存储商户用户ID等)
* mtext:商户自定义文本字段(可选/方便商户实现自己的业务逻辑)

返回

    {"code":200,"message":"场景创建成功","id":场景ID}

## 获取场景列表 ##

当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/list.json`

GET可选参数

* keyword：名称关键字
* page：当前页码
* category：类别ID
* mint:商户自定义数字字段
* mtext:商户自定义文本字段

返回

    {"code":200,"message":"操作成功","list":[{"name":"新品推广","description":"欢迎使用本产品","picture":"http://7xizfo.com1.z0.glb.clouddn.com/no_img.png","creationtime":"2015/5/19 22:10:15","updatetime":"2015/5/19 22:10:15","file":"fsd","mint":3,"mtext":"","browse":0,"share":0,"tel":0,"copyright":"0"},{"name":"我的场景","description":"这是我的第一个测试","picture":"http://7xizfo.com1.z0.glb.clouddn.com/no_img.png","creationtime":"2015/5/19 21:46:10","updatetime":"2015/5/19 21:46:10","file":"adg","mint":null,"mtext":null,"browse":0,"share":0,"tel":0,"copyright":"0"}],"page":{"count":1,"pageNo":1,"pagesize":20}}

 

## 获取表单列表 ##
当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/form.json`

GET可选参数

* page：当前页码
* sceneid：场景ID

返回

    {"code":200,"message":"操作成功","list":[{"name":"新品推广","description":"欢迎使用本产品","picture":"http://7xizfo.com1.z0.glb.clouddn.com/no_img.png","creationtime":"2015/5/19 22:10:15","updatetime":"2015/5/19 22:10:15","file":"fsd","mint":3,"mtext":"","browse":0,"share":0,"tel":0,"copyright":"0"},{"name":"我的场景","description":"这是我的第一个测试","picture":"http://7xizfo.com1.z0.glb.clouddn.com/no_img.png","creationtime":"2015/5/19 21:46:10","updatetime":"2015/5/19 21:46:10","file":"adg","mint":null,"mtext":null,"browse":0,"share":0,"tel":0,"copyright":"0"}],"page":{"count":1,"pageNo":1,"pagesize":20}}


## 去版权 ##

当前页面POST请求目标  建议在后台处理
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/copyright.json`

POST参数

* file：场景别名


## 场景上线 ##

当前页面POST请求目标  建议在后台处理
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/online.json`

POST参数

* file：场景别名


## 场景设计器 ##

在页面中头部加上：

>  `<html lang="en" ng-app="app" ng-controller="AppCtrl">``

在BODY中间加入:


    <!--程序骨架-->
    <script>
    var release_url="admin.html";   //场景发布成功后跳转网址
    var api_uid="APIUID";  //优通帐号
    var api_key="APIKEY"; //APIKEY
    var api_token="TOKEN";
    var mint=""; //商户自定义数字ID
    //商户载入自定义接口  不需要就为空
    /* 
    var uapi_id='huiyi_page'; //接口插件名称唯一
    var uapi_data=[{name: "报名表单",value:"1","diy":"自定义"},{name: "留言表单",value:"2","diy":"自定义"}];  //下拉数据源
    var uapi_name='表单';
    var uapi_description='可以设置成当前用户可用的表单';
     */

    //商户载入自定义模板 不需要就为空
    var uapi_tplid='14305997870'; //模板ID 替换原有的模板分类 例： 表单模板 id=14305997870
    var uapi_tpldata=[{"id":"1","name":"类别1","Parent":"14305997870"},{"id":"2","name":"类别2","Parent":"14305997870"}];//模板分类
    var uapi_tpllist='http://server.ucomm.cn/uem/aj_page/list.js?a=json'; //你的模板列表数据源地址  改成你的数据源地址  URL后面会自动加上 id={id}&parent={parent}
    var uapi_tplpage='http://server.ucomm.cn/uem/aj_page/page.js?a=json'; //你的模板页面数据源地址  改成你的数据源地址  URL后面会自动加上 id={id}&parent={parent} 
 
    </script>
    <script src="http://server.ucomm.cn/uem/scene.min.js"></script>
    <div id="ume_load"><div class="divam"></div>拼命加载中...</div><!--加载等待效果,可以自己设计一个,加载完成后会自动删除这个DOM
    <div id="cache"></div>
    <div id="uce_box" ng-view></div>
    <!--/程序骨架-->

访问页面路径

> http://商户域名URL#/scene/create/场景ID
    

## 场景展示: ##


在您的页面中引用JS代码:

    <script src="http://server.ucomm.cn/uem/show.min.js"></script>

通过URL访问 

> http://您的域名/您的页面文件名?场景别名

支持打包成本地APP安装版,目前只测试安卓版生成.

如果您不需要配置自己的的域名，可以使用云画册默认访问地址  `http://my.yunhuace.com/scene/别名.html`

[下载演示](http://server.ucomm.cn/scene_demo.rar)

[在线演示](http://server.ucomm.cn/scene_demo/admin.html)



# ====新增自定义模板接口(联系管理人员开通)==== #



## 获取自定义模板分类 ##
当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/tpl.json`

返回

    {"code":200,"message":"操作成功","list":[{"name":"分类1","id":1},{"name":"分类2","id":2}],"page":{"count":1,"pageNo":1,"pagesize":20}}


## 自定义模板分类添加 ##
当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/tplcaddsave.json`

POST参数

* name：模板分类名称
* orderid：模板分类排序

返回

    {"code":200,"message":"操作成功","list":[{"name":"分类1","id":1},{"name":"分类2","id":2}],"page":{"count":1,"pageNo":1,"pagesize":20}}

## 自定义模板分类修改 ##
当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/tplceditsave.json`

POST参数

* id：模板分类ID
* name：模板分类名称
* orderid：模板分类排序

返回

    {"code":200,"message":"操作成功","list":[{"name":"分类1","id":1},{"name":"分类2","id":2}],"page":{"count":1,"pageNo":1,"pagesize":20}}


## 自定义模板分类删除 ##
当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/tplcdel.json`

GET参数

* id：模板分类ID
返回

    {"code":200,"message":"操作成功"}



## 获取自定义模板列表 ##
当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/tpllist.json`

GET参数

* id：模板分类ID

返回

    {"code":200,"message":"操作成功","list":[{"name":"分类1","id":1},{"name":"分类2","id":2}],"page":{"count":1,"pageNo":1,"pagesize":20}}



## 删除自定义模板 ##
当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/tpldel.json`

POST参数

* id：模板ID

返回

    {"code":200,"message":"操作成功"}




## 添加自定义模板 ##
当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/tpladd.json`

GET参数

* classid：模板分类ID


POST参数

* json：模板JSON数据

返回

    {"code":200,"message":"操作成功"}
 
