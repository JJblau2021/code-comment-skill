---
name: code-comment
description: |
  为代码生成中文注释。当用户要求生成代码、实现功能、编写函数/类/模块时，
  或者需要为已有代码添加注释时调用此 skill。支持 JavaScript、TypeScript、Python、Go、Rust、Java。
  无论用户是否明确要求"加注释"，都应该在生成代码时自动添加完整的中文注释。
  触发场景包括但不限于："写一个函数"、"实现 XXX 功能"、"生成代码"、"需要注释"、
  "帮我写个 XXX"、"代码加上中文注释"等。
---

# Code Comment Skill

## 概述

此 skill 确保生成的代码包含完整、专业的中文注释。注释不仅帮助理解代码逻辑，
还能作为文档便于后续维护。

## 支持的语言

- JavaScript / TypeScript
- Python
- Go
- Rust
- Java

## 注释规范

### 1. 文件级注释

每个代码文件开头应包含：
- 文件功能描述
- 作者（可选）
- 创建日期（可选）
- 版本号（可选）

```python
# -*- coding: utf-8 -*-
"""
文件名称: user_service.py
功能描述: 用户服务层，负责用户注册、登录、信息管理等核心业务逻辑
创建日期: 2024-01-15
"""
```

```javascript
/**
 * 文件名称: user_service.js
 * 功能描述: 用户服务层，负责用户注册、登录、信息管理等核心业务逻辑
 * 创建日期: 2024-01-15
 */
```

### 2. 函数/方法级注释

每个函数/方法必须包含 JSDoc/DocString 风格的注释，说明：
- **功能**：函数做什么
- **参数**：每个参数的名称、类型、含义
- **返回值**：返回值的类型和含义
- **示例**：重要函数提供使用示例

```python
def calculate_user_score(user_id: int, activity_weight: float = 1.0) -> float:
    """
    计算用户综合评分
    
    根据用户的各项活动数据计算一个综合评分，用于推荐系统和排行榜展示。
    
    Args:
        user_id: 用户的唯一标识符
        activity_weight: 活动权重系数，默认为 1.0，范围 0.0-2.0
    
    Returns:
        float: 返回 0-100 之间的综合评分，数值越高表示用户越活跃
    
    Example:
        >>> score = calculate_user_score(12345, 1.5)
        >>> print(f"用户评分为: {score}")
    """
    # 实现代码...
```

```javascript
/**
 * 计算用户综合评分
 * 
 * 根据用户的各项活动数据计算一个综合评分，用于推荐系统和排行榜展示。
 * 
 * @param {number} userId - 用户的唯一标识符
 * @param {number} [activityWeight=1.0] - 活动权重系数，范围 0.0-2.0
 * @returns {number} 返回 0-100 之间的综合评分
 * 
 * @example
 * const score = calculateUserScore(12345, 1.5);
 * console.log(`用户评分为: ${score}`);
 */
function calculateUserScore(userId, activityWeight = 1.0) {
    // 实现代码...
}
```

### 3. 关键代码行注释

对于以下类型的代码行，必须添加注释：
- **业务逻辑关键点**：解释"为什么"而不是"是什么"
- **复杂条件判断**：解释判断条件的含义
- **循环中的重要操作**：解释循环目的
- **异常处理**：解释捕获异常的原因
- **重要的状态变更**：解释变更的原因和影响

```python
# 当用户连续登录超过 7 天时，额外增加活跃度奖励
# 这是为了鼓励用户保持连续登录习惯
if consecutive_days > 7:
    bonus += base_score * 0.2  # 20% 的额外奖励
    
# 注意：这里使用 UTC 时间避免时区问题
# 因为用户的本地时间可能与服务器时间不一致
created_at = datetime.now(timezone.utc)
```

### 4. 类/结构体注释

```python
class UserProfile:
    """
    用户画像类
    
    存储用户的核心信息和行为数据，用于个性化推荐和用户分析。
    该类是不可变的（immutable），创建后不允许修改内部数据。
    
    Attributes:
        user_id: 用户唯一标识
        username: 用户名，用于显示和社交功能
        email: 用户邮箱，用于验证和通知
        created_at: 账户创建时间
        preferences: 用户偏好设置字典
    
    Example:
        >>> profile = UserProfile(123, "zhangsan", "zhangsan@example.com")
        >>> print(profile.username)
        zhangsan
    """
```

## 注释风格原则

### Do（应该做）

✅ **解释意图**：说明代码想要达成什么目标
```python
# 当订单金额超过 99 元时免运费，鼓励用户增加消费
if order_amount > 99:
    shipping_fee = 0
```

