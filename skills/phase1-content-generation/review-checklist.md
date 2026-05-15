# Review 检查清单

## 📋 检查流程

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

---

## 1. 内容逻辑一致性检查

### 检查项

- [ ] 章节间有因果递进关系
- [ ] 场景贯穿全文不断裂
- [ ] 技术引入自然不生硬
- [ ] 前后内容无矛盾
- [ ] 逻辑链条完整

### 检查方法

#### 1.1 章节递进关系

```markdown
检查章节标题和内容：

1. 遇到什么问题 → 引入场景
2. 没有它会怎样 → 说明必要性
3. 技术定义 → 引入解决方案
4. 快速上手 → 最小示例
5. 深入原理 → 架构和流程
6. 实战应用 → 场景中的具体应用
7. 最佳实践 → 生产经验

验证：
✅ 每章之间有明确的因果关系
✅ 前后章节自然过渡
✅ 没有跳跃或断裂
```

#### 1.2 场景贯穿

```markdown
检查核心场景是否贯穿全文：

场景：电商下单

1. 遇到什么问题
   ✅ 提到"电商大促期间，订单服务..."
   
2. 没有它会怎样
   ✅ 提到"如果手动限流，订单会..."
   
3. 技术定义
   ✅ 类比"就像电商仓库的库存控制..."
   
4. 快速上手
   ✅ 示例"订单服务限流配置..."
   
5. 深入原理
   ✅ 场景"订单请求通过 Sentinel..."
   
6. 实战应用
   ✅ 场景"订单创建、库存扣减、支付..."
   
7. 最佳实践
   ✅ 场景"电商大促期间的限流策略..."
```

#### 1.3 技术引入

```markdown
检查技术引入是否自然：

❌ 不自然：
"今天我们来学习 Sentinel。Sentinel 是..."

✅ 自然：
"面对订单服务的突发流量，我们需要一个自动化的限流降级方案。
这就是 Sentinel 发挥作用的地方..."
```

### 通过标准

全部检查项通过 → ✅ 通过  
有 1 项未通过 → ❌ 返回 Phase 3

---

## 2. 技术准确性检查

### 检查项

- [ ] 技术定义准确无误
- [ ] 代码示例语法正确
- [ ] 配置方法切实可行
- [ ] 原理描述符合实际
- [ ] 版本信息正确

### 检查方法

#### 2.1 技术定义

```markdown
检查技术定义是否准确：

Sentinel 定义：
✅ 正确："Sentinel 是阿里巴巴开源的流量防卫兵，面向分布式服务架构的高可用防护组件"
❌ 错误："Sentinel 是一个消息队列"

检查点：
- 核心功能描述准确
- 定位清晰
- 无误导性描述
```

#### 2.2 代码示例

```markdown
检查代码示例：

1. 语法检查
   ✅ 代码语法正确
   ✅ 无编译错误
   
2. 依赖检查
   ✅ Maven 依赖版本号正确
   ✅ 依赖存在且可用
   
3. 导入检查
   ✅ import 语句完整
   ✅ 包路径正确
   
示例：
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-core</artifactId>
    <version>1.8.6</version>  ✅ 版本号正确
</dependency>

import com.alibaba.csp.sentinel.SphU;  ✅ 导入正确
import com.alibaba.csp.sentinel.Entry;  ✅ 导入正确
```

#### 2.3 配置方法

```markdown
检查配置方法：

✅ 可行：
# application.properties
spring.sentinel.transport.port=8719
spring.sentinel.dashboard.server=localhost:8080

验证：
- 配置项存在
- 配置值正确
- 配置路径正确
```

#### 2.4 原理描述

```markdown
检查原理描述：

Sentinel 原理：
✅ 正确："Sentinel 通过 SlotChain 责任链实现，每个 ProcessorSlot 负责一个功能"
❌ 错误："Sentinel 通过消息队列实现限流"

检查点：
- 架构描述准确
- 流程描述正确
- 无技术性错误
```

### 通过标准

全部检查项通过 → ✅ 通过  
有 1 项未通过 → ❌ 返回 Phase 3

---

## 3. 场景连贯性检查

### 检查项

- [ ] 核心场景贴切易懂
- [ ] 示例符合场景设定
- [ ] 类比恰当不牵强
- [ ] 场景转换自然
- [ ] 场景细节真实

### 检查方法

#### 3.1 场景贴切度

```markdown
检查场景是否贴切：

技术：Sentinel（限流降级）
场景：电商下单

✅ 贴切：
- 电商大促有突发流量
- 需要限流保护服务
- 需要降级保证核心流程
- 场景真实可信

❌ 不贴切：
- 个人博客访问（流量太小）
- 内部管理系统（无突发流量）
```

#### 3.2 示例一致性

```markdown
检查示例是否符合场景：

场景：电商下单

✅ 一致：
- 订单服务限流
- 库存扣减降级
- 支付超时处理

❌ 不一致：
- 用户登录限流（场景不符）
- 文章发布降级（场景不符）
```

#### 3.3 类比恰当性

```markdown
检查类比是否恰当：

Sentinel 类比：

✅ 恰当：
"Sentinel 就像交通路口的红绿灯，控制车辆通行节奏，
防止路口拥堵瘫痪"
- 限流 = 红绿灯控制
- 服务 = 车辆
- 拥堵 = 服务雪崩

❌ 不恰当：
"Sentinel 就像一个过滤器"
- 过于抽象
- 不体现限流特性
- 没有场景感
```

#### 3.4 场景转换

```markdown
检查场景转换是否自然：

✅ 自然：
"在实际电商场景中，限流只是第一步。
当流量超过阈值时，我们还需要降级非核心服务..."

❌ 不自然：
"现在我们来讲讲降级。
降级是 Sentinel 的另一个功能..."
```

