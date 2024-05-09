---
title: SwiftUI Techniques
date: 2024-04-30 14:42:00 +0800
categories: [Notes, SwiftUI]
tags: [swiftui]
pin: false
author: jo
toc: true
commments: true
typora-root-url: ../../Jo-CRuiSe.github.io/
math: false
mermaid: false
---

## 如何使用`@EnvironmentObjects`

在 view model 中添加`@Published`，例如：

```swift
@Published var data: String
```

再在父级页面定义：

```swift
@StateObject var viewModel: EnvironmentViewModel
```

在父级的`NavigationView`下加入`.environmentObject()`，如：

```swift
NavigationView{

}
.environmentObject(viewModel)
```

在需要使用该变量的子页中声明：

```swift
@EnvironmentObject var viewModel: EnvironmentViewModel
```

这样就可以在子界面中使用`viewModel`访问环境变量了