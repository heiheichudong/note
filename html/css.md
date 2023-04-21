# Css

#### 语法：

> 位置

- 内联样式：

```
<div style="color: fuchsia"></div>
```

- style标签内：

```
<style>
  p{
  color: blue;
  }
  </style>
```

- 外部：

```
<link rel="stylesheet" href="cssImport.css">
```
> 基本语法
- 选择器 声明块
- 元素选择器 p{} h1{} div{}等
- id选择器 #id{}
- class选择器 .class{}
- 复合选择器 
  - 交集选择器 div.class
  - 并集选择器 div,span,class,class,....
- 关系选择器
  - 父子