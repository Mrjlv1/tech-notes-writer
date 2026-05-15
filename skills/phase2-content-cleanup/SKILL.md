---
name: phase2-content-cleanup
version: 1.0.0
description: |
  Phase 2 content cleanup workflow: cleanup image prompts → backup prompts → final document.
  Ensures safe deletion with human-in-loop confirmation.
  Use after Phase 1 when user confirms draft is ready for cleanup.
description_zh: |
  第二阶段内容净化工作流：清理图像提示词 → 备份提示词 → 纯净文档。
  采用 Human-in-Loop 模式确保安全删除。
  在 Phase 1 完成后，用户确认初稿无误时使用。
category: content-creation
---

# Phase 2: 内容净化

## 工作流

```
用户确认："初稿无误，开始清理"
  ↓
Phase 5: 提示词识别和删除
  ├─ 精准识别 [🎨 生图提示词] 区块
  ├─ 仅删除提示词内容
  ├─ 保留图片描述（> 📷 ...）
  └─ 保留最终图像引用
  ↓
Phase 6: 提示词备份沉淀
  ├─ 创建备份文件
  │   路径：resources/images/{文档名}/{文档名}-image-prompts.md
  ├─ 记录提示词原文
  ├─ 记录图像位置
  ├─ 记录图像描述
  └─ 验证备份完整性
  ↓
输出：纯净文档 + 备份文件
```

---

## Phase 5: 提示词识别和删除

### ⚠️ 重要规则

**必须采用 Human-in-Loop 模式！**

### 识别提示词

#### 提示词格式

```markdown
[🎨 生图提示词]
```
[提示词内容]
```

> 📷 图片描述：[20字以内]
```

#### 识别规则

使用正则表达式匹配：

```regex
\[🎨 生图提示词\]\s*```\s*([\s\S]*?)```\s*\n\s*> 📷 (.+?)\n
```

**匹配内容**：
- `[🎨 生图提示词]` 标记
- 代码块中的完整提示词
- `> 📷` 图片描述

### 删除范围

#### ✅ 仅删除

- `[🎨 生图提示词]` 标记
- 提示词代码块内容

#### ❌ 保留

- `> 📷 图片描述`
- 图像引用（draw.io/Mermaid）
- 所有正文内容
- 代码示例
- 章节标题
- 文档导航

### 删除示例

#### 删除前（初稿）

```markdown
### 1.2 在阿里技术栈中的位置

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

#### 删除后（纯净文档）

```markdown
### 1.2 在阿里技术栈中的位置

> 📷 Sentinel 分层防护架构
```

### 安全确认

#### Human-in-Loop 确认流程

```markdown
⚠️  即将删除文档中的生图提示词

📋 识别到的提示词数量：X 个
📦 备份文件路径：resources/images/{文档名}/{文档名}-image-prompts.md

删除范围：
✅ 仅删除 [🎨 生图提示词] 标记和内容
✅ 保留图片描述（> 📷 ...）
✅ 保留所有正文内容

是否继续删除？(y/N)
```

**用户操作**：
- 输入 `y` → 执行删除
- 输入 `N` → 取消操作，保留初稿

---

## Phase 6: 提示词备份沉淀

### 备份文件创建

#### 文件路径

```
resources/images/{文档名}/{文档名}-image-prompts.md
```

**示例**：
```
resources/images/sentinel-deep-dive/sentinel-deep-dive-image-prompts.md
```

#### 创建流程

```markdown
1. 创建目录（如果不存在）
   mkdir -p resources/images/{文档名}/

2. 创建备份文件
   touch resources/images/{文档名}/{文档名}-image-prompts.md

3. 写入文件头
   # {文档名} - 图片提示词备份

4. 按顺序写入每个提示词
```

### 备份文件格式

```markdown
# {文档名} - 图片提示词备份

> 📅 备份时间：{YYYY-MM-DD HH:mm:ss}
> 📝 文档路径：{文档完整路径}
> 🔢 提示词数量：X 个

---

## 图片 1：[位置描述]

**位置**：第 X 章第 Y 节（[章节标题]）

**提示词**：
```
[完整的生图提示词原文]
```

**图片描述**：[20字以内的描述信息]

---

## 图片 2：[位置描述]

**位置**：第 X 章第 Y 节（[章节标题]）

**提示词**：
```
[完整的生图提示词原文]
```

