# AJAX 基础
## AJAX 教程

AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

AJAX 不是新的编程语言，而是一种使用现有标准的新方法。

AJAX 是与服务器交换数据并更新部分网页的艺术，在不重新加载整个页面的情况下。

## AJAX 简介
**AJAX 是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术**。

AJAX = 异步 JavaScript 和 XML。

AJAX 是一种用于创建快速动态网页的技术。

通过在后台与服务器进行少量数据交换，AJAX 可以使网页实现异步更新。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

传统的网页（不使用 AJAX）如果需要更新内容，必需重载整个网页面。

## AJAX 实例



---
# AJAX XHR（XMLHttpRequest ）
## XHR 创建对象
XMLHttpRequest 是 AJAX 的基础。

【**XMLHttpRequest 对象**】

所有现代浏览器均支持 XMLHttpRequest 对象（IE5 和 IE6 使用 ActiveXObject）。

XMLHttpRequest 用于在后台与服务器交换数据。这意味着可以在不重新加载整个网页的情况下，对网页的某部分进行更新。

【**创建 XMLHttpRequest 对象**】

创建 XMLHttpRequest 对象的语法：
```
variable=new XMLHttpRequest();
```

老版本的 Internet Explorer （IE5 和 IE6）使用 ActiveX 对象：

```
variable=new ActiveXObject("Microsoft.XMLHTTP");
```

为了应对所有的现代浏览器，包括 IE5 和 IE6，请检查浏览器是否支持 XMLHttpRequest 对象。如果支持，则创建 XMLHttpRequest 对象。如果不支持，则创建 ActiveXObject ：

```
var xmlhttp;
if (window.XMLHttpRequest)
  {// code for IE7+, Firefox, Chrome, Opera, Safari
    xmlhttp=new XMLHttpRequest();
  }
else
  {// code for IE6, IE5
    xmlhttp=new ActiveXObject("Microsoft.XMLHTTP");
  }
```

## XHR 请求
**XMLHttpRequest 对象用于和服务器交换数据**。

【向服务器发送请求】

如需将请求发送到服务器，我们使用 XMLHttpRequest 对象的 open() 和 send() 方法：

```
xmlhttp.open("GET","test1.txt",true);
xmlhttp.send();
```

【GET 还是 POST？】

与 POST 相比，GET 更简单也更快，并且在大部分情况下都能用。

然而，在以下情况中，请使用 POST 请求：
- 无法使用缓存文件（更新服务器上的文件或数据库）
- 向服务器发送大量数据（POST 没有数据量限制）
- 发送包含未知字符的用户输入时，POST 比 GET 更稳定也更可靠

【GET 请求】
```
xmlhttp.open("GET","demo_get.asp",true);
xmlhttp.send();
```
在上面的例子中，您可能得到的是缓存的结果。

为了避免这种情况，请向 URL 添加一个唯一的 ID：

```
xmlhttp.open("GET","demo_get2.asp?fname=Bill&lname=Gates",true);
xmlhttp.send();
```
如果您希望通过 GET 方法发送信息，请向 URL 添加信息：
```
xmlhttp.open("GET","demo_get2.asp?fname=Bill&lname=Gates",true);
xmlhttp.send();
```

【POST 请求】


```
xmlhttp.open("POST","demo_post.asp",true);
xmlhttp.send();
```

如果需要像 HTML 表单那样 POST 数据，请使用 setRequestHeader() 来添加 HTTP 头。然后在 send() 方法中规定您希望发送的数据：

```
xmlhttp.open("POST","ajax_test.asp",true);
xmlhttp.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xmlhttp.send("fname=Bill&lname=Gates");
```

【url - 服务器上的文件】

open() 方法的 url 参数是服务器上文件的地址：
```
xmlhttp.open("GET","ajax_test.asp",true);
```
该文件可以是任何类型的文件，比如 .txt 和 .xml，或者服务器脚本文件，比如 .asp 和 .php （在传回响应之前，能够在服务器上执行任务）。

【异步 - True 或 False？】

AJAX 指的是异步 JavaScript 和 XML（Asynchronous JavaScript and XML）。

