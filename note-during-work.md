# 笔记

---


## HTML CSS

#####  H5样式预设代码

    *{outline: none;}
    .post,aside,details,figcaption,figure,
    footer,header,hgroup,menu,nav,section{
        display:block;
    }
    ol,ul{
        list-style:none;
    }
    blockquote,q{
        quotes:none;
    }
    blockquote:before,blockquote:after,
    q:before,q:after{
        content:'';
        content:none;
    }
    table{
        border-collapse:collapse;
        border-spacing:0;
    }
    a{
        text-decoration:none;
    }
    img{
        max-width:100%;
    }
    html{
        font-size: 625%;
    }

##### 换行自动变成省略号 

    <style>
        .bhhslh{
        white-space:nowrap;
        overflow:hidden;
        text-overflow: ellipsis;
        }
    </style>    

    <div class="bhhslh">一句话：强制段落的文本不换行（满足条目列表的单行显示），超过部分隐藏不显示，隐藏部分采用省略号。一句话：强制段落的文本不换行（满足条目列表的单行显示），超过部分隐藏不显示，隐藏部分采用省略号。一句话：强制段落的文本不换行（满足条目列表的单行显示），超过部分隐藏不显示，隐藏部分采用省略号。一句话：强制段落的文本不换行（满足条目列表的单行显示），超过部分隐藏不显示，隐藏部分采用省略号。</div>


---

## JS 代码

##### 解析URL获取参数

    function getParameterByName(name, url) {
            if (!url)
                url = window.location.href;
            name = name.replace(/[\[\]]/g, "\\$&");
            var regex = new RegExp("[?&]" + name + "(=([^&#]*)|&|#|$)"), results = regex
                    .exec(url);
            if (!results)
                return null;
            if (!results[2])
                return '';
            return decodeURIComponent(results[2].replace(/\+/g, " "));
        }

jquery:

    function getUrlParam(na) {
    var reg = new RegExp("[?&]" + na + "(=([^&#]*)|&|#|$)"); //构造一个含有目标参数的正则表达式对象
    var r = window.location.href.substr(1).match(reg);  //匹配目标参数
    if (r != null) return decodeURI(r[2]);
    return null; //返回参数值
    }

##### 校验手机号码

    function isMobile(v) {
            /*
                    　　中国移动号段 1340-1348 135 136 137 138 139 150 151 152 157 158 159 187 188 147 182
                    　　中国联通号段 130 131 132 155 156 185 186 145
                    　　中国电信号段 133 1349 153 180 181 189
             */
            var cm = "134,135,136,137,138,139,150,151,152,157,158,159,187,188,147,182,183,184,178", cu = "130,131,132,155,156,185,186,145", ct = "133,153,180,181,189,177", v = v
                    || "", h1 = v.substring(0, 3), h2 = v.substring(0, 4), v = (/^1\d{10}$/)
                    .test(v) ? (cu.indexOf(h1) >= 0 ? "联通"
                    : (ct.indexOf(h1) >= 0 ? "电信" : (h2 == "1349" ? "电信" : (cm
                            .indexOf(h1) >= 0 ? "移动" : "未知")))) : false;
            /*首先找是否联通，然后查找是否电信，然后在移动中查找‘1349’为电信，最后在移动中查找 */
            return v;
        }

