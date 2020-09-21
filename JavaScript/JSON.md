# JSON



## JSON是什么？

JSON (JavaScript Object Notation, JS 对象标记) 是一种轻量级的数据交换格式。它基于 ECMAScript (w3c制定的js规范)的一个子集，采用完全独立于编程语言的文本格式来存储和表示数据。简洁和清晰的层次结构使得 JSON 成为理想的数据交换语言。 易于人阅读和编写，同时也易于机器解析和生成，并有效地提升网络传输效率。——百度百科

数据传输是我们在敲代码时，经常遇到的一个场景,前后端交互。给数据一个统一的格式有利于我们编写和解析数据。

==json，是一种数据格式，在与后端的数据交互中有较为广泛的应用(很重要)==



## JSON对象

```javascript
var person={"name":"java-hk","age":18,"gender":"男"};
console.log(person.name);//控制台输出java-hk
alert(typeof person);//object;
```



## json字符串

我们常说字符串是用引号括起来的，那么json的字符串是也是用引号扩起来的。

```javascript
var strjson='{"name":"java-hk","age":18,"gender":"男"}';
console.log(strjson);//{"name":"java-hk","age":18,"gender":"男"}
alert(typeof strjson);//string
```

以上strjson也是一个字符串，之所以叫json字符串是因为它符合json字符串的格式。



## json字符串和json对象的转换

```javascript
		<script>
        //json字符串转json对象
        var strjson='{"name":"java-hk","age":18}';
        var strjsontoobj=JSON.parse(strjson);
        console.log(strjson);
        console.log(strjsontoobj);
        console.log(typeof strjsontoobj);
        //json对象转json字符串
        var objjson={"name":"java-hk","age":18};
        var objJsonToStr=JSON.stringify(objjson);
        console.log(objJsonToStr);
        console.log(typeof objJsonToStr);
    </script>
```



## JSON的应用：

### ==1.省市区联动==

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="../script/jquery-1.7.2.js"></script>
  	//这是一个json文件
    <script src="../script/addr.js"></script>
    <script>
        $(function (){
            
           	$.each(temp,function (i,d){
               var option='<option value="'+d.code+'">'+d.label+'</option>';
               $("#prov").append(option);
            })

            $("#prov").change(function (){
                $("#city").html('<option>--请选择城市</option>')
                var provcode = $(this).val();
                $.each(temp,function (i,d){
                    if (d.code==provcode){
                        $.each(d.children,function (i,d){
                            var option='<option value="'+d.code+'">'+d.label+'</option>';
                            $("#city").append(option);
                        })
                    }

                })
            })

            $("#city").change(function (){
                var provcode = $("#prov").val();
                var citycode=$(this).val();
                $("#quxian").html('<option>--请选择区县</option>')
                $.each(temp,function (i,d){
                    if (d.code==provcode){
                        $.each(d.children,function (i,d){
                            if (d.code==citycode){
                                $.each(d.children,function (i,d){
                                    var option='<option value="'+d.code+'">'+d.label+'</option>';
                                    $("#quxian").append(option);
                                })
                            }
                        })
                    }
                })
            })
        })
    </script>
</head>
<body>
<select id="prov">
    <option value="0" selected="selected" disabled>--请选择省份</option>
</select>

<select id="city">
    <option value="1" selected="selected" disabled>--请选择城市</option>
</select>

<select id="quxian">
    <option value="2" selected="selected" disabled>--请选择区县</option>
</select>
</body>
</html>
```

