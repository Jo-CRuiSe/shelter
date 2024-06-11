---
title: 使用 SwfitUI 来做仿做一个原生计算器
date: 2024-05-21 14:01:00 +0800
categories: [SwiftUI]
tags: []
pin: false
unpublished: true
author: jo
toc: true
commments: true
typora-root-url: ../../Jo-CRuiSe.github.io/
math: false
mermaid: false
---

> Code based on [ASMR Programming - iPhone Calculator - No Talking (iOS, SwiftUI, Xcode)](https://www.youtube.com/watch?v=GZmubIUjmx4)

## Views

calcButtonView

contentsView

## ViewModel

计算器处理逻辑

### 基本运算逻辑

当栈内有内容时，<kbd>AC</kbd>显示为<kbd>C</kbd>

支持运算优先级，如果下个运算符的等级比上个低或相等，先在屏幕上显示之前计算结果；反之等待所有优先级高的运算符计算完成后再结算

### 特殊情况

除数为0，结果为`Error`

