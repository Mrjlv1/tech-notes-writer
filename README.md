# Tech Notes Writer 技能集

> 两阶段自动化技术笔记写作技能：深度调研 + 智能配图 + Review 检查 + 提示词管理

## 📋 简介

Tech Notes Writer 是一个完整的技能集，用于自动化生成高质量的技术学习笔记。它采用两阶段执行模式，确保内容质量和数据安全。

### 核心特性

- ✅ **深度调研** - 自动调用 deep-research 全面调研技术主题
- ✅ **场景驱动** - 以具体业务场景贯穿全文（如电商下单）
- ✅ **智能配图** - draw.io + Mermaid + AI 图像提示词
- ✅ **Review 检查** - 自动检查内容逻辑、技术准确性、代码完整性
- ✅ **两阶段执行** - 内容生成 + 内容净化，确保安全可控
- ✅ **提示词管理** - 自动生成、备份、清理 AI 图像提示词
- ✅ **Human-in-Loop** - 关键节点人工审核，防止误操作

---

## 🚀 快速开始

### 触发技能

```
"帮我写一篇关于 Sentinel 的技术笔记"
```

### 第一阶段：内容生成（自动）

```
Phase 1: deep-research 调研
  ↓
Phase 2: 内容整理
  ↓
Phase 3: 场景写作
  ↓
Phase 4: 智能配图
  ↓
🔍 Review 检查
  ↓
输出：初稿文档
```

### 用户审阅

```
检查内容：
- 技术准确性
- 代码可运行性
- 场景贴切度
```

### 第二阶段：内容净化（确认后）

```
"初稿无误，开始清理提示词"
  ↓
Phase 5: 删除提示词
  ↓
Phase 6: 创建备份
  ↓
输出：纯净文档 + 备份文件
```

详细使用指南：[QUICKSTART.md](QUICKSTART.md)

---

## 📦 技能集结构

```
tech-notes-writer/
├── README.md                                 # 本文件
├── QUICKSTART.md                             # 快速入门指南
├── ARCHITECTURE.md                           # 架构设计文档
│
└── skills/
    ├── SKILL.md                              # 主技能（两阶段编排）
    │
    ├── phase1-content-generation/            # 第一阶段：内容生成
    │   ├── SKILL.md                          # Phase 1-4 工作流
    │   └── review-checklist.md               # Review 检查清单
    │
    ├── phase2-content-cleanup/               # 第二阶段：内容净化
    │   └── SKILL.md                          # Phase 5-6 工作流
    │
    ├── drawio-diagram/                       # 子技能：draw.io 图表
    │   ├── SKILL.md                          # draw.io 规范
    │   └── EXAMPLES.md                       # 使用示例
    │
    └── image-prompt-manager/                 # 子技能：提示词管理
        └── SKILL.md                          # 提示词生成和备份
```

---

## 🎯 两阶段工作流

### 第一阶段：内容生成

| Phase | 名称 | 功能 | 输出 |
|-------|------|------|------|
| Phase 1 | deep-research | 深度调研技术主题 | 结构化素材 |
| Phase 2 | organize | 整理为场景结构 | 内容大纲 |
| Phase 3 | write | 按五步讲解法写作 | 文档正文 |
| Phase 4 | illustrate | 智能配图 | 含插图初稿 |
| Review | 内容检查 | 自动质量检查 | 检查报告 |

**Review 检查项**：
- ✅ 内容逻辑一致性
- ✅ 技术准确性
- ✅ 场景连贯性
- ✅ 代码示例完整性

### 第二阶段：内容净化

| Phase | 名称 | 功能 | 输出 |
|-------|------|------|------|
| Phase 5 | cleanup | 删除图像提示词 | 纯净文档 |
| Phase 6 | backup | 备份提示词 | 备份文件 |

**备份文件路径**：
```
resources/images/{文档名}/{文档名}-image-prompts.md
```

---

## 🎨 图像生成

### 三种图像方式

