 # 域名需要经过授权后才能操作以下接口 #

## 获取优通UID 与工作人员联系 ##

## 获取优通KEY 与工作人员联系 ##

## **获取通信TOKEN** ##

每个页面对应一个TOKEN，TOKEN是固定的可以保存到本地。请不要频繁获取TOKEN

当前页面GET请求目标  
> `http://server.ucomm.cn/scene/优通UID/优通KEY/token.json`

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

POST可选参数

* keyword：名称关键字
* page：当前页码
* category：类别ID
* mint:商户自定义数字字段
* mtext:商户自定义文本字段

返回

    {"code":200,"message":"操作成功","list":[{"name":"新品推广","description":"欢迎使用本产品","picture":"http://7xizfo.com1.z0.glb.clouddn.com/no_img.png","creationtime":"2015/5/19 22:10:15","updatetime":"2015/5/19 22:10:15","file":"fsd","mint":3,"mtext":"","browse":0,"share":0,"tel":0,"copyright":"0"},{"name":"我的场景","description":"这是我的第一个测试","picture":"http://7xizfo.com1.z0.glb.clouddn.com/no_img.png","creationtime":"2015/5/19 21:46:10","updatetime":"2015/5/19 21:46:10","file":"adg","mint":null,"mtext":null,"browse":0,"share":0,"tel":0,"copyright":"0"}],"page":{"count":1,"pageNo":1,"pagesize":20}}

## 去版权 ##

当前页面POST请求目标
> `http://server.ucomm.cn/scene/优通UID/优通KEY/通信TOKEN/copyright.json`

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
    </script>
    <script src="http://server.ucomm.cn/uem/scene.min.js"></script>
    <div id="ume_load"><div class="divam"></div>拼命加载中...</div>
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


[下载演示](http://server.ucomm.cn/scene_demo.rar)

[在线演示](http://server.ucomm.cn/scene_demo/admin.html)
