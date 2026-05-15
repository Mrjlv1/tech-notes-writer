---
name: drawio-diagram
description: Create and edit draw.io diagrams (.drawio or .xml files) for architecture diagrams, flowcharts, sequence diagrams, and technical illustrations. Use when working with draw.io files, creating visual diagrams for Obsidian, or when the user mentions draw.io, diagrams.net, or needs editable vector diagrams.
description_zh: 创建和编辑 draw.io 图表文件，用于架构图、流程图、时序图等技术插图。生成的图表可在 Obsidian 的 draw.io 插件中直接编辑，支持后续修改和版本管理。
category: design-ui
recommended: true
---

# Draw.io 图表生成技能

## 概述

draw.io（现名 diagrams.net）是一款流行的开源图表工具，支持创建：
- 架构图（分层架构、微服务架构）
- 流程图（业务流程、数据流向）
- 时序图（服务调用、消息传递）
- 类图、ER 图、网络拓扑图等

与 PNG/SVG 静态图片不同，draw.io 文件**可编辑**，便于后续维护和更新。

---

## 何时使用 draw.io

### 适合场景

| 场景 | 原因 |
|------|------|
| **需要后续修改** | 架构图会随项目演进变化 |
| **团队协作编辑** | 多人维护同一份架构图 |
| **版本管理** | Git 追踪图表变更历史 |
| **Obsidian 集成** | 使用 Obsidian Draw.io 插件直接编辑 |
| **多格式导出** | 同一源文件导出 PNG/SVG/PDF |

### 不适合场景

| 场景 | 推荐方案 |
|------|---------|
| 快速生成静态插图 | drafter skill（HTML → PNG） |
| 简单的思维导图 | JSON Canvas（.canvas 文件） |
| 文档内嵌小图标 | Mermaid 代码块 |

---

## Draw.io XML 格式基础

draw.io 文件本质是 mxGraph 格式的 XML 文件：

```xml
<mxfile host="app.diagrams.net" modified="2024-01-01T00:00:00.000Z">
  <diagram id="diagram-id" name="Page-1">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="827" pageHeight="1169">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
        <!-- 图形元素 -->
        <mxCell id="2" value="节点名称" style="rounded=1;fillColor=#5D7C99;" vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="120" height="60" as="geometry" />
        </mxCell>
        
        <!-- 连接线 -->
        <mxCell id="3" style="edgeStyle=orthogonalEdgeStyle;" edge="1" source="2" target="4" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### 核心概念

| 概念 | 说明 |
|------|------|
| `mxCell` | 基本单元，可以是节点（vertex）或边（edge） |
| `id` | 唯一标识符，建议使用递增数字字符串 |
| `value` | 节点显示的文字 |
| `style` | 样式定义（颜色、形状、圆角等） |
| `mxGeometry` | 位置和尺寸（x, y, width, height） |
| `vertex="1"` | 表示这是一个节点 |
| `edge="1"` | 表示这是一条连接线 |
| `source/target` | 边的起点和终点节点 ID |

---

## 常用样式参考

### 节点样式

```xml
<!-- 圆角矩形（推荐用于代码块、服务名） -->
style="rounded=1;whiteSpace=wrap;html=1;fillColor=#5D7C99;strokeColor=#4A6580;fontColor=#FFFFFF;"

<!-- 普通矩形 -->
style="whiteSpace=wrap;html=1;fillColor=#DCE6F1;strokeColor=#64748B;"

<!-- 菱形（决策点） -->
style="rhombus;whiteSpace=wrap;html=1;fillColor=#F59E0B;strokeColor=#D97706;"

<!-- 圆形 -->
style="ellipse;whiteSpace=wrap;html=1;fillColor=#22C55E;strokeColor=#16A34A;"

<!-- 圆柱体（数据库） -->
style="shape=cylinder;whiteSpace=wrap;html=1;fillColor=#E2E8F0;strokeColor=#64748B;"
```

### 连接线样式

```xml
<!-- 实线箭头 -->
style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;"