##### 加减乘除
    
    /**
     * * 加法函数，用来得到精确的加法结果 *
     * 说明：javascript的加法结果会有误差，在两个浮点数相加的时候会比较明显。这个函数返回较为精确的加法结果。 *
     * 调用：accAdd(arg1,arg2) * 返回值：arg1加上arg2的精确结果
     */
    accAdd: function (arg1, arg2) {
        var r1, r2, m, c;
        try {
            r1 = arg1.toString().split(".")[1].length;
        } catch (e) {
            r1 = 0;
        }
        try {
            r2 = arg2.toString().split(".")[1].length;
        } catch (e) {
            r2 = 0;
        }
        c = Math.abs(r1 - r2);
        m = Math.pow(10, Math.max(r1, r2));
        if (c > 0) {
            var cm = Math.pow(10, c);
            if (r1 > r2) {
                arg1 = Number(arg1.toString().replace(".", ""));
                arg2 = Number(arg2.toString().replace(".", "")) * cm;
            } else {
                arg1 = Number(arg1.toString().replace(".", "")) * cm;
                arg2 = Number(arg2.toString().replace(".", ""));
            }
        } else {
            arg1 = Number(arg1.toString().replace(".", ""));
            arg2 = Number(arg2.toString().replace(".", ""));
        }
        return (arg1 + arg2) / m;
    
    },
    /**
     ** 减法函数，用来得到精确的减法结果
     ** 说明：javascript的减法结果会有误差，在两个浮点数相减的时候会比较明显。这个函数返回较为精确的减法结果。
     ** 调用：accSub(arg1,arg2)
     ** 返回值：arg1加上arg2的精确结果
     **/
    accSub: function (arg1, arg2) {
        var r1, r2, m, n;
        try {
            r1 = arg1.toString().split(".")[1].length;
        } catch (e) {
            r1 = 0;
        }
        try {
            r2 = arg2.toString().split(".")[1].length;
        } catch (e) {
            r2 = 0;
        }
        m = Math.pow(10, Math.max(r1, r2)); /*last modify by deeka*/
        n = (r1 >= r2) ? r1 : r2;
        return ((arg1 * m - arg2 * m) / m).toFixed(n);
    },
    /**
     ** 乘法函数，用来得到精确的乘法结果
     ** 说明：javascript的乘法结果会有误差，在两个浮点数相乘的时候会比较明显。这个函数返回较为精确的乘法结果。
     ** 调用：accMul(arg1,arg2)
     ** 返回值：arg1乘以 arg2的精确结果
     **/
    accMul: function (arg1, arg2) {
        var m = 0,
            s1 = arg1.toString(),
            s2 = arg2.toString();
        try {
            m += s1.split(".")[1].length;
        } catch (e) {}
        try {
            m += s2.split(".")[1].length;
        } catch (e) {}
        return Number(s1.replace(".", "")) * Number(s2.replace(".", "")) / Math.pow(10, m);
    },
    /** 
     ** 除法函数，用来得到精确的除法结果
     ** 说明：javascript的除法结果会有误差，在两个浮点数相除的时候会比较明显。这个函数返回较为精确的除法结果。
     ** 调用：accDiv(arg1,arg2)
     ** 返回值：arg1除以arg2的精确结果
     **/
    accDiv: function (arg1, arg2) {
        var t1 = 0,
            t2 = 0,
            r1, r2;
        try {
            t1 = arg1.toString().split(".")[1].length;
        } catch (e) {}
        try {
            t2 = arg2.toString().split(".")[1].length;
        } catch (e) {}
        with(Math) {
            r1 = Number(arg1.toString().replace(".", ""));
            r2 = Number(arg2.toString().replace(".", ""));
            return (r1 / r2) * pow(10, t2 - t1);
        }
    },
    toDecimal2: function (x) {
        var f = parseFloat(x);
        if (isNaN(f)) {
            return false;
        }
        var f = Math.round(x * 100) / 100;
        var s = f.toString();
        var rs = s.indexOf('.');
        if (rs < 0) {
            rs = s.length;
            s += '.';
        }
        while (s.length <= rs + 2) {
            s += '0';
        }
        return s;
    },

##### localStorage in es6

    const STORAGE_KEY = "todolist";
    export default {
        setStorage : function(items){
            window.localStorage.setItem(STORAGE_KEY, JSON.stringify(items))
        },
        getStorage : function(){
            return JSON.parse(window.localStorage.getItem(STORAGE_KEY)|| "[]")
        }
    }

##### iframe与父的互相刷新

    //iframe刷新父:
    //TODO:相对于top的话, 这个有点不太理解, 按道理parent是找到当前iframe的父元素, 那刷新情况是否要考虑该父元素是否存在src属性?
    parent.window.location.href="url";


