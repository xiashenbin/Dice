<p align="center">
  <img align="center" src="https://raw.githubusercontent.com/bihell/blog-img/master/logo.png"/>
</p>

<p align="center">
    <a href="https://www.travis-ci.org/bihell/Dice"><img src="https://www.travis-ci.org/bihell/Dice.svg?branch=master"></a>
    <a href="https://codebeat.co/projects/github-com-bihell-dice-master"><img alt="codebeat badge" src="https://codebeat.co/badges/eb0bdd65-dad1-45e6-aea6-371c64d4d943" /></a>
    <a href="https://github.com/bihell/Dice/blob/master/LICENSE"><img alt="GitHub license" src="https://img.shields.io/github/license/bihell/Dice"></a>
    <a alt="spring boot"><img src="https://img.shields.io/badge/spring%20boot-2.2.0.RELEASE-blue"/></a>
    <a alt="vue"><img src="https://img.shields.io/badge/vue-2.6.10-orange.svg"></a>
    <a alt="nuxt"><img src="https://img.shields.io/badge/nuxt-2.8.1-yellowgreen.svg"></a>
    <a alt="docker"><img src="https://img.shields.io/badge/docker-18.06.01--ce-ff69b4.svg"></a>
    <a alt="docker-compose"><img src="https://img.shields.io/badge/docker--compose-1.22.0-lightgrey.svg"></a>
</p>

* 基于`node` `java` `spring-boot` `vue` `nuxt` 开发的个人管理系统，目前已经实现「博客」、「媒体库」、「代码段」功能
* 支持传统手动部署和`docker`部署
* 功能精简但齐全，界面简洁却美观，满足个人日常使用要求
* 项目会持续更新，如果有不完善的地方，欢迎指出

> 演示站点: [http://bihell.com](http://bihell.com)  QQ 群：48384453

### 项目结构

#### 文件结构

```
├── dice
│   ├── dice-admin          // 管理后台，使用vue-element-admin，它基于 vue 和 element-ui实现
│   ├── dice-docker         // docker部署文件
│   ├── dice-front          // 博客前端，使用 Fame，基于 vue 和 nuxt
│   ├── dice-server         // 管理服务端，基于 spring-boot全家桶
│   └── docker-compose.yml  // docker-compose文件
```

### 部分界面

![博客前端](https://raw.githubusercontent.com/bihell/blog-img/master/dice1.png)
![](https://raw.githubusercontent.com/bihell/blog-img/master/dice4.png)
![](https://raw.githubusercontent.com/bihell/blog-img/master/dice5.png)
![](https://raw.githubusercontent.com/bihell/blog-img/master/dice7.png)
![代码段](https://raw.githubusercontent.com/bihell/blog-img/master/snippet.png)
![媒体库](https://raw.githubusercontent.com/bihell/blog-img/master/dice-media.png)

### 部署方式

**注：博客管理后台默认的账号：dice，密码：123456**

#### Docker方式部署(推荐)

1. 克隆项目到本地

   ```
   git clone https://github.com/bihell/Dice.git
   ```

3. 启动项目

    ```
    docker-compose up 或 docker-compose up -d
    ```
    第一次启动推荐`docker-compose up`，可以看到启动日志，由于要下载镜像和maven依赖，时间可能较久，视网络环境和性能而定

    ```
    ➜ dice git:(master) docker-compose up -d
    Creating network "dice_default" with the default driver
    Creating dice-admin  ... done
    Creating dice-front  ... done
    Creating dice-mysql ... done
    Creating dice-server ... done
    Creating dice-nginx  ... done
    ```
4. 访问地址
  
    启动完成后，在浏览器访问 
    
    `http://xx.xxx.xx.xx/` 为博客前端首页
    
    `http://xx.xxx.xx.xx/admin` 为博客管理后台首页

#### 开发环境

首先保证有 `java8` `mysql5.7.x` `maven3.3.x` `node 12.6.0` `npm 6.11.3` `redis 5.0.6` 的环境(版本不一定要完全一样，但避免奇怪的问题出现，最好相同)

1. 克隆项目到本地

   ```
   git clone https://github.com/bihell/Dice.git
   ```

2. 部署服务端 (项目使用lombok插件，如果要在ide中调试要有lombok插件)

    2.1 进入服务端文件夹

        `cd dice-server`

    2.2 修改spring-boot配置文件

      `vi src/main/resources/application-dev.properties`

      ```
      spring:
            datasource:
              driverClassName: com.mysql.cj.jdbc.Driver
              url: jdbc:mysql://localhost:3306/dice?useUnicode=true&characterEncoding=utf-8&useSSL=false&serverTimezone=Asia/Shanghai
              username: root
              password: root
      ```
      将数据库的用户名和密码修改成对应你数据库的用户名密码
    
    2.3 启动dice-server

      `mvn clean spring-boot:run -Dmaven.test.skip=true`

3. 部署博客前端

    3.1 进入前端文件夹

      `cd dice-front`

    3.2 安装依赖和启动服务

      ```
    npm install
    npm run dev
      ```

    3.3 访问地址

      启动完成后，浏览器访问 `http://localhost:3000`

4. 部署博客后端

    4.1 进入后端文件夹

      `cd dice-admin`

    4.2 安装依赖和启动服务

     ```
    npm install
    npm run dev
     ```

    4.3 访问地址

      启动完成后，浏览器访问 `http://localhost:8010/admin`