| 方式 | 适用场景 | 示例 | 输出格式 |
|------|---------|------|---------|
| **draw.io** | 复杂架构图（>10 组件） | 分层架构、数据流向 | .drawio + .png |
| **Mermaid** | 简单流程图、时序图 | 调用流程、生命周期 | Markdown 代码块 |
| **AI 提示词** | 概念插图、场景示意 | 限流场景、降级流程 | 提示词文本 |

### AI 提示词格式

#### 初稿中（清理前）

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

#### 纯净文档（清理后）

```markdown
### 1.2 在阿里技术栈中的位置

> 📷 Sentinel 分层防护架构
```

#### 备份文件

```markdown
# sentinel-deep-dive - 图片提示词备份

## 图片 1：Sentinel 在阿里技术栈中的位置

**位置**：第 1 章第 2 节（1.2 在阿里技术栈中的位置）

**提示词**：
```
极简科技教育图解，扁平矢量插画...（完整提示词）
```

**图片描述**：Sentinel 分层防护架构
```

---

## 🔍 Review 功能详解

### 检查流程

```
Phase 4 完成
  ↓
Review 自动执行
  ├─ 1. 内容逻辑一致性检查
  ├─ 2. 技术准确性检查
  ├─ 3. 场景连贯性检查
  └─ 4. 代码示例完整性检查
  ↓
生成检查报告
  ├─ ✅ 全部通过 → 输出初稿
  └─ ❌ 有未通过 → 返回 Phase 3 重新写作
```

### 检查项详情

#### 1. 内容逻辑一致性

- [ ] 章节间有因果递进关系
- [ ] 场景贯穿全文不断裂
- [ ] 技术引入自然不生硬
- [ ] 前后内容无矛盾

#### 2. 技术准确性

- [ ] 技术定义准确无误
- [ ] 代码示例语法正确
- [ ] 配置方法切实可行
- [ ] 原理描述符合实际

#### 3. 场景连贯性

- [ ] 核心场景贴切易懂
- [ ] 示例符合场景设定
- [ ] 类比恰当不牵强
- [ ] 场景转换自然

#### 4. 代码示例完整性

- [ ] 代码可直接运行
- [ ] 包含必要注释说明
- [ ] 有完整上下文
- [ ] 关键步骤不缺失

---

## 🔒 安全机制

### Human-in-Loop 节点

| 节点 | 位置 | 说明 | 操作 |
|------|------|------|------|
| 初稿审核 | Phase 4 后 | 确认初稿质量 | ✅ 可行 / ❌ 修改 |
| 清理确认 | Phase 5 前 | 确认删除提示词 | ✅ 删除 / ❌ 保留 |

### 数据保护

- ✅ **必须先备份** - 备份文件不存在则拒绝删除
- ✅ **备份验证** - 验证备份完整性和数量匹配
- ✅ **Human 确认** - 必须人工确认才能删除
- ✅ **二次确认** - 删除前再次确认
- ✅ **永久保留** - 备份文件永久存储

### 删除范围

**仅删除**：
- `[🎨 生图提示词]` 标记
- 提示词代码块内容

**保留**：
- `> 📷 图片描述`
- 图像引用（draw.io/Mermaid）
- 所有正文内容
- 代码示例
- 章节标题

---

## 📝 文档规范

### Frontmatter

```yaml
---
title: "{技术名称} 深度剖析"
tags:
  - "{技术名}"
  - "中间件"
  - "阿里技术栈"
  - "深度调研"
created: {当前日期 YYYY-MM-DD}
updated: {当前日期 YYYY-MM-DD}
related:
  - "[[相关笔记 1]]"
  - "[[相关笔记 2]]"
---
```

### 五步讲解法

1. **遇到问题** - 具体困境
2. **没有它会怎样** - 朴素方案行不通
3. **一句话定义 + 类比** - 生活比喻
4. **快速上手** - 最小可运行代码
5. **深入原理** - 架构图 + 底层流程

### 章节总结

每个核心章节后添加：

```markdown
> 💡 **核心要点**
> 
> - 要点 1
> - 要点 2
> - 要点 3
```

---

## 📊 技能集版本

| 版本 | 日期 | 核心功能 |
|------|------|---------|
| **v1.0.0** | **2026-05-14** | **deep-research + draw.io + Mermaid + AI 图像提示词 + Human-in-Loop + 两阶段执行 + Review 检查 + 提示词备份** |

