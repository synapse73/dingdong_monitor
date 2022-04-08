## maicai.ddxq.tools
特别感谢原作者@6r6，让我今天买到肉！！

**Checker.sh**

| 描述  |
| ------------ |
| 每隔一段时间检查今天是否有可配送时段，有则推送到手机  |

**MacOS+iOS使用（亲测好用）**

for barkID:
IOS手机请安装[Bark](https://apps.apple.com/cn/app/bark-%E7%BB%99%E4%BD%A0%E7%9A%84%E6%89%8B%E6%9C%BA%E5%8F%91%E6%8E%A8%E9%80%81/id1403753865)推送工具

Customed Notification Content https://api.day.app/xxxxxxxx/Customed
“xxxxxxxxxx”就是你的barkID
 
 
for CURL:
我目前试下来最方便的方法是，电脑上下载proxyman之类的抓包软件，在电脑端微信打开叮咚小程序，登录一个自己不常用的手机号
（我怕用大号有危险，不过目前没遇到），然后填自己的地址，加入购物车一样东西，试图结算，选时间。
在抓包软件里 找到开头是 https://maicai.api.ddxq.mobi/order/getMultiReserveTime 这条，导出cURL，结果会非常长，填充到sh文件里
(如果不够长，一定没找对）
(记得打开enable https）

```bash
# 在MacOS终端运行如下命令
brew install curl
brew install jq
# 修改checker.sh内容,填充cURL和BarkID
bash checker.sh
# 遇到“人多”的错误会停止，所以我后来跑的是：
while :; do sh checker.sh; done
```
---

**CentOS 服务器+iOS使用**
```shell
yum install screen
yum install jq
wget https://raw.githubusercontent.com/6r6/maicai.ddxq.tools/main/checker.sh
# 修改checker.sh内容，将抓包获得的项目、BarkID填充至对应位置
# BarkID在安装应用、注册设备后获得 示例：https://api.day.app/这里是BarkID/
# 挂载后台运行，避免会话关闭任务停止
screen -S shopping 
bash checker.sh
# 查看后台会话
screen -r shopping
```
