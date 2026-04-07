# Code Comment Skill

## 概述

`code-comment` 是一个代码注释生成技能。当生成代码时自动调用，为代码添加完整、专业的中文注释。

## 功能特点

- **多语言支持**：JavaScript、TypeScript、Python、Go、Rust、Java
- **完整注释体系**：文件级注释、类/函数级注释、关键代码行注释
- **中文优先**：所有注释使用中文，包含中文标点
- **开箱即用**：生成代码时自动触发，无需手动调用

## 注释规范

### 1. 文件级注释

每个代码文件开头包含：
- 文件名称
- 功能描述
- 创建日期

### 2. 函数/方法级注释

使用 JSDoc/DocString 风格，包含：
- **功能说明**：函数的作用
- **参数说明**：每个参数的名称、类型、含义
- **返回值**：返回值的类型和含义
- **示例**：重要函数提供使用示例

### 3. 关键代码行注释

对以下代码添加注释：
- 业务逻辑关键点
- 复杂条件判断
- 异常处理
- 重要状态变更

## 支持的语言

| 语言 | 文件类型 |
|------|---------|
| JavaScript | `.js` |
| TypeScript | `.ts` `.tsx` |
| Python | `.py` |
| Go | `.go` |
| Rust | `.rs` |
| Java | `.java` |

## 使用场景

- 生成新代码时自动添加注释
- 实现功能时自动添加注释
- 编写函数/类/模块时自动添加注释

## 示例

**Python 示例：**

```python
# -*- coding: utf-8 -*-
"""
文件名称: user_service.py
功能描述: 用户服务层，负责用户注册、登录、信息管理等核心业务逻辑
创建日期: 2024-01-15
"""

def calculate_user_score(user_id: int, activity_weight: float = 1.0) -> float:
    """
    计算用户综合评分
    
    根据用户的各项活动数据计算一个综合评分，用于推荐系统和排行榜展示。
    
    Args:
        user_id: 用户的唯一标识符
        activity_weight: 活动权重系数，默认为 1.0
    
    Returns:
        float: 返回 0-100 之间的综合评分
    """
    # 获取用户活动数据
    activities = get_user_activities(user_id)
    
    # 根据权重计算评分
    score = sum(a['value'] * activity_weight for a in activities)
    
    return min(score, 100)  # 评分上限为 100
```

**TypeScript 示例：**

```typescript
/**
 * 文件名称: task_queue.ts
 * 功能描述: 任务队列类实现，提供基本的队列操作功能
 */

/**
 * 任务队列类
 * 
 * 基于数组实现的简单任务队列，支持入队、出队和判空操作。
 */
export class TaskQueue<T> {
    /**
     * 入队操作
     * 
     * 将新元素添加到队列的尾部。
     * 
     * @param {T} element - 要添加的元素
     * @returns {number} 返回入队后队列的新长度
     */
    public enqueue(element: T): number {
        this.items.push(element);
        return this.items.length;
    }
}
```

## 安装

将此技能添加到你的 Sisyphus 配置中即可使用。

## 触发方式

以下场景会自动触发：
- "写一个函数"
- "实现 XXX 功能"
- "生成代码"
- "帮我写个 XXX"
- 任何代码生成请求