---

## 🚀 Plugin 开发预留

### 架构设计

未来可开发为 Obsidian Plugin：

```
tech-notes-writer-plugin/
├── src/
│   ├── phase1/                     # 第一阶段模块
│   │   ├── research.ts             # deep-research
│   │   ├── organize.ts             # 内容整理
│   │   ├── writing.ts              # 场景写作
│   │   ├── illustration.ts         # 智能配图
│   │   └── review.ts               # Review 检查
│   ├── phase2/                     # 第二阶段模块
│   │   ├── cleanup.ts              # 提示词删除
│   │   └── backup.ts               # 提示词备份
│   ├── ui/                         # 用户界面
│   │   ├── preview.ts              # 预览面板
│   │   ├── review-panel.ts         # Review 面板
│   │   └── cleanup-confirm.ts      # 清理确认
│   └── core/                       # 核心模块
│       ├── workflow.ts             # 工作流引擎
│       ├── prompt-manager.ts       # 提示词管理
│       └── file-handler.ts         # 文件处理
├── manifest.json                   # Obsidian 插件清单
└── styles.css                      # 样式文件
```

### 接口预留

当前 Skill 设计已预留：

1. **工作流引擎接口** - Phase 独立执行、暂停恢复、进度追踪
2. **提示词管理接口** - 生成、提取、备份
3. **Review 检查接口** - 逻辑、准确性、连贯性、完整性检查
4. **文件处理接口** - 读取、识别、创建、写入

---

## 📚 文档索引

| 文档 | 路径 | 说明 |
|------|------|------|
| **快速入门** | [QUICKSTART.md](QUICKSTART.md) | 5 分钟快速开始 |
| **架构设计** | [ARCHITECTURE.md](ARCHITECTURE.md) | 技能集架构和 Plugin 预留 |
| **主技能** | [skills/SKILL.md](skills/SKILL.md) | 两阶段工作流编排 |
| **第一阶段** | [skills/phase1-content-generation/SKILL.md](skills/phase1-content-generation/SKILL.md) | 内容生成全流程 |
| **第二阶段** | [skills/phase2-content-cleanup/SKILL.md](skills/phase2-content-cleanup/SKILL.md) | 内容净化全流程 |
| **Review 清单** | [skills/phase1-content-generation/review-checklist.md](skills/phase1-content-generation/review-checklist.md) | Review 检查项 |
| **draw.io 规范** | [skills/drawio-diagram/SKILL.md](skills/drawio-diagram/SKILL.md) | 架构图生成规范 |
| **提示词管理** | [skills/image-prompt-manager/SKILL.md](skills/image-prompt-manager/SKILL.md) | 提示词生成和备份 |

---

## 💡 最佳实践

### 内容生成阶段

1. **明确场景** - 指定具体的业务场景（如电商下单）
2. **深度调研** - 让 deep-research 全面调研技术主题
3. **插图规划** - 提前识别需要插图的位置和类型
4. **仔细审阅** - 检查内容准确性、代码可运行性

### 内容净化阶段

1. **完整审阅** - 确认所有细节无误后再清理
2. **验证备份** - 确认备份文件创建成功且完整
3. **安全清理** - 仅删除提示词，保留所有正文内容
4. **永久保留** - 备份文件永久存储，随时可恢复

---

## 🤝 贡献指南

### 扩展技能集

1. 在 `phase1-content-generation/templates/` 添加新模板
2. 在 `image-prompt-manager/templates/` 添加提示词模板
3. 更新 `ARCHITECTURE.md` 记录变更

### 改进 Review 检查

1. 在 `phase1-content-generation/review-checklist.md` 添加检查项
2. 更新主 SKILL.md 的 Review 流程
3. 测试新的检查逻辑

---

## 📞 技术支持

- **问题反馈**：提交 Issue
- **功能建议**：提交 Feature Request
- **文档改进**：提交 PR

---

**最后更新**：2026-05-14  
**技能集版本**：v1.0.0  
**许可证**：MIT
