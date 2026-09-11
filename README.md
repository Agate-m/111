
#### 1、 获取roomid（图书馆id）和seatid（座位号）

在进入预约图书馆列表界面时断开网络，点击你想预约的图书馆的`选座`按钮，会提示网页无法打开，此时点击`右上角的三条杠`，选择`复制链接`，会得到类似这样的链接：

> https://office.chaoxing.com/front/apps/seat/select?id=5483&day=2023-10-12&backLevel=2&pageToken=0f46f3acc7be4c60862cb9815870ddfd

其中的`id=5483`的5483即为对应图书馆的id，将其填写到config.json中，座位联网后自己挑即可。

1.**fork该仓库**

2.**修改config.json**：这个仿照之前的方式进行修改即可，但是注意，username和password请留空或者随便填以防止泄漏个人账号密码。（具体的需要填写在自己repo的settings中）。时间什么也是需要修改（修改到仓库中）不要忘记。

3.**配置账号密码**：在settings->secrets and variables->Repository secrets 创建两个secret keys。名称分别为USERNAMES，PASSWORDS，填写自己的账号和密码即可。（如果有多个用户，请使用,(英文逗号)隔开，如果密码中有逗号可能会出现问题）。

```
xxxxxxx,xxxxxxx
```

2、**运行action**：在action -> auto_reserve -> run workflows 选择默认分支即可。

## config配置
之后编辑config.json并填写座位预约相关信息即可
```json
{
    "reserve": [
        {"username": "XXXXXXXX", //https://passport2.chaoxing.com/mlogin?loginType=1&newversion=true&fid=&  在这个网站查看是否可以顺利登陆 
        "password": "XXXXXXXX",
        "time": ["08:00","22:00"], // 预约的起始时间
        "roomid":"2609", //2609:四楼外圈,5483:四楼内圈,2610:五楼外圈,5484:五楼内圈
        "seatid":"002", // 注意要用0补全至3位数，例如6号座位应该填006
        "daysofweek": ["Monday" , "Tuesday", "Wednesday", "Thursday", "Friday"]
        },
        {"username": "xxxxxxxxxx",
        "password": "xxxxxxxxx",
        "time": ["20:00","21:00"],
        "roomid":"5483",
        "seatid":["056"],
        "daysofweek": ["Saturday" , "Sunday"]
    }
}
```

### 无法预约情况debug方式
> 1、电脑端访问："https://passport2.chaoxing.com/mlogin?loginType=1&newversion=true&fid=" 使用自己的用户名密码登录
> 2、电脑端访问："https://office.chaoxing.com/front/third/apps/seat/code?id={图书馆id}&seatNum={座位id}" 查看是否显示时间表
> 3、尝试预约看看是否会出现验证方式

目前无法实现跨单位座位预约。
