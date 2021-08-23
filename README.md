<h1 align="center">Fuck163MusicTasks</h1>

<h4 align="center">自动完成网易云音乐人任务并领取云豆</h4>

<p align="center"><strike>说白了就是白嫖网易云年费黑胶</strike></p>

<p align="center">
	<a href="https://goreportcard.com/report/github.com/XiaoMengXinX/Fuck163MusicTasks">
      <img src="https://goreportcard.com/badge/github.com/XiaoMengXinX/Fuck163MusicTasks?style=flat-square">
	</a>
	<a href="https://github.com/XiaoMengXinX/Fuck163MusicTasks/releases">
    <img src="https://img.shields.io/github/v/release/XiaoMengXinX/Fuck163MusicTasks?include_prereleases&style=flat-square">
  </a>
</p>

## ✨ 特性

- web/Android 双平台每日签到
- 音乐人每日签到（登录音乐人中心）
- 自动发布动态（音乐人每日任务）
- 自动回复粉丝评论（音乐人每日任务）
- 自动恢复粉丝私信（音乐人每日任务）
- 自动领取已完成任务的云豆
- ~~自动兑换年费黑胶~~（并没有）

## 🧩 依赖
本项目依赖于 [Binaryify](https://github.com/Binaryify) 的 [网易云音乐API (Binaryify/NeteaseCloudMusicApi)](https://github.com/Binaryify/NeteaseCloudMusicApi)

您可以自建服务，也可以使用 [Binaryify 在 vercel 上的 deployment](https://github.com/Binaryify/NeteaseCloudMusicApi/deployments/) ，个人推荐自建以保证数据安全性

## 📋 配置

请下载并修改项目根目录下的 config_example.json

**请不要直接复制粘贴 README 中的示例配置，如果一定要这样做的话，请确保在解析前移除所有注释。**

```json
{
  "NeteaseAPI": "YOUR_COSTUM_API", // 参建上方的 "依赖", 须填入你想要使用的 网易云音乐API 地址
  "DEBUG": false, // 是否开启 DEBUG, 也可以在命令行参数加 -d 以开启 DEBUG模式
  "Users": [ // 用户配置
    {
      "Cookies": [ // 至少填入一个用户的 MUSIC_U, 支持多用户及多 Cookie
        {
          "key": "MUSIC_U",
          "value": "USER_1_MUSIC_U"
        }
      ]
    },
    {
      "Cookies": [
        {
          "key": "MUSIC_U",
          "value": "USER_2_MUSIC_U"
        }
      ]
    }
  ],
  "EventSendConfig": { // 发送动态配置
    "LagConfig": { // 延时配置
      "RandomLag": true, // 是否开启随机延时
      "LagBetweenSendAndDelete": true, // 是否开启发送动态与删除动态间的延时
      "DefaultLag": 60, // 默认延时，若 RandomLag 为 true, 则忽略此参数
      "LagMin": 30, // 随机延时最小值
      "LagMax": 120 // 随机延时最大值
    }
  },
  "CommentReplyConfig": { // 回复评论配置
    "RepliedComment": [ // 填入你想回复的评论信息, 此处的 Array 对应上面的用户配置
      { // USER_1 的评论配置
        "ID": 123456, // 待回复评论的歌曲ID
        "CommentId": 123456 // 待回复评论的评论ID
      },
      { // USER_2 的评论配置
        "ID": 123456,
        "CommentId": 123456
      }
    ],
    "LagConfig": { // 评论延时设置, 配置项同上
      "RandomLag": true,
      "LagBetweenSendAndDelete": true,
      "DefaultLag": 60,
      "LagMin": 30,
      "LagMax": 120
    }
  },
  "SendMsgConfig": { // 回复私信配置, 此处的 Array 同样对应上面的用户配置
    "UserID": [ // USER_1 的私信配置
      [ // 可填入多个 userID, 程序将会在回复私信时随机选择
        123456, // USER_1 回复私信的用户1号
        233333 // USER_1 回复私信的用户2号
      ],
      [ // USER_2 的私信配置
        123456
      ]
    ],
    "LagConfig": { // 回复私信延迟配置, 配置项同上
      "RandomLag": true,
      "DefaultLag": 10,
      "LagMin": 5,
      "LagMax": 20
    }
  },
  "Content": [ // 发送动态、回复评论、回复私信的文本内容, 须至少填入两条, 程序将会随机选择
    "YOUR_CUSTOM_TEXT_1",
    "YOUR_CUSTOM_TEXT_2"
  ]
}
```

## 📖 快速开始
**※ 请确保你已经阅读了上方的 "配置"，并按说明写好了你自己的配置文件**

**请到 [Release 页](https://github.com/XiaoMengXinX/Fuck163MusicTasks/releases) 下载最新版的构建，并将你的配置文件重命名为 `config.json`，将其与下载的可执行文件放在同一目录**

**在命令行运行 Fuck163MusicTasks**

```
$ ./Fuck163MusicTasks
2021/08/24 00:13:00 [INFO] [用户名] 签到成功，获得 9 经验 (Android) (main.go:227)
2021/08/24 00:13:00 [INFO] [用户名] 签到成功，获得 5 经验 (Android) (main.go:237)
2021/08/24 00:13:00 [INFO] [用户名] 账号当前云豆数: 241 (main.go:368)
2021/08/24 00:13:00 [INFO] [用户名] 获取音乐人任务中... (main.go:369)
2021/08/24 00:13:01 [INFO] [用户名] 任务「登录音乐人中心」任务未完成，已添加到任务列表 (main.go:389)
2021/08/24 00:13:01 [INFO] [用户名] 正在运行自动任务中 (main.go:158)
2021/08/24 00:13:01 [INFO] [用户名] 执行音乐人签到任务中 (main.go:169)
2021/08/24 00:13:01 [INFO] [用户名] 音乐人签到成功 (main.go:175)
2021/08/24 00:13:01 [INFO] [用户名] 所有任务执行完成，正在重新检查并领取云豆 (main.go:209)
2021/08/24 00:13:01 [INFO] [用户名] 账号当前云豆数: 241 (main.go:368)
2021/08/24 00:13:01 [INFO] [用户名] 获取音乐人任务中... (main.go:369)
2021/08/24 00:13:01 [INFO] [用户名] 「登录音乐人中心」任务已完成，正在领取云豆 (main.go:377)
2021/08/24 00:13:01 [INFO] [用户名] 领取「登录音乐人中心」任务云豆成功 (main.go:383)
2021/08/24 00:13:01 [INFO] [用户名] 账号当前云豆数: 242 (main.go:368)
2021/08/24 00:13:01 [INFO] [用户名] 后面的任务，明天再来探索吧！ (main.go:394)
```

#### **进阶操作**：

您可以通过命令行参数修改输入的配置文件目录以及开启 DEBUG 模式，详见：

```
Usage of ./Fuck163MusicTasks:
  -c string
        Config filename (default "config.json")
  -d    DEBUG mode
  -v    Print version
```



## ⚙️ 构建

构建前请确保拥有 `Go 1.16.5`或更高版本

**克隆代码**

```
git clone https://github.com/XiaoMengXinX/Fuck163MusicTasks
```

**使用脚本自动编译 ( 支持 windows 的 bash 环境，例如 git bash )**

```
cd Fuck163MusicTasks
bash build.sh 

# 也可以加入参数以交叉编译，如
bash build.sh linux arm64
```

## 🛠️ 部署

未来会支持 Github Action 部署，待更新...
