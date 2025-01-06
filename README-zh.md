# ZerePy

ZerePy 是一个开源的 Python 框架，旨在让您在 X 上部署自己的Agent，支持 OpenAI、Anthropic 和 EternalAI 大语言模型。



ZerePy is built from a modularized version of the Zerebro backend. With ZerePy, you can launch your own agent with
similar core functionality as Zerebro. For creative outputs, you'll need to fine-tune your own model.

ZerePy 是基于 Zerebro 后端的模块化版本开发的。通过 ZerePy，你可以启动拥有类似 Zerebro 的核心功能的Agent。如果你需要做一些创造性输出，你会需要自行微调模型。

## 特征

- 用于管理代理的命令行界面（CLI）
- 集成了 Twitter/X
- 集成了 Farcaster
- 集成了 Echochambers
- 支持 OpenAI/Anthropic/EternalAI LLM
- 模块化连接系统

## 快速开始

使用 ZerePy 的最快方式是通过我们的 Replit 模板:

https://replit.com/@blormdev/ZerePy?v=1

1. Fork 这个模版 (需要有Replit账户)
2. 点击顶部的运行按钮
3. 完成！CLI 应该已准备好使用，你可以跳转到配置部分

## 要求

系统:

- Python 3.10 或者更高版本 (3.10 和 3.11 最适合初学者)
- Poetry 1.5 或更高版本

API 密钥:

- LLM: 创建账户并获取一个 API 密钥（至少一个）
  - OpenAI: https://platform.openai.com/api-keys
  - Anthropic: https://console.anthropic.com/account/keys
  - EternalAI: https://eternalai.oerg/api
- 社交平台（根据需求选择:
  - X API: https://developer.x.com/en/docs/authentication/oauth-1-0a/api-key-and-secret
  - Farcaster: Warpcast 恢复短语
  - Echochambers: API 密钥和端口

## 安装

1. 如果您还没有安装 Poetry（依赖管理工具），请首先安装：

这里有官方安装指南：https://python-poetry.org/docs/#installing-with-the-official-installer

2. 克隆仓库:

```bash
git clone https://github.com/blorm-network/ZerePy.git
```

3. 进入 `zerepy` 目录:

```bash
cd zerepy
```

4. 安装依赖:

```bash
poetry install --no-root
```

这将创建一个虚拟环境并安装所有所需的依赖.

## 使用方法

1. 激活虚拟环境:

```bash
poetry shell
```

2. 运行应用程序:

```bash
poetry run python main.py
```

## 配置连接并启动agent

1. 配置所需的连接:

   ```
   configure-connection twitter    # For Twitter/X integration
   configure-connection openai     # For OpenAI
   configure-connection anthropic  # For Anthropic
   configure-connection farcaster  # For Farcaster
   configure-connection eternalai  # For EternalAI
   ```

2. 使用 `list-connections` 查看所有可用连接及其状态

3. 加载 Agent (通常默认加载一个Agent, 可以通过 CLI 或在 agents/general.json):

   ```
   load-agent example
   ```

4. 启动 agent:
   ```
   start
   ```

## 平台特性

### Twitter/X

- 根据prompts发送推文
- 阅读timeline， 支持可配置数量
- 回复timeline中的推文
- 喜欢timeline中的推文

### Farcaster

- 发布内容
- 回复内容
- 喜欢并转发内容
- 阅读timeline
- 获取内容的回复


### Echochambers

- 向聊天室发送新消息
- 根据聊天室上下文回复消息
- 阅读聊天室历史
- 获取聊天室信息和话题

## 创建你的agent

要使agent输出更好，关键是尽可能提供详细的配置文件。为agent构建一个故事和上下文，并选择一些优秀的推文示例进行包含。

如果您想更进一步，您可以微调您自己的模型: https://platform.openai.com/docs/guides/fine-tuning.

在 `agents` 目录中创建一个新的 JSON 文件，按照以下结构进行配置:

```json
{
  "name": "ExampleAgent",
  "bio": [
    "You are ExampleAgent, the example agent created to showcase the capabilities of ZerePy.",
    "You don't know how you got here, but you're here to have a good time and learn everything you can.",
    "You are naturally curious, and ask a lot of questions."
  ],
  "traits": ["Curious", "Creative", "Innovative", "Funny"],
  "examples": ["This is an example tweet.", "This is another example tweet."],
  "loop_delay": 900,
  "config": [
    {
      "name": "twitter",
      "timeline_read_count": 10,
      "own_tweet_replies_count": 2,
      "tweet_interval": 5400
    },
    {
      "name": "farcaster",
      "timeline_read_count": 10,
      "cast_interval": 60
    },
    {
      "name": "openai",
      "model": "gpt-3.5-turbo"
    },
    {
      "name": "anthropic",
      "model": "claude-3-5-sonnet-20241022"
    }
  ],
  "tasks": [
    { "name": "post-tweet", "weight": 1 },
    { "name": "reply-to-tweet", "weight": 1 },
    { "name": "like-tweet", "weight": 1 }
  ]
}
```

## 可用命令

在 CLI 中使用 help 查看所有可用命令。常用命令包括:

- `list-agents`: 显示可用 agent
- `load-agent`: 加载特定 agent
- `agent-loop`: 启动自主行为
- `agent-action`: 执行单个动作
- `list-connections`: 显示可用连接
- `list-actions`: 显示连接的可用动作
- `configure-connection`: 设置新的连接
- `chat`: 与agent开始互动聊天