<!-- 虚线箭头 -->
style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;dashed=1;"

<!-- 带标签的线 -->
style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;edgeLabel=数据传输;"

<!-- 正交边（直角转折） -->
style="edgeStyle=orthogonalEdgeStyle;endArrow=classic;html=1;strokeColor=#64748B;"

<!-- 曲线边（推荐用于数据流） -->
style="edgeStyle=segmentEdgeStyle;curved=1;endArrow=classic;html=1;strokeColor=#64748B;"
```

---

## 工作流

### 1. 创建新图表

**步骤**：
1. 创建 `.drawio` 文件（XML 格式）
2. 定义 `<mxfile>` 和 `<diagram>` 结构
3. 添加根节点（id="0" 和 id="1"）
4. 按布局添加图形元素和连接线
5. 验证 XML 格式正确性

**示例：简单的三层架构图**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="app.diagrams.net" modified="2024-01-15T10:00:00.000Z" agent="Qoder" version="24.0.0">
  <diagram id="hsf-arch-001" name="HSF Architecture">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" tooltips="1" connect="1" arrows="1" fold="1" page="1" pageScale="1" pageWidth="1200" pageHeight="800">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
        <!-- Consumer 层 -->
        <mxCell id="10" value="Consumer&#10;（服务调用方）" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#5D7C99;strokeColor=#4A6580;fontColor=#FFFFFF;fontSize=14;" vertex="1" parent="1">
          <mxGeometry x="100" y="100" width="180" height="80" as="geometry" />
        </mxCell>
        
        <!-- Provider 层 -->
        <mxCell id="11" value="Provider&#10;（服务提供方）" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#5D7C99;strokeColor=#4A6580;fontColor=#FFFFFF;fontSize=14;" vertex="1" parent="1">
          <mxGeometry x="920" y="100" width="180" height="80" as="geometry" />
        </mxCell>
        
        <!-- ConfigServer -->
        <mxCell id="12" value="ConfigServer&#10;（注册中心）" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DCE6F1;strokeColor=#64748B;fontSize=14;" vertex="1" parent="1">
          <mxGeometry x="510" y="350" width="180" height="80" as="geometry" />
        </mxCell>
        
        <!-- 连接线 -->
        <mxCell id="20" value="RPC 调用" style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;rounded=1;" edge="1" source="10" target="11" parent="1">
          <mxGeometry x="-0.3" y="0" relative="1" as="geometry">
            <mxPoint as="offset" />
          </mxGeometry>
        </mxCell>
        
        <mxCell id="21" value="服务注册" style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;dashed=1;rounded=1;" edge="1" source="11" target="12" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        
        <mxCell id="22" value="地址推送" style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;dashed=1;rounded=1;" edge="1" source="12" target="10" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

### 2. 编辑现有图表

**步骤**：
1. 读取 `.drawio` 文件
2. 解析 XML 结构
3. 定位目标节点或边（通过 `id` 或 `value`）
4. 修改属性（位置、样式、文字等）
5. 保存文件

### 3. 导出图片

draw.io 文件可以在以下位置导出为 PNG/SVG：
- **在线编辑器**：https://app.diagrams.net/
- **桌面应用**：Download from GitHub
- **Obsidian 插件**：Draw.io Integration
- **命令行**：使用 `drawio` CLI 工具

```bash
# 导出为 PNG
drawio -x -o output.png input.drawio

# 导出为 SVG
drawio -x -f svg -o output.svg input.drawio
```

---

## 布局指南

### 1. 页面设置

```xml
<mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" 
              pageWidth="1200" pageHeight="800">
