---
title: Spline灯光使用方法
date: 2024-02-10 22:45:00 +0800
categories: [Notes, Spline]
tags: []
pin: false
author: jo
toc: true
commments: true
typora-root-url: ../../Jo-CRuiSe.github.io/
math: false
mermaid: false
---

## 光源

### 平行光

1. 特点：没有衰减，永远指向原点

2. 属性：

   - 颜色
   - 强度
   - 阴影
   - 助手
   - 尺寸
   - 深度：光线照射距离，越小性能消耗越低

   
### 点光源

属性：

   - 颜色
   - 强度
   - 距离
   - 衰减
   - 阴影
   - 阴影分辨率
   - 半径：不能实现弥散效果
   - 助手
   - 深度

### 聚光灯

属性：

   - 颜色
   - 强度
   - 距离
   - 角度
   - 柔和
   - 衰减
   - 阴影
   - 助手
   - 尺寸
   - 深度

## 灯光材质

**不可删除**

### 无

不接受任何灯光

### 漫反射（Lambert）

适合混凝土、沙子

### 透光（Phong）

相对真实，光照强度越强，高光越明显，适合塑料和皮肤

### 自然（Physical）

既可以实现透光效果，也可以实现金属效果

### 卡通（Toon）

渲染是一层层的
