# study
begin to learn new language(python) and how to use Github

# django做的电商网站 关于坑： 
## 1.在订单提交的时候必须输入{% csrf_token %}   
## 2.关于models，在只能有一个autofield或者id找不到的时候，进行migrate是正确的选择   
## 3.templates中html找不到：settings的templates中的`dir=[BASE_DIR+"/templates",], ` 
## 4.model找不到，在app里面加上model的名称。  
## 5.前端使用静态文件的时候，加上  
  ```python
  STATICFILES_DIRS = [
      os.path.join(BASE_DIR, "static"),
  ]
  ```
  并在根目录新建文件夹：`static`   
## 6.网页使用html的时候，加上`{% load staticfiles %}`
并且所有的静态文件如css，js等，地址都要写成`<link rel="stylesheet" href="{% static 'layui/css/layui.css' %}">`的形式。   
## 7.关于db=table.objects.all()之后出来的数值，想要在前端使用，则需要进行序列化 
```python
    ajax_testvalue = serializers.serialize("json", db)
    m=json.loads(ajax_testvalue)
    data_db=[x['fields'] for x in m]
```
## 8.关于session
写入用`request.session['username']=username`
  注意，通过session跳转页面需要重定向，用`Httpresponseredirect()`,否则会在原有界面上进行render，最终数据混乱。   
## 9.加速下载：
 `pip install web.py -i http://pypi.douban.com/simple --trusted-host pypi.douban.com`   
## 10.`'WSGIRequest' object has no attribute 'raw_post_data'` python3以后都用`request.body`   
## 11.json传值到后台，
如果一个字段中有多个值，需要使用getlist来获取。`req =str(request.POST.getlist('cart[]'))`   
## 12.django获取到json之后
用getlist得到所有json的值，然后分别eval变成字典，就可以用了。
## 13.session跨域：
前后端分离，post请求的时候会有跨域问题，解决跨域需要用到：
```js
$('#2').click(function(){
$.ajax({
        url: 'http://127.0.0.1:8000/test/',
        type: 'post',
        data: {tel:'2232223',playerid:'2345'},
        //加上 xhrFields及crossDomain
        xhrFields: {
            withCredentials: true//允许带上凭据
        },
        crossDomain: true,
        //
        success:function(res){
        alert("Data:"+res)
        },
    });
});
```
session的问题，用手机号来解决：
设置同样的set-cookie
response.set-cookie(key,value)