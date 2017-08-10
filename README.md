## 一、我们从最简单的环境开始搭建
1. 安装node.js，从[node.js官网](https://nodejs.org)下载并安装node，安装过程很简单，一路“下一步”就可以了。安装完成以后，打开命令行工具(win+r)，然后输入cmd),输入node -v，如果出现相应版本号，则说明安装成功。

2. 安装淘宝镜像，打开命令行工具，把这个```（npm install -g cnpm --registry= https://registry.npm.taobao.org）```复制，安装这个便于快速的下载依赖包，因为npm的服务器在国外。安装完成之后输入 cnpm -v，如果出现相应的版本号，则说明安装成功。

3. 安装webpack，打开命令行工具输入：npm install webpack -g，安装完成之后输入 webpack -v，如下图，则说明安装成功。

4. 安装vue-cli脚手架构建工具，打开命令行工具输入：npm install vue-cli -g，安装完成之后输入 vue -V（注意这里是大写的“V”），则说明安装成功。  

## 二、通过以上四步，我们需要准备的环境和工具都准备好了，接下来就开始使用vue-cli来构建项目
1. 在硬盘上找一个文件夹放工程用的。这里有两种方式指定到相关目录：①cd 目录路径 ②如果以安装git的，在相关目录右键选择Git Bash Here

2. 安装vue脚手架输入：vue init webpack vue-project ，注意这里的“vue-project” 是项目的名称可以说是随便的起名，但是需要主要的是“不能用中文”。

3. cd 命令进入创建的工程目录，首先cd vue-project（这里是自己建工程的名字）

4. 安装项目依赖：npm install，因为自动构建过程中已存在package.json文件，所以这里直接安装依赖就行。不要从国内镜像cnpm安装(会导致后面缺了很多依赖库)，但是但是如果真的安装“个把”小时也没成功那就用：cnpm install 

5. 安装 vue 路由模块 vue-router 和网络请求模块 vue-resource，输入：cnpm install vue-router vue-resource --save

6. 启动项目，输入：npm run dev。服务启动成功后浏览器会默认打开一个“欢迎页面”(注意：这里是默认服务启动的是本地的8080端口，所以请确保你的8080端口不被别的程序所占用)
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
