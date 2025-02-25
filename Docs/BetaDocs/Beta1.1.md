### easyMirai Api 接口文档

#### 写在前面

使用须知：本项目基于 [Mirai](`https://github.com/mamoe/mirai`) 进行二次开发

此文档为v1.1-Beta版，请及时 [Click here](https://github.com/ExMikuPro/easyMirai) 检查更新！

#### 目录

[写前准备](#写前准备)

[获取插件版本号](#获取插件版本号)

[获取Session](#获取Session)

[绑定Session](#绑定Session)

[获取并绑定session到Bot](#获取并绑定session到Bot)

[获取信息列长度](#获取信息列长度)

[从队列头部获取信息后移除](#从队列头部获取信息后移除)

[从队列部获取信息后不移除](#从队列头部获取信息后不移除)

[从队列尾部获取信息后移除](#从队列尾部获取信息后移除)

[从队列尾部获取信息后不移除](#从队列尾部获取信息后不移除)

[发送好友消息](#发送好友消息)

[发送群聊消息](#发送群聊消息)

[禁言群成员](#禁言群成员)

[解除群成员禁言](#解除群成员禁言)

[禁言群全体成员](#禁言群全体成员)

[解除群全体成员禁言](#解除群全体成员禁言)

[移除群成员](#移除群成员)

[主动退出群聊](#主动退出群聊)

[撤回消息](#撤回消息)

[上传图片文件](#上传图片文件)

[上传语音文件](#上传语音文件)

#### 写前准备

easyMirai需要调用requests库进行数据的获取

在使用前请先确定requests库是否进行安装

如果没有请执行以下代码进行安装

    pip install requests

调用easyMirai.py

```python

from Package import easyMirai
```

实例化函数输入

```python
mirai = easyMirai.Mirai(host, port, Key, Qid, count, debug, times)
```

| 变量名   | 输入类型 | 可选性 | 备注              | 默认值   |
|-------|------|-----|-----------------|-------|
| host  | str  | 不可选 | BotIP地址         | 无     |
| port  | str  | 不可选 | Bot端口号          | 无     |
| key   | str  | 不可选 | Bot通信verify key | 无     |
| qid   | str  | 不可选 | Bot登录的ID号       | 无     |
| count | str  | 可选  | 单次信息获取条数        | "1"   |
| debug | bool | 可选  | 调试开关，信息输出到控制台   | False |
| times | int  | 可选  | 获取信息等待时间        | 1     |

#### 获取插件版本号

变量方法：

```python
mirai.version()
```

| 类型   | 输入参数 | 输入参数类型 | 输出参数类型 | 备注                    |
|------|------|--------|--------|-----------------------|
| 初始化类 | 无    | 无      | dict   | 获取mirai-api-http模块版本号 |

响应值：

```json

{
  "version": "v1-HTTP.0.0"
}

```

#### 获取Session

```python
mirai.getSession()
```

| 类型   | 输入参数 | 输入参数类型 | 输出参数类型 | 备注         |
|------|------|--------|--------|------------|
| 初始化类 | 无    | 无      | dict   | 获取session码 |

响应值：

```json
{
  "code": 0,
  "session": "UnVerifiedSession"
}
```

#### 绑定Session

变量方法：

```python
mirai.bindSession()
```

| 类型   | 输入参数 | 输入参数类型 | 输出参数类型 | 备注               |
|------|------|--------|--------|------------------|
| 初始化类 | 无    | 无      | dict   | 将session与Bot进行绑定 |

响应值：

```json
{
  "code": 0,
  "msg": "success"
}
```

#### 获取并绑定session到Bot

变量方法：

```python
mirai.begin()
```

| 类型   | 输入参数 | 输入参数类型 | 输出参数类型 | 备注                        |
|------|------|--------|--------|---------------------------|
| 初始化类 | 无    | 无      | 控制台    | 获取session并绑定Bot，此函数为前两者结合 |

#### 获取信息列长度

变量方法：

```python
mirai.getCountMessage()
```

| 类型    | 输入参数 | 输入参数类型 | 输出参数类型 | 备注        |
|-------|------|--------|--------|-----------|
| 信息获取类 | 无    | 无      | dict   | 获取消息队列总长度 |

响应值：

```json
{
  "code": 0,
  "msg": "",
  "data": 1024
}
```

#### 从队列头部获取信息后不移除

变量方法：

```python
mirai.getFetchMessage()
```

| 类型    | 输入参数 | 输入参数类型 | 输出参数类型 | 备注                     |
|-------|------|--------|--------|------------------------|
| 信息获取类 | 无    | 无      | dict   | 获取队列头部消息后移除，即按时间顺序获取消息 |

响应值：

```json
{
  "type": "FriendMessage",
  "sender": {
    "id": 123,
    "nickname": "",
    "remark": ""
  },
  "messageChain": []
}
```

#### 从队列头部获取信息后移除

变量方法：

```python
mirai.getPeekMessage()
```

| 类型    | 输入参数 | 输入参数类型 | 输出参数类型 | 备注                      |
|-------|------|--------|--------|-------------------------|
| 信息获取类 | 无    | 无      | dict   | 获取队列头部消息后不移除，即按时间顺序获取消息 |

响应值：

```json
{
  "type": "FriendMessage",
  "sender": {
    "id": 123,
    "nickname": "",
    "remark": ""
  },
  "messageChain": []
}
```

#### 从队列尾部获取信息后移除

变量方法：

```python
mirai.getPeekMessage()
```

| 类型    | 输入参数 | 输入参数类型 | 输出参数类型 | 备注                      |
|-------|------|--------|--------|-------------------------|
| 信息获取类 | 无    | 无      | dict   | 获取队列头部消息后不移除，即按最新消息顺序获取 |

响应值：

```json
{
  "type": "FriendMessage",
  "sender": {
    "id": 123,
    "nickname": "",
    "remark": ""
  },
  "messageChain": []
}
```

#### 从队列尾部获取信息后移除

变量方法：

```python
mirai.getPeekMessage()
```

| 类型    | 输入参数 | 输入参数类型 | 输出参数类型 | 备注                     |
|-------|------|--------|--------|------------------------|
| 信息获取类 | 无    | 无      | dict   | 获取队列头部消息后移除，即按最新消息顺序获取 |

响应值：

```json
{
  "type": "FriendMessage",
  "sender": {
    "id": 123,
    "nickname": "",
    "remark": ""
  },
  "messageChain": []
}
```

#### 从队列尾部获取信息后不移除

变量方法：

```python
mirai.getPeekMessage()
```

| 类型    | 输入参数 | 输入参数类型 | 输出参数类型 | 备注                      |
|-------|------|--------|--------|-------------------------|
| 信息获取类 | 无    | 无      | dict   | 获取队列头部消息后不移除，即按最新消息顺序获取 |

响应值：

```json
{
  "type": "FriendMessage",
  "sender": {
    "id": 123,
    "nickname": "",
    "remark": ""
  },
  "messageChain": []
}
```

#### 发送好友消息

变量方法：

```python
mirai.sendFriendMessage()
```

| 类型    | 输入参数    | 输入参数类型   | 输出参数类型 | 备注       |
|-------|---------|----------|--------|----------|
| 信息发送类 | msg，tar | dict，str | 无      | 发送好友普通消息 |

输入参数：

| 参数  | 输入类型 | 实例参数      | 备注    |
|-----|------|-----------|-------|
| msg | dict | 见下 _输入格式_ | 信息列   |
| tar | str  | "121324"  | 目标QQ号 |

输入格式：

```python
msg = {"type": "Plain", "text": "发送的文字"}  # 发送文字
msg = {"type": "Image", "url": "https://this.com/this.png"}  # 发送图片
```

#### 发送群聊消息

变量方法：

```python
mirai.sendGroupMessage()
```

| 类型     | 输入参数    | 输入参数类型   | 输出参数类型 | 备注       |
|--------|---------|----------|--------|----------|
| 群事件处理类 | msg，tar | dict，str | 无      | 发送群聊普通消息 |

输入参数：

| 参数  | 输入类型 | 实例参数      | 备注    |
|-----|------|-----------|-------|
| msg | dict | 见下 _输入格式_ | 信息列   |ß
| tar | str  | "121324"  | 目标Q群号 |

输入格式：

```python
msg = {"type": "Plain", "text": "发送的文字"}  # 发送文字
msg = {"type": "Image", "url": "https://this.com/this.png"}  # 发送图片
```

#### 禁言群成员

变量方法：

```python
mirai.muteMember()
```

| 类型     | 输入参数                  | 输入参数类型      | 输出参数类型 | 备注            |
|--------|-----------------------|-------------|--------|---------------|
| 群事件处理类 | target，memberId，times | str，str，str | 无      | 禁言指定群成员(需要权限) |

输入参数：

| 参数       | 输入类型 | 实例参数       | 备注               |
|----------|------|------------|------------------|
| target   | str  | "12345678" | 目标群号             |
| memberId | str  | "121324"   | 目标成员QQ号          |
| times    | str  | "121324"   | 设置禁言时间单位为秒，最多30天 |

#### 解除群成员禁言

变量方法：

```python
mirai.unMuteMember()
```

| 类型     | 输入参数            | 输入参数类型  | 输出参数类型 | 备注            |
|--------|-----------------|---------|--------|---------------|
| 群事件处理类 | target，memberId | str，str | 无      | 解除群成员禁言(需要权限) |

输入参数：

| 参数       | 输入类型 | 实例参数       | 备注               |
|----------|------|------------|------------------|
| target   | str  | "12345678" | 目标群号             |
| memberId | str  | "121324"   | 目标成员QQ号          |

#### 禁言群全体成员

变量方法：

```python
mirai.muteAll()
```

| 类型     | 输入参数   | 输入参数类型 | 输出参数类型 | 备注            |
|--------|--------|--------|--------|---------------|
| 群事件处理类 | target | str    | 无      | 禁言群全体成员(需要权限) |

输入参数：

| 参数       | 输入类型 | 实例参数       | 备注               |
|----------|------|------------|------------------|
| target   | str  | "12345678" | 目标群号             |

#### 解除群全体成员禁言

变量方法：

```python
mirai.unMuteAll()
```

| 类型     | 输入参数   | 输入参数类型 | 输出参数类型 | 备注              |
|--------|--------|--------|--------|-----------------|
| 群事件处理类 | target | str    | 无      | 解除群全体成员禁言(需要权限) |

输入参数：

| 参数       | 输入类型 | 实例参数       | 备注               |
|----------|------|------------|------------------|
| target   | str  | "12345678" | 目标群号             |

#### 移除群成员

```python
mirai.kick()
```

| 类型     | 输入参数            | 输入参数类型  | 输出参数类型 | 备注            |
|--------|-----------------|---------|--------|---------------|
| 群事件处理类 | target，memberId | str，str | 无      | 解除群成员禁言(需要权限) |

输入参数：

| 参数       | 输入类型 | 实例参数       | 备注      |
|----------|------|------------|---------|
| target   | str  | "12345678" | 目标群号    |
| memberId | str  | "121324"   | 目标成员QQ号 |
| msg      | str  | "您已被移出群聊"  | 信息      |

#### 主动退出群聊

```python
mirai.quitGroup()
```

| 类型     | 输入参数   | 输入参数类型 | 输出参数类型 | 备注          |
|--------|--------|--------|--------|-------------|
| 群事件处理类 | target | str    | 无      | Bot主动退出指定群聊 |

输入参数：

| 参数       | 输入类型 | 实例参数       | 备注      |
|----------|------|------------|---------|
| target   | str  | "12345678" | 目标群号    |

#### 撤回消息

变量方法：

```python
mirai.reCall()
```

| 类型    | 输入参数 | 输入参数类型 | 输出参数类型 | 备注   |
|-------|------|--------|--------|------|
| 信息操作类 | tar  | str    | 无      | 撤回信息 |

输入参数：

| 参数  | 输入类型 | 实例参数      | 备注     |
|-----|------|-----------|--------|
| tar | str  | "121324"  | 目标消息编号 |

#### 上传图片文件

变量方法：

```python
mirai.uploadVoice()
```

| 类型    | 输入参数        | 输入参数类型  | 输出参数类型 | 备注     |
|-------|-------------|---------|--------|--------|
| 文件操作类 | types，files | str，str | dict   | 上传图片文件 |

输入参数：

| 参数    | 输入类型 | 实例参数         | 备注                          |
|-------|------|--------------|-----------------------------|
| types | str  | "friend"     | "friend" 或 "group" 或 "temp" |
| files | str  | "./this.png" | 目标文件名                       |

响应值：

```json
{
  "imageId": "{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}.mirai",
  "url": "https://example.com/example.example"
}
```

#### 上传语音文件

变量方法：

```python
mirai.sendGroupMessage()
```

| 类型    | 输入参数        | 输入参数类型  | 输出参数类型 | 备注     |
|-------|-------------|---------|--------|--------|
| 文件操作类 | types，files | str，str | dict   | 上传图片文件 |

输入参数：

| 参数    | 输入类型 | 实例参数         | 备注                          |
|-------|------|--------------|-----------------------------|
| types | str  | "friend"     | "friend" 或 "group" 或 "temp" |
| files | str  | "./this.png" | 目标文件名                       |

响应值：

```json
{
  "imageId": "{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}.mirai",
  "url": "https://example.com/example.example"
}
```

# 未完待续！

 