下面是抄来的, 均未经测试

    第一种方法:用iframe的name属性定位
    <input type="button" name="Button" value="Button" onclick="document.frames('ifrmname').location.reload()">
    或者
    <input type="button" name="Button" value="Button" onclick="document.all.ifrmname.document.location.reload()">
    第二种方法:用iframe的id属性定位
    <input type="button" name="Button" value="Button" onclick="ifrmid.window.location.reload()">
    第三种方法:当iframe的src为其它网站地址(即跨域操作时)
    <input type="button" name="Button" value="Button" onclick="window.open(document.all.ifrmname.src,'ifrmname','')">
    父页面中存在两个iframe，一个iframe中是一个链接列表，其中的链接指向另一个iframe，用于显示内容。现在当内容内容添加后，在链接列表中添加了一条记录，则需要刷新列表iframe。
    在内容iframe的提交js中使用parent.location.reload()将父页面全部刷新，因为另一个iframe没有默认的url，只能通过列表选择，所以只显示了列表iframe的内容。
    使用window.parent.frames["列表iframe名字"].location="列表url"即可进刷新列表iframe，而内容iframe在提交后自己的刷新将不受影响。
    document.frames("refreshAlarm").location.reload(true);
    document.frames("refreshAlarm").document.location.reload(true);
    document.frames("refreshAlarm").document.location="http://www.phpernote.com/";
    document.frames("refreshAlarm").src="http://www.phpernote.com/";
    注意区别：document.all.refreshAlarm 或 document.frames("refreshAlarm") 得到的是http://www.phpernote.com/页面中那个iframe标签，所以对src属性操作有用。
    document.frames("refreshAlarm").document得到iframe里面的内容，也就是"http://www.phpernote.com/"中的内容。
    javascript(js)自动刷新页面的实现方法总结:
    间隔10秒刷新一次，在页面的head标签中加入下面的代码段：
    <meta http-equiv="refresh"content="10;url=跳转的页面或者是需要刷新的页面URL地址">
    定时刷新页面（间隔2秒刷新一下页面）：
    <script language="javascript">
    setTimeout("location.href='url'",2000);//url是要刷新的页面URL地址
    </script>
    直接刷新页面事件：
    <script language="javascript">
    window.location.reload(true);
    //如需刷新iframe，则只需把window替换为响应的iframe的name属性值或ID属性值
    </script>
    直接刷新页面事件：
    <script language=''javascript''>
    window.navigate("本页面url");
    </script>
    直接刷新页面事件：
    function abc(){
    window.location.href="/blog/window.location.href";
    setTimeout("abc()",10000);
    }
    刷新框架页：
    <script language="javascript">
    top.leftFrm.location.reload();
    parent.frmTop.location.reload();
    </script>

##### url及ajax相关

    function getBaseURL() {
        return window.location.host;
    }

    function get(url, params, callback) {
        ajax(url, params, callback, "GET");
    }

    function post(url, params, callback) {
        ajax(url, params, callback, "POST");
    }

    function ajax(url, params, callback, type, isAsync) {
        $.ajax({
            url : url,
            data : params,
            type : type ? type : "POST",
            async : isAsync == null ? true : isAsync,
            success : function(data) {
                if (data && data.code == UnAuthCode) {//这里可以搞一些类似权限控制的公共方法
                    alert(data.msg);
                } else {
                    callback(data);
                }
            }
        });
    }

---

## 框架

##### 模板插件dot.js

[dot.js](http://olado.github.io/doT/index.html)

简单用法: 

    var tempFn = doT.template("<h1>Here is a sample template {{=it.foo}}</h1>");
    var resultText = tempFn({foo: 'with doT'});

js:
    
    //数据和dom独立
    //首先初始化模板
    var evalText = doT.template($("#template-id").html());
    //再将数据插入模板
    $list.append(evalText(data));

html常用绑定语法:

    //赋值 : 
    <div>Hi {{=it.name}}!</div>
    <div>{{=it.age || ''}}</div>
    //遍历 :
    {{ for(var prop in it) { }}
    <div>{{=prop}}</div>
    {{ } }}
    //条件判断 : 
    {{? it.name }}
    <div>Oh, I love your name, {{=it.name}}!</div>
    {{?? it.age === 0}}
    <div>Guess nobody named you yet!</div>
    {{??}}
    You are {{=it.age}} and still don't have a name?
    {{?}}
    //数组 :
    {{~it.array :value:index}}
    <div>{{=value}}!</div>
    {{~}}

数据在进入模板前每一项必须初始化.
在项目中使用了过多的无意义条件判断, 在对象值不存在的情况下只需要{{=it.age || ''}}即可

##### jq-formatCurrency 基于jq的货币格式化插件

    $("#elementId").formatCurrency();

可配置项:

    symbol: '',
    positiveFormat: '%s%n',
    negativeFormat: '(%s%n)',
    decimalSymbol: '.',
    digitGroupSymbol: ',',
    groupDigits: true

bug:
//TODO:
对数据进行货币格式化时, 当被格式化数字为0.040/1.020/0.09等时, 会对应被错误的格式化成0.4/1.2/0.9
可重现, 不会改

##### vue

Vuejs群资料：http://t.cn/Rb1aUQT
小凡哥Vuejs视频
http://i.youku.com/u/UMzQxOTE4MDE5Mg==
讲解 vue.js 实例
https://github.com/bhnddowinf/vuejs-learn
视频github资源
vue2.0相关文档
http://vuefe.cn/ 中文文档
http://vuejs.org/guide/ 官网原文文档
http://router.vuejs.org/zh-cn/index.html vue-router2.0中文文档
http://vuex.vuejs.org/en/index.html vuex2.0 英文文档
https://github.com/bhnddowinf/vuejs2-learn v2学习项目




