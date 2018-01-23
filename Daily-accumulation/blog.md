
     
    
### 积累
> 判定元素是否滚动到底

如果元素滚动到底，下面等式返回true，没有则返回false.

```
element.scrollHeight - element.scrollTop === element.clientHeight
```

>  超出部分以 ... 显示
```
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;
display: inline-block;
width: 100%;
```
> 截取 url  
```
var getUrlRelativePath = function() {　　　　
    var url = document.location.toString(); //http://sdk.com/admin/app/addApp?mean=addApp&from=app　　　　
    var arrUrl = url.split("//"); //["http:", "sdk.com/admin/app/addApp?mean=addApp&from=app"]　　
    var start = arrUrl[1].indexOf("/");//7　　　　
    var relUrl = arrUrl[1].substring(start); // /admin/app/addApp?mean=addApp&from=app
    if (relUrl.indexOf("?") != -1) {　　　　　　
        relUrl = relUrl.split("?")[0];　　　　
    }
    return relUrl.split('/', 4).join('/'); // /admin/app/addApp
};
```
#### 轮流点击元素
```
    var elCover = document.getElementById('cover');
    var arrElTarget = [
        document.getElementsByTagName('a')[0], 
        document.getElementById('backTo'), 
        document.getElementById('image')
    ], index = 0;

    coverGuide(elCover, arrElTarget[index]);

    elCover.onclick = function() {
        index++;
        if (!arrElTarget[index]) {
            index = 0;    
        }
        coverGuide(elCover, arrElTarget[index]);
    };
```


 
