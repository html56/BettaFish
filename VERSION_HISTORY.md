# BettaFish 版本历史记录

## 版本管理说明

本文档记录所有重要版本的提交 ID，方便快速回滚。

---

## ✅ 稳定版本（推荐使用）

### v1.1.5 - 布局比例优化版（当前版本）

**Git 标签**：`v1.1.5-layout-fix`  
**提交 ID**：`81249d8`  
**提交信息**：style: 调整左右布局比例，左侧 71% 右侧 29%，更接近参考设计  
**提交时间**：2026-01-11  
**状态**：✅ 稳定，已验证

**功能特点**：
- ✅ 调整左右布局比例，左侧分析结果区域占 71%，右侧控制台占 29%
- ✅ 更接近参考设计的视觉效果，左侧内容区域更宽敞
- ✅ 保留所有之前的优化和修复

**回滚命令**：
```bash
cd /home/ubuntu/BettaFish
git reset --hard v1.1.5-layout-fix
git push -f origin main
```

---

### v1.1.4 - 消息提示修复版

**Git 标签**：`v1.1.4-message-fix`  
**提交 ID**：`f06c175`  
**提交信息**：fix: 添加消息提示样式，修复搜索按钮无响应问题  
**提交时间**：2026-01-11  
**状态**：✅ 稳定，已验证

**功能特点**：
- ✅ 添加消息提示样式，修复搜索按钮无响应问题
- ✅ 添加 `.message` 元素的 CSS 样式（success/error/info/warning）
- ✅ 移除 message 元素的 inline style，让 CSS 控制显示
- ✅ 现在点击搜索按钮时会显示清晰的错误提示
- ✅ 用户可以看到"没有运行中的应用，无法执行搜索"等提示
- ✅ 消息提示会在 3 秒后自动消失
- ✅ 保留所有之前的优化和修复

**回滚命令**：
```bash
cd /home/ubuntu/BettaFish
git reset --hard v1.1.4-message-fix
# 重启 Flask 应用
```

---

### v1.1.3 - 状态指示灯持续显示修复版

**Git 标签**：`v1.1.3-status-fix`  
**提交 ID**：`8dc9b1c`  
**提交信息**：fix: 修复 updateAppStatus 函数中的类名错误，确保状态指示灯持续显示  
**提交时间**：2026-01-11  
**状态**：✅ 稳定，已验证

**功能特点**：
- ✅ 修复状态指示灯在 WebSocket 更新后消失的问题
- ✅ 修正 JavaScript 中的类名错误（status-indicator → system-status-indicator）
- ✅ 状态指示灯现在会持续显示，不会在刷新或状态更新后消失
- ✅ 所有 Engine 的状态都能正确显示（红色=停止，绿色=运行，黄色=启动中）
- ✅ 保留所有现代化界面设计和之前的所有优化
- ✅ 所有功能正常工作

**回滚命令**：
```bash
cd /home/ubuntu/BettaFish
git reset --hard v1.1.3-status-fix
# 重启 Flask 应用
```

---

### v1.1.2 - 状态指示灯修复版

**Git 标签**：`v1.1.2-status-indicator`  
**提交 ID**：`622484c`  
**提交信息**：fix: 修复状态指示灯显示问题，增大尺寸并添加阴影效果  
**提交时间**：2026-01-11  
**状态**：⚠️ 部分问题（指示灯会消失）

**功能特点**：
- ✅ 修复标签页上的状态指示灯显示问题
- ✅ 将标签按钮改为 flex 布局，正确显示指示灯和文字
- ✅ 增大指示灯尺寸从 6px 到 10px，更加醒目
- ✅ 为指示灯添加阴影效果，增强视觉层次
- ⚠️ 指示灯在 WebSocket 更新后会消失（已在 v1.1.3 修复）

**回滚命令**：
```bash
cd /home/ubuntu/BettaFish
git reset --hard v1.1.2-status-indicator
# 重启 Flask 应用
```

---

### v1.1.1 - 配置弹窗修复版

**Git 标签**：`v1.1.1-config-fix`  
**提交 ID**：`8008d03`  
**提交信息**：fix: 修复配置弹窗布局问题并美化样式  
**提交时间**：2026-01-11  
**状态**：✅ 稳定，已验证

**功能特点**：
- ✅ 修复配置弹窗布局显示错乱问题
- ✅ 配置字段改为单列垂直布局，清晰易读
- ✅ 添加完整的配置弹窗样式（头部、底部、按钮）
- ✅ 优化配置表单的间距和字体
- ✅ 保留现代化界面设计的所有优点
- ✅ 所有功能正常工作

**回滚命令**：
```bash
cd /home/ubuntu/BettaFish
git reset --hard v1.1.1-config-fix
# 重启 Flask 应用
```

---

### v1.1.0 - 现代化界面设计

