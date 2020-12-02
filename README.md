# Ace is an embeddable code editor written in JavaScript.

https://github.com/ajaxorg/ace

## iframe使用

``` 

<iframe class="ace-editor" id="ace-editor" src="https://ace520.github.io/ace/" frameborder="no" border="0" marginwidth="0"   marginheight="0" scrolling="no" allowtransparency="yes"></iframe>
```

* GET参数设置主题、字体大小、语言、是否只读

``` 

https://ace520.github.io/ace?theme=twilight&fontSize=16&mode=javascript&readOnly=false

* theme
* fontSize
* mode
* readOnly

```

* JS设置内容、获取内容、监听内容变化

``` 

<script>
    var aceIframeWin = document.getElementById("ace-editor").contentWindow;
    setTimeout(function () {
        //设置内容
        aceIframeWin.postMessage({
            method: 'setValue',
            content: '123'
        }, "*");
        //获取内容
        aceIframeWin.postMessage({
            method: 'getValue'
        }, "*");

        //监听子页面返回
        window.addEventListener("message", function (event) {
            let data = event.data;
            switch (data.method) {
                case 'setValue': //设置内容返回
                    console.log(data.content);
                    break;
                case 'getValue': //获取内容返回
                    console.log(data.content);
                    break;
                case 'change': //内容改变返回
                    console.log(data.content);
                    break;
            }
        }, false);
    }, 100);
</script>
```