**图片描述**：[20字以内的描述信息]

---

...
```

### 备份示例

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

**位置**：第 3 章第 3 节（3.3 三者协作关系）

**提示词**：
```
极简科技教育图解，扁平矢量插画，纯白底 #F8FAFC。
电商下单限流降级场景图，水平布局从左到右。
左侧：用户下单图标（圆角 12px，填充 #5D7C99）
中间：限流检查菱形（填充 #F59E0B）
右侧：订单服务矩形（圆角 8px，填充 #DCE6F1）
连接线：贝塞尔曲线，#64748B，箭头表示流程
每个框体带柔和弥散阴影
字体：中文思源黑体，英文 Inter
风格：高端工程教材，苹果 Keynote 审美
```

**图片描述**：电商下单限流流程

---

## 图片 3：Sentinel 核心架构

**位置**：第 5 章第 1 节（5.1 架构设计）

**提示词**：
```
极简科技教育图解，扁平矢量插画，纯白底 #F8FAFC。
Sentinel 核心架构概览图，中心辐射布局。
中心：Sentinel Core（圆角 12px，填充 #5D7C99）
四周：SlotChain、ProcessorSlot、Statistic、RuleManager（圆角 8px，填充 #DCE6F1）
连接线：贝塞尔曲线，#64748B，箭头指向数据流向
每个框体带柔和弥散阴影
字体：中文思源黑体，英文 Inter
风格：高端工程教材，苹果 Keynote 审美
```

**图片描述**：Sentinel 核心架构概览
```

---

## 🔒 安全机制

### 备份验证

#### 验证流程

```markdown
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

4. 检查文件是否可读写
   if (!file.canRead() || !file.canWrite()) {
       throw Error("备份文件权限错误");
   }
```

#### 验证报告

```markdown
# 备份验证报告

✅ 备份文件已创建
   路径：resources/images/sentinel-deep-dive/sentinel-deep-dive-image-prompts.md

✅ 提示词数量匹配
   初稿提示词：3 个
   备份提示词：3 个

✅ 文件格式正确
   文件头：正确
   分隔符：正确
   提示词格式：正确

✅ 文件权限正常
   可读：是
   可写：是

## 总结
✅ 备份验证通过，可以安全删除初稿提示词
```

### 删除前二次确认

```markdown
⚠️  二次确认

✅ 备份文件已创建并验证通过
   路径：resources/images/sentinel-deep-dive/sentinel-deep-dive-image-prompts.md

即将删除：
- 3 个 [🎨 生图提示词] 区块
- 仅删除提示词内容
- 保留图片描述和所有正文

是否确认删除？(y/N)
```

---

## ✅ 完成标准

Phase 2 完成的标志：

- ✅ 提示词识别完成
- ✅ Human 确认删除
- ✅ 提示词删除完成
- ✅ 备份文件创建成功
- ✅ 备份验证通过
- ✅ 输出纯净文档
- ✅ 输出备份文件

---

## 📊 输出清单

### 输出文件

| 文件 | 路径 | 说明 |
|------|------|------|
| **纯净文档** | `note/{文档名}.md` | 删除提示词后的最终文档 |
| **备份文件** | `resources/images/{文档名}/{文档名}-image-prompts.md` | 提示词备份（永久保留） |

### 保留内容

纯净文档中保留：
- ✅ 所有正文内容
- ✅ 所有章节标题
- ✅ 所有代码示例
- ✅ draw.io 图片引用
- ✅ Mermaid 代码块
- ✅ 图片描述（`> 📷 ...`）
- ✅ 文档导航

### 删除内容

仅删除：
- ❌ `[🎨 生图提示词]` 标记
- ❌ 提示词代码块内容

---

## 💡 常见问题

### Q1: 删除后能恢复提示词吗？

**A**: 可以！备份文件永久保留：
```
resources/images/{文档名}/{文档名}-image-prompts.md
```

### Q2: 可以跳过备份直接删除吗？

**A**: 不可以！必须先创建备份文件并验证通过。

### Q3: 如何验证备份完整性？

**A**: 系统自动验证：
- 提示词数量匹配
- 文件格式正确
- 文件权限正常

### Q4: 删除会影响正文吗？

**A**: 不会！仅删除提示词内容，保留所有正文。

---

**最后更新**：2026-05-14  
**版本**：v1.0.0