```

常用尺寸：
- **宽屏**：1200 x 800（推荐用于架构图）
- **A4 横向**：1169 x 827
- **A4 纵向**：827 x 1169

### 2. 网格对齐

- 网格大小：`gridSize="10"`
- 所有坐标建议使用 10 的倍数
- 节点间距：至少 50px

### 3. 典型布局模式

#### 垂直分层布局

```
┌─────────────────┐
│   Layer 1 (y=100)  │
├─────────────────┤
│   Layer 2 (y=300)  │
├─────────────────┤
│   Layer 3 (y=500)  │
└─────────────────┘
```

#### 水平流程布局

```
┌─────┐     ┌─────┐     ┌─────┐
│Step1│────→│Step2│────→│Step3│
└─────┘     └─────┘     └─────┘
(x=100)    (x=400)    (x=700)
```

#### 中心辐射布局

```
         ┌────────┐
         │ Center │
         │(x=500) │
         └────────┘
        ↙    ↓    ↘
   ┌───┐  ┌───┐  ┌───┐
   │ A │  │ B │  │ C │
   └───┘  └───┘  └───┘
```

---

## 色彩规范（与笔记技能统一）

| 用途 | 色值 | 使用场景 |
|------|------|---------|
| 主视觉蓝 | `#5D7C99` | 核心服务、主流程节点 |
| 辅助淡蓝 | `#DCE6F1` | 次要组件、基础设施 |
| 背景灰 | `#E2E8F0` | 辅助元素、分组框 |
| 成功绿 | `#22C55E` | 完成状态、成功路径 |
| 警告橙 | `#F59E0B` | 注意项、中间状态 |
| 危险红 | `#EF4444` | 错误、拦截点 |
| 线条色 | `#64748B` | 所有连接线和边框 |
| 文字色 | `#1E293B` | 所有文本 |

---

## 最佳实践

### 1. 节点设计

✅ **推荐**：
- 使用圆角（`rounded=1`）
- 文字换行（`whiteSpace=wrap`）
- 字体大小 12-14px
- 节点尺寸统一（如 120x60 或 180x80）

❌ **避免**：
- 直角矩形（不够现代）
- 文字过长不换行
- 节点大小参差不齐
- 超过 5 种颜色

### 2. 连接线设计

✅ **推荐**：
- 使用圆角连接（`rounded=1`）
- 线条宽度 2px
- 添加箭头（`endArrow=classic`）
- 重要连接添加标签

❌ **避免**：
- 交叉线条过多
- 无箭头的线（方向不明）
- 线条太细（<1px）

### 3. 文字排版

✅ **推荐**：
- 中文使用 `&#10;` 换行
- 标题 14px，正文 12px
- 关键信息加粗或变色
- 保持文字居中对齐

❌ **避免**：
- 一段超长文字
- 超过 3 行文字
- 字体太小（<10px）

### 4. 文件管理

✅ **推荐**：
- 文件名：`{文档名}-{图类型}.drawio`
- 版本管理：纳入 Git
- 导出图片同步保存
- 添加 `modified` 时间戳

示例：
```
resources/images/hsf-deep-dive/
├── hsf-architecture.drawio    # 源文件（可编辑）
└── hsf-architecture.png       # 导出图片（文档引用）
```

---

## 与 Obsidian 集成

### 1. 安装 Draw.io 插件

在 Obsidian 中：
1. Settings → Community Plugins → Browse
2. 搜索 "Draw.io Integration"
3. 安装并启用

### 2. 在 Obsidian 中编辑

- 点击 `.drawio` 文件即可在 Obsidian 内编辑
- 支持实时预览
- 可直接导出为 PNG 嵌入笔记

### 3. 文档引用方式

```markdown
<!-- 方式 1：引用导出的 PNG -->
![HSF 架构图](../resources/images/hsf-deep-dive/hsf-architecture.png)

<!-- 方式 2：直接嵌入 drawio 文件（需插件支持） -->
![[hsf-architecture.drawio]]
```

---

## 完整示例：电商订单流程图

