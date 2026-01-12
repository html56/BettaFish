# 配置文件更新说明

## 更新时间

2026-01-10 23:18

## 更新内容

已成功将用户提供的配置文件应用到 BettaFish 项目中，并保留了本地数据库配置。

## 数据库配置（已保留本地配置）

| 配置项 | 值 | 说明 |
|--------|-----|------|
| **DB_HOST** | localhost | 使用本地 PostgreSQL |
| **DB_PORT** | 5432 | PostgreSQL 默认端口 |
| **DB_USER** | bettafish | 本地数据库用户 |
| **DB_PASSWORD** | bettafish | 本地数据库密码 |
| **DB_NAME** | bettafish | 数据库名称 |
| **DB_DIALECT** | postgresql | 数据库类型 |

## LLM 配置（已应用用户配置）

所有 Agent 均使用阿里云通义千问模型：

| Agent | API Key | Base URL | 模型名称 |
|-------|---------|----------|----------|
| **Insight Agent** | sk-31825a267e964ebcad39b74c8890e8a9 | https://dashscope.aliyuncs.com/compatible-mode/v1 | qwen-plus |
| **Media Agent** | sk-31825a267e964ebcad39b74c8890e8a9 | https://dashscope.aliyuncs.com/compatible-mode/v1 | qwen-plus |
| **Query Agent** | sk-31825a267e964ebcad39b74c8890e8a9 | https://dashscope.aliyuncs.com/compatible-mode/v1 | qwen-plus |
| **Report Agent** | sk-31825a267e964ebcad39b74c8890e8a9 | https://dashscope.aliyuncs.com/compatible-mode/v1 | qwen-plus |
| **Forum Host** | sk-31825a267e964ebcad39b74c8890e8a9 | https://dashscope.aliyuncs.com/compatible-mode/v1 | qwen-plus |
| **Keyword Optimizer** | sk-31825a267e964ebcad39b74c8890e8a9 | https://dashscope.aliyuncs.com/compatible-mode/v1 | qwen-plus |

## 搜索工具配置

| 工具 | API Key |
|------|---------|
| **Tavily** | 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 |
| **Bocha** | sk-ceb491d95d464690baa58f5b8b4b648d |

## 性能优化配置

为了快速运行，已应用以下优化配置：

| 配置项 | 值 | 说明 |
|--------|-----|------|
| **MAX_REFLECTIONS** | 1 | 最大反思次数 |
| **MAX_SEARCH_RESULTS_FOR_LLM** | 1 | LLM 处理的最大搜索结果数 |
| **DEFAULT_GET_COMMENTS_FOR_TOPIC_LIMIT** | 1 | 获取评论的默认限制 |
| **GENERATION_MODE** | quick | 快速生成模式 |
| **ENABLE_FORUM_DISCUSSION** | False | 禁用论坛讨论 |
| **FORUM_MAX_ROUNDS** | 1 | 论坛最大轮次 |
| **FORUM_HOST_SPEECH_THRESHOLD** | 1 | 论坛主持人发言阈值 |
| **FORUM_MAX_TOTAL_ROUNDS** | 1 | 论坛总最大轮次 |

这些配置可以显著提高系统响应速度，适合快速测试和开发。

## 服务状态

Flask 应用已重启并正常运行：

- **访问地址**: https://5000-if0z2czbu23xp179i1yfk-5c9abc12.sg1.manus.computer
- **本地地址**: http://localhost:5000
- **状态**: 运行中，等待启动系统组件

## Web 界面验证

通过 Web 界面的 "LLM 配置" 窗口可以看到：

**数据库连接**：已正确显示本地 PostgreSQL 配置（localhost:5432，用户 bettafish）。

**Insight Agent**：API Key 和 Base URL 已正确加载，使用阿里云通义千问 qwen-plus 模型。

**Media Agent**：API Key 和 Base URL 已正确加载，使用阿里云通义千问 qwen-plus 模型。

**其他 Agent**：Query Agent、Report Agent、Forum Host、Keyword Optimizer 均已配置完成。

**搜索工具**：Tavily 和 Bocha API Key 已配置。

## 下一步操作

配置已完成，可以直接使用：

1. 在 Web 界面点击 "保存并启动系统" 按钮
2. 等待所有 Agent 初始化完成
3. 在搜索框输入分析需求开始使用

或者直接在搜索框输入内容，系统会自动启动并开始分析。

## 备份信息

原配置文件已备份到：`/home/ubuntu/BettaFish/.env.backup`

如需恢复原配置，可以执行：
```bash
cp /home/ubuntu/BettaFish/.env.backup /home/ubuntu/BettaFish/.env
```

## 配置文件位置

- **当前配置**: `/home/ubuntu/BettaFish/.env`
- **备份配置**: `/home/ubuntu/BettaFish/.env.backup`
- **用户上传**: `/home/ubuntu/upload/pasted_file_58n3Mb_.env`
