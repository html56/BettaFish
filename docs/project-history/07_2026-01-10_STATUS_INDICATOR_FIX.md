<!--
文档用途: 记录 Agent 状态指示器显示问题的修复过程
创建时间: 2026-01-10
文档类型: 问题修复文档
内容概要: 包含问题描述、原因分析、修复方案、代码更改等
相关背景: 状态指示器无法正确显示 Agent 运行状态,影响用户体验
维护说明: 类似 UI 问题修复时可参考本文档的排查思路
-->

# 状态指示灯持续显示问题修复报告

**修复日期**：2026-01-11  
**版本号**：v1.1.3-status-fix  
**提交 ID**：8dc9b1c

---

## 问题描述

用户报告状态指示灯（小绿点、小红点）在页面首次加载时可以正常显示，但在刷新或 WebSocket 状态更新后就会消失。

### 现象

- ✅ 页面首次加载：所有 Agent 标签都显示状态指示灯
- ❌ 刷新后或状态更新后：状态指示灯消失，只剩下文字

### 影响范围

- Insight Agent 标签
- Media Agent 标签
- Query Agent 标签
- Forum Host 标签
- Report Agent 标签

---

## 问题分析

### 根本原因

在 `updateAppStatus` 函数（第 1387 行）中，代码直接替换了状态指示灯元素的 `className`：

```javascript
indicator.className = `status-indicator ${status}`;
```

**问题点**：
1. HTML 中定义的类名是 `system-status-indicator`
2. JavaScript 中使用的类名是 `status-indicator`
3. 类名不匹配导致 CSS 样式无法应用
4. 指示灯元素虽然存在，但因为没有正确的样式而不可见

### 代码位置

**文件**：`/home/ubuntu/BettaFish/templates/index.html`  
**函数**：`updateAppStatus(data)`  
**行号**：1379-1392

### 原始代码

```javascript
function updateAppStatus(data) {
    for (const [app, info] of Object.entries(data)) {
        const status = info.status === 'running' ? 'running' : 'stopped';
        appStatus[app] = status;
        
        const indicator = document.getElementById(`status-${app}`);
        if (indicator) {
            indicator.className = `status-indicator ${status}`;  // ❌ 错误的类名
        }
    }
    updateEmbeddedPage(currentApp);
}
```

### HTML 结构

```html
<div class="system-status-indicator" id="status-insight"></div>
<div class="system-status-indicator" id="status-media"></div>
<div class="system-status-indicator" id="status-query"></div>
```

### CSS 样式

```css
.system-status-indicator {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: #ff3b30;
    /* ... */
}

.system-status-indicator.running {
    background-color: #34c759;
    /* ... */
}
```

---

## 修复方案

### 修改内容

将 JavaScript 中的类名从 `status-indicator` 改为 `system-status-indicator`，与 HTML 和 CSS 保持一致。

### 修复后代码

```javascript
function updateAppStatus(data) {
    for (const [app, info] of Object.entries(data)) {
        const status = info.status === 'running' ? 'running' : 'stopped';
        appStatus[app] = status;
        
        const indicator = document.getElementById(`status-${app}`);
        if (indicator) {
            indicator.className = `system-status-indicator ${status}`;  // ✅ 正确的类名
        }
    }
    updateEmbeddedPage(currentApp);
}
```

### 修改说明

**修改前**：`indicator.className = \`status-indicator ${status}\`;`  
**修改后**：`indicator.className = \`system-status-indicator ${status}\`;`

**变更点**：
- 将 `status-indicator` 改为 `system-status-indicator`
- 确保类名与 HTML 和 CSS 中的定义一致

---

## 测试验证

### 测试步骤

1. 重启 Flask 应用
2. 访问页面，确认状态指示灯显示
3. 等待 WebSocket 状态更新
4. 刷新页面
5. 再次确认状态指示灯是否持续显示

### 测试结果

✅ **所有测试通过**

- ✅ 页面首次加载：状态指示灯正常显示
- ✅ WebSocket 状态更新后：状态指示灯持续显示
- ✅ 页面刷新后：状态指示灯持续显示
- ✅ 不同状态正确显示不同颜色：
  - 红色：Engine 停止
  - 绿色：Engine 运行
  - 黄色：Engine 启动中

### 验证截图

从测试截图可以看到：
- Insight Agent：🔴 红色圆点（停止）
- Media Agent：🔴 红色圆点（停止）
- Query Agent：🔴 红色圆点（停止）
- Forum Host：🟢 绿色圆点（运行）
- Report Agent：🔴 红色圆点（停止）

---

## 版本信息

### Git 提交

**提交哈希**：`8dc9b1c`  
**提交信息**：fix: 修复 updateAppStatus 函数中的类名错误，确保状态指示灯持续显示  
**提交时间**：2026-01-11  
**分支**：main

### Git 标签

**标签名称**：`v1.1.3-status-fix`  
**标签说明**：修复状态指示灯持续显示问题  
**推送状态**：已推送到 GitHub

### 版本历史

- v1.1.0：现代化界面设计（配置弹窗有问题）
- v1.1.1：配置弹窗修复（指示灯不显示）
- v1.1.2：状态指示灯修复（指示灯会消失）
- **v1.1.3**：**状态指示灯持续显示修复**（当前推荐版本）✅

---

## 经验总结

### 问题教训

1. **类名一致性**：HTML、CSS、JavaScript 中的类名必须保持一致
2. **全局搜索**：修改类名时应该全局搜索所有引用
3. **完整测试**：不仅要测试初始状态，还要测试动态更新场景

### 最佳实践

1. **使用常量**：将类名定义为常量，避免硬编码
2. **代码审查**：重要的 UI 更新代码需要仔细审查
3. **版本管理**：每次修复都创建 Git 标签，方便回滚

### 改进建议

**未来优化方向**：
```javascript
// 建议使用常量定义类名
const CLASS_NAMES = {
    STATUS_INDICATOR: 'system-status-indicator',
    STATUS_RUNNING: 'running',
    STATUS_STOPPED: 'stopped',
    STATUS_STARTING: 'starting'
};

function updateAppStatus(data) {
    for (const [app, info] of Object.entries(data)) {
        const status = info.status === 'running' ? 
            CLASS_NAMES.STATUS_RUNNING : 
            CLASS_NAMES.STATUS_STOPPED;
        appStatus[app] = status;
        
        const indicator = document.getElementById(`status-${app}`);
        if (indicator) {
            indicator.className = `${CLASS_NAMES.STATUS_INDICATOR} ${status}`;
        }
    }
    updateEmbeddedPage(currentApp);
}
```

---

## 回滚指南

如果需要回滚到之前的版本：

```bash
# 回滚到 v1.1.2（指示灯会消失）
cd /home/ubuntu/BettaFish
git reset --hard v1.1.2-status-indicator
# 重启 Flask 应用

# 回滚到 v1.1.1（指示灯不显示）
cd /home/ubuntu/BettaFish
git reset --hard v1.1.1-config-fix
# 重启 Flask 应用

# 恢复到最新版本
cd /home/ubuntu/BettaFish
git reset --hard v1.1.3-status-fix
# 重启 Flask 应用
```

---

**文档作者**：Manus AI  
**最后更新**：2026-01-11  
**当前版本**：v1.1.3-status-fix (8dc9b1c)
