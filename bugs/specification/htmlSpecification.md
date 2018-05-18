#### input没有闭合标签
> 通过用图片覆盖radio实现改变radio默认样式
> 是有人把伪类元素家在了input上了
> 我把这个伪类元素改到label上了，调好上线
- chrome
![](images/input_bug.png)
> 
![](images/input_bug1.png)
```
:before//是加在一个元素内部的，而input没有闭合标签，chrome可以识别，给其自动加了，而ie、firfox不能
```
#### 闭合标签写错