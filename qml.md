## QML

####  插件的使用
```
编译dll debug/release要对应
以module名在目的程序建立文件夹 
写qmldir
module QmlVlc
plugin QmlVlcPlugin
```

#### 各种问题

## 显示不出来
没有设置height/width

## anchors.topMargin
 没有设置anchors.top
 
 ## Json/Model
 model能放到var里面当object用 但不等同于一个json 调试看数据很多 有时候JSON.stringify 会失败
 
 ## Json undefined
json object赋值 不能逐个赋值 要={}赋值
                    //jsLogin.avatar = "qrc:/uh.png"
                    //jsLogin.username = "敌军还有30秒到达葬场"
                    //jsLogin.userid = "923834"
                    jsLogin = {"avatar":"qrc:/uh.png","username":"敌军还有30秒到达葬场","userid":"923834"}
                    console.log("jsLogin", JSON.stringify(jsLogin))
看w3school 用 var jsObj = new Object();  也行 ， 抽空试一下 					
					
## 编译无法链接外部符号
重新生成
import 路件不对

## 绑定关系不生效
一般是绑定关系被破坏了，=赋值了

## 性能优化
项目-Run-Environment-批量编辑
QSG_VISUALIZE=overdraw
颜色相关说明同一批次渲染
超出立方体部分会浪费顶点着色器