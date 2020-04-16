

问题报错：Uncaught TypeError: $(...).on is not a function

问题分析：jQuery版本的问题，因为老版本的jQuery中不支持on方法，可以用bind方法代替

解决方案：

```jQuery
$("#CurType").bind("change", function () {
})

替代
$("#CurType").on("change", function () {
})
```