✅ **解释复杂逻辑**：用简单的语言解释复杂判断
```python
# 判断是否为闰年：能被 4 整除但不能被 100 整除，或者能被 400 整除
is_leap = (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)
```

✅ **解释非常规做法**：说明为什么用非直觉的方式实现
```python
# 使用位运算而非乘除法，提升计算性能约 3 倍
# 在高频调用场景下这种优化是值得的
shifted_value = original_value >> 1  # 除以 2
```

✅ **使用中文标点**：保持注释的专业性和可读性
```python
# 完成用户验证后，将用户状态标记为已激活
```

### Don't（不应该做）

❌ **不要翻译代码**：不要给显而易见的代码加注释
```python
# 错误示例
i += 1  # i 加 1
```

❌ **不要用英文注释**：保持一致性，全部使用中文
```python
# 错误示例
# loop through the list
```

❌ **不要留空注释**：不要写空的或无意义的注释占位
```python
# 错误示例
# TODO: implement this later
# 这里稍后实现
```

## 注释密度指南

| 代码类型 | 注释密度 | 说明 |
|---------|---------|------|
| 业务逻辑核心 | 高 | 每 3-5 行有一个注释 |
| 数据处理/算法 | 高 | 关键步骤都有注释 |
| 工具函数 | 中 | 重要步骤有注释 |
| 简单赋值/调用 | 低 | 必要时注释 |
| 配置文件 | 中 | 配置项含义都注释 |

## 输出要求

生成代码时：
1. 首先输出文件级注释
2. 然后是类/函数定义及注释
3. 最后是实现代码，关键行有行内注释
4. 保持注释与代码的适当比例（建议 1:4 到 1:3）
5. 确保所有注释都是中文，包含中文标点

## 示例：完整带注释的代码

```python
# -*- coding: utf-8 -*-
"""
文件名称: order_processor.py
功能描述: 订单处理模块，负责订单创建、支付、取消等全生命周期管理
"""

from datetime import datetime, timezone
from typing import Optional, List
from enum import Enum


class OrderStatus(Enum):
    """
    订单状态枚举
    
    定义订单在整个生命周期中的所有可能状态。
    """
    PENDING = "pending"      # 待支付
    PAID = "paid"            # 已支付
    SHIPPED = "shipped"       # 已发货
    COMPLETED = "completed"   # 已完成
    CANCELLED = "cancelled"  # 已取消


class OrderProcessor:
    """
    订单处理器类
    
    负责处理订单的核心业务逻辑，包括创建订单、计算价格、处理支付等。
    该类是线程安全的，可用于高并发的订单处理场景。
    """
    
    def __init__(self, tax_rate: float = 0.13):
        """
        初始化订单处理器
        
        Args:
            tax_rate: 税率，默认为 13%（中国增值税率）
        """
        self.tax_rate = tax_rate
        self.orders: List[dict] = []  # 存储所有订单的列表
    
    def create_order(self, user_id: int, items: List[dict], 
                     shipping_address: str) -> dict:
        """
        创建新订单
        
        验证商品信息，计算总价，生成订单并存储。
        
        Args:
            user_id: 下单用户的唯一标识
            items: 商品列表，每个商品包含 id、name、price、quantity
            shipping_address: 收货地址，格式为省市区详细地址
        
        Returns:
            dict: 创建成功的订单对象，包含 order_id、total_amount 等字段
        
        Raises:
            ValueError: 当商品列表为空或用户 ID 无效时抛出
        """
        # 参数校验：确保商品列表不为空
        if not items:
            raise ValueError("商品列表不能为空")
        
        # 生成唯一订单 ID：使用时间戳 + 用户 ID 后 4 位
        order_id = f"ORD{int(datetime.now(timezone.utc).timestamp() * 1000)}{user_id % 10000:04d}"
        
        # 计算商品总价（不含税）
        subtotal = sum(item['price'] * item['quantity'] for item in items)
        
        # 计算税额：总价 × 税率
        tax_amount = subtotal * self.tax_rate
        
        # 计算最终金额：商品总价 + 税额 + 运费（满 99 免运费）
        shipping_fee = 0 if subtotal > 99 else 10
        total_amount = subtotal + tax_amount + shipping_fee
        
        # 构建订单对象
        order = {
            'order_id': order_id,
            'user_id': user_id,
            'items': items,
            'shipping_address': shipping_address,
            'subtotal': subtotal,       # 商品总价（不含税）
            'tax_amount': tax_amount,   # 税额
            'shipping_fee': shipping_fee,  # 运费
            'total_amount': total_amount,  # 最终金额
            'status': OrderStatus.PENDING.value,
            'created_at': datetime.now(timezone.utc).isoformat()
        }
        
        # 存储订单
        self.orders.append(order)
        
        return order
```
