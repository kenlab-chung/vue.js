# 工程说明
node.js版本:v13.5.0
npm版本：6.13.4
cnpm版本：6.1.1
vue-cli版本：@vue/cli 4.1.2

# 工具安装方法
```
sudo apt update  //更新软件资源列表
```
## node.js 安装方法
安装：
```
sudo apt-get install -y nodejs
```
查看版本：
```
node -v
```
## npm 安装方法
```
sudo apt-get install npm //安装
sudo npm config set registry https://registry.npm.taobao.org/ //设镜像地址为淘宝npm镜像地址
```
## cnpm 安装方法（可选）
```
sudo npm install -g cnpm --registry=https://registry.npm.taobao.org
sudo cnpm -v //查看版本号
```
## n 安装方法
```
sudo npm install -g n
```
## node.js模块管理
```
sudo n stable                //安装稳定版本
sudo n latest                //安装最新版本
sudo n rm 0.10.1             //删除某个版本
sudo n use 0.10.21 some.js   //以制定的版本执行脚本
```
## vue-cli 4.0安装
```
sudo npm uninstall vue-cli -g //如果以前安装过老版本vue-cli则需要卸载之
sudo npm install @vue/cli -g //安装vue-cli 4.0
sudo vue -V  // 查看版本号
```
## 创建项目
```
vue create ucwebapp //ucwebapp为项目名称(后续操作默认即可)，建议不要用中文，不要用驼峰方式命名，用中划线或下划线
```
## element-ui 使用
安装
```
sudo npm i element-ui -S //在项目根目录下执行
```
使用（全局引入，main.js中添加如下代码）
```
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(ElementUI)
```
## vue-router
安装（项目根目录下执行）
```
sudo npm install vue-router --save-dev
```
使用（在src新建router目录，在router目录下新建index.js）
```
import Vue from 'vue'                   //引入vue
import Router from 'vue-router'         //引入vue-router 安装命令：

import home from '@/components/home.vue' //引入home组件
import about from '@/components/about.vue' //引入about组件
import login from '@/components/login.vue' //引入login组件

Vue.use(Router) 

const routes = [                        //配置路由，这里是个数组
    {                                   //每一个链表都是一个对象
        path:'/home',                       //链表路径
        name:'home',                   //路由名称
        component:home                 //对应度组件模板
    } ,
    {
        path:'/about',
        name:'about',
        component:about
    },
    {
        path:'/login',
        name:'login',
        component:login
    }
]

const router = new Router({
    routes,
    mode:''
})

export default router
```
注册（main.js）
```
import router from './router' //导入引用
```
将
```
new Vue({  
  render: h => h(App),
}).$mount('#app')
```
改为
```
new Vue({
  router,  //注入到根实例中
  render: h => h(App),
}).$mount('#app')
```
调用模板（如在App.vue的template加入如下内容）
```
 <router-link to="/login">login</router-link>| 
    <router-link to="/home">home</router-link>|    
    <router-link to="/about">about</router-link>   
    </header>
    <router-view></router-view>
```
App.vue全部代码
```
<template>
  <div id="app">    
    <img alt="Vue logo" src="./assets/logo.png">  
    <header>
    <router-link to="/login">login</router-link>| 
    <router-link to="/home">home</router-link>|    
    <router-link to="/about">about</router-link>   
    </header>
    <router-view></router-view>    
  </div>
</template>

<script>

export default {
  name: 'app'  
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```
## axios 和 qs
安装
```
sudo npm install axios -S
sudo npm install qs -S
```
配置（在main.js中引入）
```
import qs from 'qs'
import axios from 'axios'

Vue.prototype.$axios = axios
Vue.prototype.$qs = qs
```
在项目根目录下依次建立static/config文件，并在config文件夹下新建global.js文件,内容如下：
```
const host = "http://192.168.6.207:8763"  //协议+域名地址+端口
export default {
    host
}
```
在main.js中导入文件引用，并挂载
```
import global from '../static/config/global'

Vue.prototype.global = global 
```
请求后台接口数据
```
//不需要带参数的get请求
this.$axios.get(this.global.host.+"后台接口地址").then(res=>{ 
    // 获取服务器返回的数据
    })

//带参数的get请求
this.$axios.get(this.global.host.+"后台接口地址"，{
    params:{
        phone:123456, //参数，键值对，Key值：value值
        name:hh
    }
}).then(res=>{ 
    // 获取服务器返回的数据
    })
//post请求
var data = {phone:123456,name:hh} //定义一个data存储需要携带度参数
this.$axios.post(this.global.host.+"后台接口地址"，this.$qs.stringify(data)).then(res=>{ 
    // 获取服务器返回的数据
    })
```
组件发送axios请求例子
```
<template>
    <div>
        <li v-for="cate in categoryList">{{cate.name}}</li>
    </div>
</template>
<script>
export default {
    created (){
        this.getCategory();
    },
    data () {
        return {
            categoryList:[]
            }
    },
    methods:{
        getCategory:function(){
            this.$axios.get(this.global.host+"虚拟接口/a/all_category").then(res=>{
                var result = res.data;
                if(result.code == 0){
                    this.categoryList = result.data;
                }
            })
        }
    }
}
</script>
```
## vuex
安装
```
npm install vuex -S
```