**Git 标签**：`v1.1.0-modern-ui`  
**提交 ID**：`227b9e0`  
**提交信息**：feat: 升级前端界面为现代化 macOS 风格设计  
**提交时间**：2026-01-10  
**状态**：⚠️ 部分问题（配置弹窗布局错乱）

**功能特点**：
- ✅ 现代化 macOS 风格界面
- ✅ 简洁的灰白色调主题
- ✅ 卡片式布局设计
- ✅ 流畅的动画效果
- ⚠️ 配置弹窗布局有问题（已在 v1.1.1 修复）

---

### v1.0 - 原始稳定版本

**Git 标签**：`v1.0-stable`  
**提交 ID**：`f7ee164`  
**提交信息**：feat: 升级前端界面为现代科技风格  
**提交时间**：2026-01-10  
**状态**：✅ 稳定，已验证

**功能特点**：
- ✅ 界面布局正常，所有功能正常工作
- ✅ 配置弹窗正常显示，表单元素排列整齐
- ✅ 应用了现代科技风格（毛玻璃效果、渐变色）
- ✅ 保留了原有的所有功能

**回滚命令**：
```bash
cd /home/ubuntu/BettaFish
git reset --hard v1.0-stable
# 重启 Flask 应用
```

---

## 📊 版本对比

| 版本 | 提交 ID / 标签 | 状态 | 界面 | 功能 | 推荐 |
|------|---------------|------|------|------|------|
| **v1.1.4** | `f06c175` / `v1.1.4-message-fix` | ✅ 稳定 | ✅ 完美 | ✅ 正常 | ⭐⭐⭐⭐⭐ |
| v1.1.3 | `8dc9b1c` / `v1.1.3-status-fix` | ✅ 稳定 | ⚠️ 消息提示不显示 | ✅ 正常 | ⭐⭐⭐⭐ |
| v1.1.2 | `622484c` / `v1.1.2-status-indicator` | ⚠️ 部分问题 | ⚠️ 指示灯会消失 | ✅ 正常 | ⭐⭐⭐ |
| v1.1.1 | `8008d03` / `v1.1.1-config-fix` | ✅ 稳定 | ⚠️ 指示灯不显示 | ✅ 正常 | ⭐⭐⭐ |
| v1.1.0 | `227b9e0` / `v1.1.0-modern-ui` | ⚠️ 部分问题 | ⚠️ 配置弹窗有问题 | ✅ 正常 | ⭐⭐ |
| v1.0 | `f7ee164` / `v1.0-stable` | ✅ 稳定 | ✅ 正常 | ✅ 正常 | ⭐⭐⭐⭐ |

---

## 🏷️ Git 标签列表

```bash
# 查看所有标签
git tag -l

# 输出：
# v1.0-stable
# v1.1.0-modern-ui
# v1.1.1-config-fix
# v1.1.2-status-indicator
# v1.1.3-status-fix
# v1.1.4-message-fix
```

### 使用标签回滚

```bash
# 回滚到最新稳定版本
git reset --hard v1.1.4-message-fix

# 回滚到状态指示灯持续显示版本
git reset --hard v1.1.3-status-fix

# 回滚到状态指示灯修复版本（指示灯会消失）
git reset --hard v1.1.2-status-indicator

# 回滚到配置弹窗修复版本（指示灯不显示）
git reset --hard v1.1.1-config-fix

# 回滚到现代化界面版本（配置弹窗有问题）
git reset --hard v1.1.0-modern-ui

# 回滚到原始稳定版本
git reset --hard v1.0-stable
```

---

## 🔄 快速回滚指南

### 回滚到最新稳定版本 v1.1.4

```bash
# 1. 进入项目目录
cd /home/ubuntu/BettaFish

# 2. 回滚到最新稳定版本
git reset --hard v1.1.4-message-fix

# 3. 停止当前 Flask 应用
ps aux | grep "python3.11 app.py" | grep -v grep | awk '{print $2}' | xargs kill

# 4. 重启 Flask 应用
cd /home/ubuntu/BettaFish && nohup python3.11 app.py > /dev/null 2>&1 &

# 5. 强制推送到 GitHub（如果需要）
git push origin main --force
```

### 验证回滚是否成功

1. 访问 Web 界面
2. 检查主界面是否正常显示
3. 点击"配置"按钮，检查配置弹窗是否正常
4. 检查状态指示灯是否显示
5. 输入关键词点击搜索，检查消息提示是否显示

---

## 🚀 当前推荐配置

**推荐版本**：v1.1.4-message-fix (f06c175)  
**推荐分支**：main  
**推荐 CSS**：static/modern_style_new.css  
**推荐 HTML**：templates/index.html

**版本特点**：
- 现代化 macOS 风格界面
- 配置弹窗布局完美
- 状态指示灯持续显示
- 消息提示正常工作
- 所有功能正常工作
- 最佳用户体验

---

**文档维护者**：Manus AI  
**最后更新**：2026-01-11  
**当前稳定版本**：v1.1.4-message-fix (f06c175)
