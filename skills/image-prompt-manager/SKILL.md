---
name: image-prompt-manager
version: 1.0.0
description: |
  Manage AI image generation prompts for technical notes. Generate prompts, create backups, and cleanup draft prompts with human-in-loop confirmation.
  Use when generating AI image prompts or managing prompt backups.
description_zh: |
  管理 AI 图像生图提示词：生成提示词、创建备份、清理初稿提示词（Human-in-Loop 确认）。
  在生成 AI 图像提示词或管理提示词备份时使用。
category: content-creation
---

# Image Prompt Manager

## 功能

1. ✅ 生成 AI 图像生图提示词
2. ✅ 创建提示词备份文件
3. ✅ Human-in-Loop 确认后清理初稿提示词

---

## 功能 1：生成提示词

### 提示词格式

```markdown
[🎨 生图提示词]
```
极简科技教育图解，扁平矢量插画，纯白底 #F8FAFC。
[图名]，[布局描述]。
[元素 1 描述]（圆角 12px，填充 #5D7C99，文字 #1E293B）
[元素 2 描述]（圆角 8px，填充 #DCE6F1）
连接线：贝塞尔曲线，#64748B，箭头指向数据流向
每个框体带柔和弥散阴影
字体：中文思源黑体，英文 Inter
风格：高端工程教材，苹果 Keynote 审美
```

> 📷 图片描述：[20字以内的描述信息]
```

### 生成规则

#### 1. 结合上下文

```markdown
分析当前章节内容：
- 提取关键概念
- 确定视觉元素
- 明确要表达的核心信息

示例：
章节内容："Sentinel 采用分层防护架构，从上到下依次是..."

生成的提示词：
"Sentinel 分层防护架构图，垂直布局自上而下..."
```

#### 2. 精确描述

```markdown
必须包含：
✅ 布局（垂直/水平/中心辐射）
✅ 色彩（#5D7C99 主蓝，#DCE6F1 辅助蓝）
✅ 元素（圆角、阴影、文字）
✅ 风格（工程蓝图、扁平矢量）

示例：
"垂直布局自上而下"  ✅ 明确布局
"圆角 12px，填充 #5D7C99"  ✅ 精确描述
"贝塞尔曲线，#64748B"  ✅ 指定线条
```

#### 3. 图片描述

```markdown
要求：
✅ 20 字以内
✅ 简洁明了
✅ 概括核心内容

示例：
"Sentinel 分层防护架构"  ✅ 12 字
"电商下单限流流程"  ✅ 8 字
"Sentinel 核心架构概览"  ✅ 11 字
```

### 提示词模板

#### 架构图模板

```markdown
[🎨 生图提示词]
```
极简科技教育图解，扁平矢量插画，纯白底 #F8FAFC。
[技术名称] [架构图类型]，[布局描述]。
[顶层元素]（圆角 12px，填充 #5D7C99，文字白色）
[中层元素]（圆角 12px，填充 #F59E0B，文字白色）
[底层元素]（[数量]个圆角矩形，填充 #DCE6F1）
连接线：贝塞尔曲线，#64748B，箭头指向数据流向
每个框体带柔和弥散阴影
字体：中文思源黑体，英文 Inter
风格：高端工程教材，苹果 Keynote 审美
```

> 📷 [20字以内的描述]
```

#### 场景图模板

```markdown
[🎨 生图提示词]
```
极简科技教育图解，扁平矢量插画，纯白底 #F8FAFC。
[场景名称]场景图，[布局描述]。
[左侧元素]（圆角 12px，填充 #5D7C99）
[中间元素]（[形状]，填充 #F59E0B）
[右侧元素]（圆角 8px，填充 #DCE6F1）
连接线：贝塞尔曲线，#64748B，箭头表示流程
每个框体带柔和弥散阴影
字体：中文思源黑体，英文 Inter
风格：高端工程教材，苹果 Keynote 审美
```

> 📷 [20字以内的描述]
```

---

## 功能 2：创建备份文件

### 备份文件路径

```
resources/images/{文档名}/{文档名}-image-prompts.md
```

### 备份流程

```markdown
1. 识别文档中所有 [🎨 生图提示词] 区块

2. 创建目录
   mkdir -p resources/images/{文档名}/

3. 创建备份文件
   touch resources/images/{文档名}/{文档名}-image-prompts.md

4. 写入文件头
   # {文档名} - 图片提示词备份
   
   > 📅 备份时间：{YYYY-MM-DD HH:mm:ss}
   > 📝 文档路径：{文档完整路径}
   > 🔢 提示词数量：X 个

5. 按顺序写入每个提示词
   ## 图片 1：[位置描述]
   
   **位置**：第 X 章第 Y 节（[章节标题]）
   
   **提示词**：
   ```
   [完整提示词]
   ```
   
   **图片描述**：[20字描述]
```

### 备份文件示例

