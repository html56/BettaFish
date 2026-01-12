# BettaFish 部署日志

## 部署时间
2026-01-10 12:30 - 12:35 EST

## 部署环境
- **操作系统**: Ubuntu 22.04 LTS
- **Python 版本**: 3.11.0rc1
- **数据库**: PostgreSQL 14
- **Web 框架**: Flask 2.3.3

## 部署步骤记录

### 1. 克隆仓库
```bash
gh repo clone html56/BettaFish
```
- **状态**: ✅ 成功
- **仓库大小**: 155.63 MiB
- **文件数量**: 454 个文件

### 2. 环境配置

#### 2.1 安装 PostgreSQL
```bash
sudo apt-get update
sudo apt-get install -y postgresql postgresql-contrib
sudo service postgresql start
```
- **状态**: ✅ 成功
- **版本**: PostgreSQL 14

#### 2.2 安装 Python 依赖
```bash
sudo pip3 install -r requirements.txt
```
- **状态**: ✅ 成功
- **主要依赖包**:
  - Flask 2.3.3
  - Flask-SocketIO 5.3.6
  - Streamlit 1.28.1
  - OpenAI >= 1.3.0
  - SQLAlchemy 2.0.35
  - Playwright 1.45.0
  - Pandas >= 2.0.0
  - 其他 40+ 依赖包

#### 2.3 安装 Playwright 浏览器
```bash
python3.11 -m playwright install chromium
```
- **状态**: ✅ 成功

### 3. 数据库初始化

#### 3.1 创建数据库用户和数据库
```bash
sudo -u postgres psql -c "CREATE USER bettafish WITH PASSWORD 'bettafish';"
sudo -u postgres psql -c "CREATE DATABASE bettafish OWNER bettafish;"
sudo -u postgres psql -c "GRANT ALL PRIVILEGES ON DATABASE bettafish TO bettafish;"
```
- **状态**: ✅ 成功
- **数据库名称**: bettafish
- **用户名**: bettafish
- **密码**: bettafish

#### 3.2 初始化数据表
```bash
cd MindSpider/schema
python3.11 init_database.py
```
- **状态**: ✅ 成功
- **创建表数量**: 26 张表
- **主要表**:
  - daily_topics (每日话题)
  - daily_news (每日新闻)
  - crawling_tasks (爬虫任务)
  - weibo_note (微博内容)
  - weibo_note_comment (微博评论)
  - xhs_note (小红书内容)
  - xhs_note_comment (小红书评论)
  - douyin_aweme (抖音视频)
  - douyin_aweme_comment (抖音评论)
  - bilibili_video (B站视频)
  - bilibili_video_comment (B站评论)
  - kuaishou_video (快手视频)
  - zhihu_content (知乎内容)
  - tieba_note (贴吧帖子)
  - 以及其他创建者信息表

### 4. 应用配置

#### 4.1 创建 .env 配置文件
配置内容包括:
- **数据库配置**:
  - DB_HOST=localhost
  - DB_PORT=5432
  - DB_USER=bettafish
  - DB_PASSWORD=bettafish
  - DB_NAME=bettafish
  - DB_DIALECT=postgresql

- **LLM 配置** (所有 Agent 使用统一配置):
  - API_KEY: 使用环境变量 OPENAI_API_KEY
  - BASE_URL: https://api.openai.com/v1
  - MODEL_NAME: gpt-4.1-mini
  
- **配置的 Agent**:
  - Insight Agent (私有数据库挖掘)
  - Media Agent (多模态内容分析)
  - Query Agent (精准信息搜索)
  - Report Agent (智能报告生成)
  - Forum Host (论坛主持人)
  - Keyword Optimizer (关键词优化)

### 5. 启动应用

#### 5.1 启动 Flask 主应用
```bash
cd /home/ubuntu/BettaFish
nohup python3.11 app.py > logs/flask_app.log 2>&1 &
```
- **状态**: ✅ 成功
- **进程 ID**: 5072
- **监听地址**: 0.0.0.0:5000
- **访问地址**: https://5000-imv1xtb4vg855ho1d2euc-fb887f9e.sg1.manus.computer

#### 5.2 应用状态验证
- HTTP 响应码: 200 ✅
- 进程状态: 运行中 ✅
- 端口监听: 正常 ✅
- Web 界面: 可访问 ✅

## 部署结果

### ✅ 部署成功

所有组件已成功部署并正常运行:

1. **数据库**: PostgreSQL 14 运行正常，26 张表已创建
2. **Flask 应用**: 已启动，监听端口 5000
3. **配置文件**: .env 文件已创建并正确配置
4. **依赖包**: 所有必需的 Python 包已安装
5. **Web 界面**: 可通过浏览器访问

### 访问信息

- **应用 URL**: https://5000-imv1xtb4vg855ho1d2euc-fb887f9e.sg1.manus.computer
- **本地地址**: http://localhost:5000
- **应用名称**: 微舆 (BettaFish)
- **应用描述**: 多智能体舆情分析系统

### 功能模块

应用包含以下功能模块:

1. **Insight Engine**: 私有数据库挖掘
2. **Media Engine**: 多模态内容分析
3. **Query Engine**: 精准信息搜索
4. **Forum Engine**: 智能体论坛协作
5. **Report Engine**: 智能报告生成

### 使用说明

1. 访问应用 URL
2. 首次使用需要在 "LLM 配置" 中确认配置
3. 点击 "保存并启动系统" 启动各个 Engine
4. 在主界面输入分析需求开始使用

### 注意事项

1. **API 密钥**: 当前使用的是沙箱环境的 OPENAI_API_KEY，所有 Agent 都配置为使用 gpt-4.1-mini 模型
2. **数据库**: 数据库已初始化但为空，需要运行爬虫系统 (MindSpider) 来采集数据
3. **爬虫系统**: 如需使用完整功能，需要单独启动 MindSpider 爬虫系统
4. **外部 API**: Tavily 和 Bocha 搜索 API 未配置，但不影响基本功能
5. **机器学习模型**: torch 和 transformers 等大型包未安装，情感分析功能可能受限

### 日志文件

- **Flask 应用日志**: /home/ubuntu/BettaFish/logs/flask_app.log
- **系统日志目录**: /home/ubuntu/BettaFish/logs/

### 进程管理

查看应用进程:
```bash
ps aux | grep "python3.11 app.py"
```

停止应用:
```bash
pkill -f "python3.11 app.py"
```

重启应用:
```bash
cd /home/ubuntu/BettaFish
nohup python3.11 app.py > logs/flask_app.log 2>&1 &
```

### 数据库连接信息

- **主机**: localhost
- **端口**: 5432
- **用户名**: bettafish
- **密码**: bettafish
- **数据库名**: bettafish

连接数据库:
```bash
PGPASSWORD=bettafish psql -h localhost -U bettafish -d bettafish
```

## 后续优化建议

1. **安装机器学习依赖**: 如需使用情感分析功能，需要安装 torch 和 transformers
2. **配置外部搜索 API**: 申请 Tavily 或 Bocha API 密钥以增强搜索能力
3. **运行爬虫系统**: 启动 MindSpider 采集社交媒体数据
4. **优化 LLM 配置**: 根据实际需求为不同 Agent 配置不同的模型
5. **生产环境部署**: 使用 Docker Compose 或 Nginx + Gunicorn 进行生产部署

## 部署完成时间
2026-01-10 12:35 EST
