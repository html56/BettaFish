# BettaFish 部署信息

## 部署状态

✅ **部署成功！**

## 访问信息

- **Web 界面地址**: https://5000-if0z2czbu23xp179i1yfk-5c9abc12.sg1.manus.computer
- **本地地址**: http://localhost:5000
- **主机**: 0.0.0.0
- **端口**: 5000

## 数据库配置

- **数据库类型**: PostgreSQL
- **主机**: localhost
- **端口**: 5432
- **用户名**: bettafish
- **密码**: bettafish
- **数据库名**: bettafish
- **字符集**: utf8mb4

数据库已成功初始化，所有表和视图已创建完成。

## 已安装的依赖

核心依赖已全部安装：
- Flask + Flask-SocketIO (Web 框架)
- Streamlit (单引擎应用)
- PostgreSQL + asyncpg (数据库)
- Playwright (浏览器自动化)
- OpenAI SDK (LLM 接口)
- Tavily Python (搜索 API)
- Pandas, NumPy (数据处理)
- 其他所有 requirements.txt 中的依赖

## 待配置项

⚠️ **需要配置 LLM API 密钥才能使用完整功能**

系统需要以下 API 密钥（可在 Web 界面的 "LLM 配置" 中填写）：

1. **Insight Agent** (推荐 Kimi)
   - API Key
   - Base URL
   - 模型名称 (如 kimi-k2-0711-preview)

2. **Media Agent** (推荐 Gemini)
   - API Key
   - Base URL
   - 模型名称 (如 gemini-2.5-pro)

3. **Query Agent** (推荐 DeepSeek)
   - API Key
   - Base URL
   - 模型名称 (如 deepseek-reasoner)

4. **Report Agent** (推荐 Gemini)
   - API Key
   - Base URL
   - 模型名称 (如 gemini-2.5-pro)

5. **Forum Host LLM** (推荐 Qwen3)
   - API Key
   - Base URL
   - 模型名称 (如 Qwen/Qwen3-235B-A22B-Instruct-2507)

6. **Keyword Optimizer** (小参数 Qwen3)
   - API Key
   - Base URL
   - 模型名称

7. **搜索工具**
   - Tavily API Key (https://www.tavily.com/)
   - Bocha API Key (https://open.bochaai.com/)

8. **MindSpider Agent** (推荐 Deepseek)
   - API Key
   - Base URL
   - 模型名称 (如 deepseek-chat)

## 如何配置

1. 打开 Web 界面
2. 点击 "LLM 配置" 按钮
3. 填写各个 Agent 的 API 密钥和配置
4. 点击 "保存并启动系统"

或者直接编辑 `/home/ubuntu/BettaFish/.env` 文件，填写对应的环境变量。

## 项目目录

- **项目路径**: `/home/ubuntu/BettaFish`
- **配置文件**: `/home/ubuntu/BettaFish/.env`
- **主应用**: `/home/ubuntu/BettaFish/app.py`
- **日志目录**: `/home/ubuntu/BettaFish/logs`
- **报告目录**: `/home/ubuntu/BettaFish/final_reports`

## 启动命令

```bash
cd /home/ubuntu/BettaFish
python3.11 app.py
```

## 系统架构

BettaFish 是一个多智能体舆情分析系统，包含以下组件：

- **Query Agent**: 国内外新闻广度搜索
- **Media Agent**: 多模态内容分析
- **Insight Agent**: 私有数据库挖掘
- **Report Agent**: 智能报告生成
- **Forum Engine**: Agent 协作论坛
- **MindSpider**: 微博爬虫系统

## 注意事项

1. 系统已启动并运行在后台
2. 数据库已初始化完成
3. 所有依赖已安装（除了 torch 等机器学习库，这些是可选的）
4. 需要配置 LLM API 密钥后才能使用完整的分析功能
5. 可以通过 Web 界面进行配置，配置会自动同步到 .env 文件

## 开发建议

- 项目使用 Python 3.11
- 代码结构清晰，采用模块化设计
- 可以直接修改源码进行定制开发
- 建议先配置好 API 密钥，测试基本功能后再进行二次开发
