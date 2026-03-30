# Career Tracker 项目说明

## 项目概述

P7后端开发求职准备追踪系统，单文件 HTML 应用，部署在 Vercel。

**GitHub**: https://github.com/horizon6666/career-tracker
**在线地址**: https://career-tracker-five.vercel.app/

## 技术架构

- **单文件应用**: `index.html` 包含所有 HTML/CSS/JS
- **状态管理**: localStorage 持久化
- **样式**: CSS 变量 + 深色科技风格
- **字体**: JetBrains Mono (代码) + Outfit (正文)

## 功能模块

### 1. LeetCode 刷题追踪 (leetcodeData)

LeetCode Hot 100，按算法分类组织：

| 分类 | 题数 |
|------|------|
| 哈希 | 3 |
| 双指针 | 4 |
| 滑动窗口 | 2 |
| 子串 | 3 |
| 普通数组 | 5 |
| 矩阵 | 4 |
| 链表 | 14 |
| 二叉树 | 16 |
| 图论 | 4 |
| 回溯 | 8 |
| 二分查找 | 6 |
| 栈 | 5 |
| 堆 | 3 |
| 贪心算法 | 4 |
| 动态规划 | 10 |
| 多维动态规划 | 5 |
| 技巧 | 5 |
| **总计** | **100** |

每题包含: `id`(题号), `name`, `difficulty`, `link`

### 2. Go技术复习 (techData)

7个分类，53个知识点：
- Go底层原理 (10)
- 分布式系统 (8)
- 微服务架构 (8)
- 消息队列 (6)
- Redis缓存 (7)
- MySQL数据库 (8)
- 系统设计方法论 (6)

### 3. 系统设计题库 (systemDesignData)

10道系统设计题，含关键词标签。

### 4. 面试准备

5个文本域：自我介绍、离职原因、职业规划、薪资期望、谈判技巧

### 5. 公司追踪 (companyData)

5家大厂：字节、阿里、腾讯、美团、快手，各有状态流程。

## 状态结构 (state)

```javascript
state = {
    targetDate: null,       // 目标日期
    leetcode: {},           // { "题目名": boolean }
    tech: {},               // { "知识点名": boolean }
    system: {},             // { "题目名": boolean }
    interview: {},          // { intro, leave, plan, salary, negotiate }
    companies: {}           // { "公司名": "状态" }
}
```

## 关键函数

| 函数 | 作用 |
|------|------|
| `saveState()` | 保存到 localStorage |
| `loadState()` | 加载状态 |
| `toggleCategory(header)` | 展开/收起分类 |
| `toggleLeetCode(name, event)` | 切换题目完成状态（需阻止事件冒泡） |
| `updateLeetCodeUI()` | 渲染刷题列表 |
| `updateLeetCodeSummary()` | 更新 sidebar 分类进度预览 |
| `switchPage(page)` | 切换页面 |

## 数据管理

- 导出: `exportData()` 下载 JSON 文件
- 导入: `importData(event)` 从 JSON 恢复

## 注意事项

- 点击题目完成时需阻止事件冒泡 (`event.stopPropagation()`)，避免触发分类收起
- sidebar 已添加分类进度预览，无需点进页面即可查看各分类进度
- 题目完成后会调用 `updateLeetCodeUI()` 刷新界面，保持分类展开状态