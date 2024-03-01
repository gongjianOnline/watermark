# 前端防删水印应用案例
[博客链接](http://gjweb.top)

## 飞书的水印方案

![](http://gjweb.top/wp-content/uploads/2024/03/%E9%A3%9E%E4%B9%A6%E6%B0%B4%E5%8D%B0-00_00_00-00_00_30-2.gif)

**问题**：当用户在F12中修改 css 为 `display:none` / `opacity: 0`或者删除元素，水印作用将失效

## 防删水印解决方案：

![](http://gjweb.top/wp-content/uploads/2024/03/%E9%98%B2%E5%88%A0%E6%B0%B4%E5%8D%B0-00_00_00-00_00_30.gif)

**思路**：利用  MutationObserver API 监听水印元素的变化，只要监听水印元素被用户操作了就手动删除重新创建水印元素