### 通过标准

全部检查项通过 → ✅ 通过  
有 1 项未通过 → ❌ 返回 Phase 3

---

## 4. 代码示例完整性检查

### 检查项

- [ ] 代码可直接运行
- [ ] 包含必要注释说明
- [ ] 有完整上下文
- [ ] 关键步骤不缺失
- [ ] 异常处理完整

### 检查方法

#### 4.1 可运行性

```markdown
检查代码是否可运行：

✅ 完整：
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-core</artifactId>
    <version>1.8.6</version>
</dependency>

import com.alibaba.csp.sentinel.SphU;
import com.alibaba.csp.sentinel.Entry;
import com.alibaba.csp.sentinel.slots.block.BlockException;

public class OrderService {
    public void createOrder() {
        // 定义资源
        try (Entry entry = SphU.entry("OrderService")) {
            // 业务逻辑
            System.out.println("订单创建成功");
        } catch (BlockException e) {
            // 限流降级
            System.out.println("订单服务被限流");
        }
    }
}

验证：
✅ 依赖完整
✅ import 完整
✅ 代码语法正确
✅ 可直接编译运行
```

#### 4.2 注释完整性

```markdown
检查注释是否充分：

✅ 充分：
// 定义资源，"OrderService" 是资源名称
try (Entry entry = SphU.entry("OrderService")) {
    // 被保护的业务逻辑
    System.out.println("订单创建成功");
} catch (BlockException e) {
    // 当触发限流、降级时进入此分支
    System.out.println("订单服务被限流");
}

❌ 不充分：
try (Entry entry = SphU.entry("OrderService")) {
    System.out.println("订单创建成功");
} catch (BlockException e) {
    System.out.println("订单服务被限流");
}
```

#### 4.3 上下文完整

```markdown
检查代码上下文：

✅ 完整：
// 1. 添加依赖
<dependency>
    <groupId>com.alibaba.csp</groupId>
    <artifactId>sentinel-core</artifactId>
    <version>1.8.6</version>
</dependency>

// 2. 导入类
import com.alibaba.csp.sentinel.SphU;

// 3. 定义资源
try (Entry entry = SphU.entry("OrderService")) {
    // 业务逻辑
}

❌ 不完整：
// 直接给出代码，没有依赖和导入
try (Entry entry = SphU.entry("OrderService")) {
    // 业务逻辑
}
```

#### 4.4 异常处理

```markdown
检查异常处理：

✅ 完整：
try (Entry entry = SphU.entry("OrderService")) {
    // 业务逻辑
} catch (BlockException e) {
    // 限流降级处理
    fallback();
} catch (Exception e) {
    // 其他异常处理
    handleError(e);
} finally {
    // 清理资源
    cleanup();
}

❌ 不完整：
try (Entry entry = SphU.entry("OrderService")) {
    // 业务逻辑
} catch (BlockException e) {
    // 仅处理限流，未处理其他异常
}
```

### 通过标准

全部检查项通过 → ✅ 通过  
有 1 项未通过 → ❌ 返回 Phase 3

---

## 📊 检查报告模板

```markdown
# Review 检查报告

**文档**：{文档名称}
**检查时间**：{YYYY-MM-DD HH:mm:ss}

---

## 1. 内容逻辑一致性

**状态**：✅ 通过 / ❌ 未通过

**详细说明**：
- 章节递进关系：✅ 通过 - 因果递进清晰
- 场景贯穿：✅ 通过 - 电商场景贯穿全文
- 技术引入：✅ 通过 - 自然引入 Sentinel
- 逻辑链条：✅ 通过 - 完整无断裂

---

## 2. 技术准确性

**状态**：✅ 通过 / ❌ 未通过

**详细说明**：
- 技术定义：✅ 通过 - 定义准确
- 代码示例：✅ 通过 - 语法正确，依赖完整
- 配置方法：✅ 通过 - 配置项正确
- 原理描述：✅ 通过 - 架构描述准确
- 版本信息：✅ 通过 - 版本号正确

---

## 3. 场景连贯性

**状态**：✅ 通过 / ❌ 未通过

**详细说明**：
- 场景贴切度：✅ 通过 - 电商场景贴切
- 示例一致性：✅ 通过 - 示例符合场景
- 类比恰当性：✅ 通过 - 红绿灯类比恰当
- 场景转换：✅ 通过 - 转换自然
- 场景细节：✅ 通过 - 细节真实

---

## 4. 代码示例完整性

**状态**：✅ 通过 / ❌ 未通过

**详细说明**：
- 可运行性：✅ 通过 - 代码可直接运行
- 注释完整性：✅ 通过 - 关键步骤有注释
- 上下文完整：✅ 通过 - 依赖、导入完整
- 关键步骤：✅ 通过 - 无缺失
- 异常处理：✅ 通过 - 异常处理完整

---

## 总结

**检查结果**：✅ 全部通过 / ❌ 有未通过项

**未通过项**（如有）：
- [检查项]：[详细说明]

**建议**：
- [修改建议]

**下一步**：
- ✅ 全部通过 → 输出初稿文档
- ❌ 有未通过 → 返回 Phase 3 重新写作
```

---

## ✅ 使用指南

### 自动检查

```markdown
Phase 4 完成后，自动执行 Review 检查：

1. 按顺序执行 4 个检查项
2. 每项检查所有子项
3. 生成检查报告
4. 判断是否全部通过
5. 输出检查结果
```

### 人工复核

```markdown
系统自动检查完成后，用户可人工复核：

1. 查看检查报告
2. 确认检查结果
3. 如有疑问，手动修改
4. 重新触发 Review
```

---

**最后更新**：2026-05-14  
**版本**：5.0.0