```markdown
# sentinel-deep-dive - 图片提示词备份

> 📅 备份时间：2026-05-14 10:30:00
> 📝 文档路径：/Users/wang/Documents/Obsidian Vault/MyNote/note/sentinel-deep-dive.md
> 🔢 提示词数量：3 个

---

## 图片 1：Sentinel 在阿里技术栈中的位置

**位置**：第 1 章第 2 节（1.2 在阿里技术栈中的位置）

**提示词**：
```
极简科技教育图解，扁平矢量插画，纯白底 #F8FAFC。
Sentinel 分层防护架构图，垂直布局自上而下。
顶层：用户请求（圆角 12px，填充 #5D7C99，文字白色）
中层：Sentinel 防护盾（圆角 12px，填充 #F59E0B，文字白色）
底层：HSF + TDDL 数据库（2个圆角矩形，填充 #DCE6F1）
连接线：贝塞尔曲线，#64748B，箭头指向数据流向
每个框体带柔和弥散阴影
字体：中文思源黑体，英文 Inter
风格：高端工程教材，苹果 Keynote 审美
```

**图片描述**：Sentinel 分层防护架构

---

## 图片 2：限流降级场景示意

...
```

---

## 功能 3：清理提示词

### ⚠️ Human-in-Loop 确认

**必须人工确认才能删除！**

### 清理流程

```markdown
1. 识别所有 [🎨 生图提示词] 区块

2. 创建备份文件（必须先备份）

3. 验证备份完整性
   - 提示词数量匹配
   - 文件格式正确
   - 文件权限正常

4. 【HUMAN 确认】
   ⚠️  即将删除文档中的生图提示词
   
   📋 识别到的提示词数量：X 个
   📦 备份文件路径：{备份路径}
   
   删除范围：
   ✅ 仅删除 [🎨 生图提示词] 标记和内容
   ✅ 保留图片描述（> 📷 ...）
   ✅ 保留所有正文内容
   
   是否继续删除？(y/N)

5. 用户确认
   - 输入 y → 执行删除
   - 输入 N → 取消操作

6. 执行删除
   - 删除 [🎨 生图提示词] 标记
   - 删除提示词代码块
   - 保留 > 📷 图片描述
   - 保留所有正文

7. 完成确认
   ✅ 提示词已清理
   📦 备份文件保留：{备份路径}
```

### 删除示例

#### 删除前

```markdown
### 1.2 在阿里技术栈中的位置

[🎨 生图提示词]
```
极简科技教育图解...
```

> 📷 Sentinel 分层防护架构
```

#### 删除后

```markdown
### 1.2 在阿里技术栈中的位置

> 📷 Sentinel 分层防护架构
```

---

## 🔒 安全机制

### 备份验证

```markdown
验证流程：

1. 检查备份文件是否存在
   if (!file.exists(backupPath)) {
       throw Error("备份文件创建失败");
   }

2. 检查提示词数量是否匹配
   if (backupPromptCount != draftPromptCount) {
       throw Error("提示词数量不匹配");
   }

3. 检查文件格式是否正确
   if (!validateBackupFormat(backupPath)) {
       throw Error("备份文件格式错误");
   }

4. 检查文件权限
   if (!file.canRead() || !file.canWrite()) {
       throw Error("备份文件权限错误");
   }
```

### 删除保护

```markdown
保护措施：

✅ 必须先备份
   - 备份文件不存在 → 拒绝删除
   
✅ 备份验证通过
   - 验证失败 → 拒绝删除
   
✅ Human 确认
   - 未确认 → 拒绝删除
   
✅ 二次确认
   - 删除前再次确认
   
✅ 永久保留备份
   - 备份文件永不删除
```

---

## 📊 使用示例

### 示例 1：生成提示词

```markdown
输入：为"Sentinel 分层防护架构"生成提示词

输出：

[🎨 生图提示词]
```
极简科技教育图解，扁平矢量插画，纯白底 #F8FAFC。
Sentinel 分层防护架构图，垂直布局自上而下。
顶层：用户请求（圆角 12px，填充 #5D7C99，文字白色）
中层：Sentinel 防护盾（圆角 12px，填充 #F59E0B，文字白色）
底层：HSF + TDDL 数据库（2个圆角矩形，填充 #DCE6F1）
连接线：贝塞尔曲线，#64748B，箭头指向数据流向
每个框体带柔和弥散阴影
字体：中文思源黑体，英文 Inter
风格：高端工程教材，苹果 Keynote 审美
```

> 📷 Sentinel 分层防护架构
```

### 示例 2：创建备份

```markdown
输入：为 sentinel-deep-dive.md 创建提示词备份

输出：
✅ 备份文件已创建
   路径：resources/images/sentinel-deep-dive/sentinel-deep-dive-image-prompts.md
   提示词数量：3 个
```

### 示例 3：清理提示词

```markdown
输入：清理 sentinel-deep-dive.md 中的提示词

系统：
⚠️  即将删除文档中的生图提示词

📋 识别到的提示词数量：3 个
📦 备份文件路径：resources/images/sentinel-deep-dive/sentinel-deep-dive-image-prompts.md

是否继续删除？(y/N)

用户输入：y

系统：
✅ 提示词已清理
📦 备份文件保留：resources/images/sentinel-deep-dive/sentinel-deep-dive-image-prompts.md
```

---

## 💡 最佳实践

### 生成提示词

1. **结合上下文** - 分析章节内容，提取关键概念
2. **精确描述** - 指定布局、色彩、元素、风格
3. **简洁描述** - 图片描述控制在 20 字以内

### 创建备份

1. **及时备份** - Phase 6 自动触发
2. **验证完整性** - 检查数量和格式
3. **永久保留** - 备份文件永不删除

### 清理提示词

1. **仔细审阅** - 确认初稿无误
2. **验证备份** - 确认备份完整
3. **安全删除** - 仅删除提示词内容

---

**最后更新**：2026-05-14  
**版本**：v1.0.0
