# VUE
 
## main.js,App.vue,index.html如何调用  
    * index.html文件入口 
    * src放置组件和入口文件  
    * node_modules为依赖的模块  
    * config中配置了路径端口值等  
    * build中配置了webpack的基本配置、开发环境配置、生产环境配置等  
##  main.js,App.vue,index.html顺序  

  ![](../../attachments/front/vue文件执行先后顺序.png)  

```markdown
    1、执行index.html文件
    
    2、执行main.js文件
    
    3、main.js挂载了app.vue文件，用app.vue的templete替换index.html中的
    
    4、main.js中注入了路由文件，将对应的组件渲染到router-view中
    
    5、router-view中加载Layout文件
    
    6、Layout 加载Navbar, Sidebar, AppMain
```