```xml
<?xml version="1.0" encoding="UTF-8"?>
<mxfile host="app.diagrams.net" modified="2024-01-15T12:00:00.000Z">
  <diagram id="order-flow-001" name="Order Creation Flow">
    <mxGraphModel dx="1422" dy="762" grid="1" gridSize="10" guides="1" connect="1" arrows="1" page="1" pageScale="1" pageWidth="1400" pageHeight="900">
      <root>
        <mxCell id="0" />
        <mxCell id="1" parent="0" />
        
        <!-- 用户 -->
        <mxCell id="10" value="用户请求" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#5D7C99;strokeColor=#4A6580;fontColor=#FFFFFF;fontSize=14;" vertex="1" parent="1">
          <mxGeometry x="50" y="350" width="120" height="60" as="geometry" />
        </mxCell>
        
        <!-- HSF 服务 -->
        <mxCell id="11" value="HSF OrderService&#10;createOrder()" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#DCE6F1;strokeColor=#64748B;fontSize=12;" vertex="1" parent="1">
          <mxGeometry x="300" y="350" width="160" height="60" as="geometry" />
        </mxCell>
        
        <!-- TDDL 数据库 -->
        <mxCell id="12" value="TDDL&#10;order_db" style="shape=cylinder;whiteSpace=wrap;html=1;fillColor=#E2E8F0;strokeColor=#64748B;fontSize=12;" vertex="1" parent="1">
          <mxGeometry x="600" y="200" width="120" height="100" as="geometry" />
        </mxCell>
        
        <!-- MetaQ 消息队列 -->
        <mxCell id="13" value="MetaQ&#10;ORDER_TOPIC" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#E2E8F0;strokeColor=#64748B;fontSize=12;" vertex="1" parent="1">
          <mxGeometry x="600" y="500" width="120" height="100" as="geometry" />
        </mxCell>
        
        <!-- EagleEye 链路追踪 -->
        <mxCell id="14" value="EagleEye&#10;TraceId: xxx" style="rounded=1;whiteSpace=wrap;html=1;fillColor=#F59E0B;strokeColor=#D97706;fontColor=#FFFFFF;fontSize=12;" vertex="1" parent="1">
          <mxGeometry x="900" y="350" width="140" height="60" as="geometry" />
        </mxCell>
        
        <!-- 成功响应 -->
        <mxCell id="15" value="返回订单ID" style="ellipse;whiteSpace=wrap;html=1;fillColor=#22C55E;strokeColor=#16A34A;fontColor=#FFFFFF;fontSize=12;" vertex="1" parent="1">
          <mxGeometry x="1200" y="350" width="120" height="60" as="geometry" />
        </mxCell>
        
        <!-- 连接线 -->
        <mxCell id="20" value="1.发起请求" style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;rounded=1;" edge="1" source="10" target="11" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        
        <mxCell id="21" value="2.写入订单" style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;rounded=1;" edge="1" source="11" target="12" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        
        <mxCell id="22" value="3.发送消息" style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;rounded=1;" edge="1" source="11" target="13" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        
        <mxCell id="23" value="4.记录链路" style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;dashed=1;rounded=1;" edge="1" source="11" target="14" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
        
        <mxCell id="24" value="5.返回结果" style="endArrow=classic;html=1;strokeColor=#64748B;strokeWidth=2;rounded=1;" edge="1" source="14" target="15" parent="1">
          <mxGeometry relative="1" as="geometry" />
        </mxCell>
      </root>
    </mxGraphModel>
  </diagram>
</mxfile>
```

---

## 验证清单

创建或编辑 draw.io 文件后，验证：

- [ ] XML 格式正确（可用 XML 验证器检查）
- [ ] 所有节点 `id` 唯一
- [ ] 所有连接线的 `source` 和 `target` 指向有效节点
- [ ] 节点不重叠（留至少 50px 间距）
- [ ] 文字清晰可读（字号 ≥ 12px）
- [ ] 颜色符合规范（不超过 5 种主色）
- [ ] 文件可在 draw.io 中正常打开
- [ ] 导出 PNG 后清晰度足够

---

## 参考资源

- **在线编辑器**：https://app.diagrams.net/
- **GitHub**：https://github.com/jgraph/drawio
- **Obsidian 插件**：Draw.io Integration
- **mxGraph 文档**：https://jgraph.github.io/mxgraph/
- **样式参考**：https://www.drawio.com/doc/faq/shape-style
