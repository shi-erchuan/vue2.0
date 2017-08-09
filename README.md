### vue2.0项目中遇到的问题及解决办法
#### 1.axios使用post请求参数无法传给后台服务器
    之前在项目中使用vue2.0搭建了一个后台管理系统，在与后台数据交互的时候出现了问题，axios的post请求无法传递,在网上查阅下资料才知道，在node环境中可以使用Qs模块,Qs.stringify(data)来处理数据，安装了axios自带qs模块，引入即可
```javascript
var Qs=require('qs');
var app = new Vue({
    el: "#register",
    data: {
        registerUrl: "/KindlePocket/bindingData"
        newUserInfo: {
            userName:'n',
            phone:'13',
            email:'12',
            emailPwd:'22',
            kindleEmail:'asd'
        }
    },
    methods: {
        register: function() {
                axios.post(this.registerUrl, Qs.stringify(this.newUserInfo), {
                      headers: {
                            'Content-Type': 'application/x-www-form-urlencoded'
                      }
                  })
                  .then(function (response) {
                    console.log(response);
                  })
                  .catch(function (error) {
                    console.log(error);
                  });
            
        }
    }
})
```