XMLHttpRequest 对象如果要用于 AJAX 的话，其 open() 方法的 async 参数必须设置为 true：
```
xmlhttp.open("GET","ajax_test.asp",true);
```

对于 web 开发人员来说，发送异步请求是一个巨大的进步。很多在服务器执行的任务都相当费时。AJAX 出现之前，这可能会引起应用程序挂起或停止。

通过 AJAX，JavaScript 无需等待服务器的响应，而是：
- 在等待服务器响应时执行其他脚本
- 当响应就绪后对响应进行处理

【Async = true】
当使用 async=true 时，请规定在响应处于 onreadystatechange 事件中的就绪状态时执行的函数：
```
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
xmlhttp.open("GET","test1.txt",true);
xmlhttp.send();
```

【Async = false】

如需使用 async=false，请将 open() 方法中的第三个参数改为 false：
```
xmlhttp.open("GET","test1.txt",false);
```

我们不推荐使用 async=false，但是对于一些小型的请求，也是可以的。

请记住，JavaScript 会等到服务器响应就绪才继续执行。如果服务器繁忙或缓慢，应用程序会挂起或停止。

注释：当您使用 async=false 时，请不要编写 onreadystatechange 函数 - 把代码放到 send() 语句后面即可：
```
xmlhttp.open("GET","test1.txt",false);
xmlhttp.send();
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```


## XHR 响应
【服务器响应】

如需获得来自服务器的响应，请使用 XMLHttpRequest 对象的 responseText 或 responseXML 属性。

属性 | 描述
---|---
responseText |获得字符串形式的响应数据。
responseXML |获得 XML 形式的响应数据。

【responseText 属性】
如果来自服务器的响应并非 XML，请使用 responseText 属性。

responseText 属性返回字符串形式的响应，因此您可以这样使用：
```
document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
```
【responseXML 属性】
如果来自服务器的响应是 XML，而且需要作为 XML 对象进行解析，请使用 responseXML 属性：

请求 books.xml 文件，并解析响应：
```
xmlDoc=xmlhttp.responseXML;
txt="";
x=xmlDoc.getElementsByTagName("ARTIST");
for (i=0;i<x.length;i++)
  {
  txt=txt + x[i].childNodes[0].nodeValue + "<br />";
  }
document.getElementById("myDiv").innerHTML=txt;
```


## XHR readyState
【onreadystatechange 事件】

当请求被发送到服务器时，我们需要执行一些基于响应的任务。

每当 readyState 改变时，就会触发 onreadystatechange 事件。

readyState 属性存有 XMLHttpRequest 的状态信息。

下面是 XMLHttpRequest 对象的三个重要的属性：

属性 | 描述
---|---
onreadystatechange |存储函数（或函数名），每当 readyState 属性改变时，就会调用该函数。
readyState |存有 XMLHttpRequest 的状态。从 0 到 4 发生变化。。<br><br>0: 请求未初始化。<br> 1: 服务器连接已建立。<br> 2: 请求已接收。<br> 3: 请求处理。<br>中 4: 请求已完成，且响应已就绪
status |200: "OK"。<br> 404: 未找到页面

在 onreadystatechange 事件中，我们规定当服务器响应已做好被处理的准备时所执行的任务。

当 readyState 等于 4 且状态为 200 时，表示响应已就绪：
```
xmlhttp.onreadystatechange=function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  }
```
**注释**：onreadystatechange 事件被触发 5 次（0 - 4），对应着 readyState 的每个变化。

【使用 Callback 函数】

callback 函数是一种以参数形式传递给另一个函数的函数。

如果您的网站上存在多个 AJAX 任务，那么您应该为创建 XMLHttpRequest 对象编写一个标准的函数，并为每个 AJAX 任务调用该函数。

该函数调用应该包含 URL 以及发生 onreadystatechange 事件时执行的任务（每次调用可能不尽相同）：
```
function myFunction()
{
loadXMLDoc("ajax_info.txt",function()
  {
  if (xmlhttp.readyState==4 && xmlhttp.status==200)
    {
    document.getElementById("myDiv").innerHTML=xmlhttp.responseText;
    }
  });
}
```

# AJAX 高级
## AJAX ASP/PHP










