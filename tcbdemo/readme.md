# TCB MongoDB + SCF + Website 最佳实践

## 操作场景
   该模板可以快速部署一个基于 **TCB MongoDB + SCF + Website** 的全栈 Serverless 应用。主要包含以下组件：
   
   - **Serverless Website：** 前端通过托管 html 静态页面到 COS 对象存储中。
   - **Serverless Cloud Function：** 后端函数部署到云端，通过http进行触发调用
   - **TCB云开发环境：** 通过创建云开发环境并调用MongoDB，为全栈网站提供数据库服务。
   
## 操作步骤
   
   ### 安装
   
   通过 npm 全局安装 [serverless cli](https://github.com/serverless/serverless)：
   ```bash
   $ npm install -g serverless
   ```
   
   如果之前您已经安装过 Serverless Framework，可以通过下列命令升级到最新版：
   ```bash
   $ npm update -g serverless
   ```
   
   安装完毕后，通过运行serverless -v命令，查看 Serverless Framework 的版本信息，确保版本信息不低于以下版本：
   ```bash
   $ serverless –v
   Framework Core: 1.67.3
   Plugin: 3.6.6
   SDK: 2.3.0
   Components: 2.30.0
   ```
   
   ### 配置
   
   1.新建一个本地文件夹，使用create --template-url命令，下载相关 template：
   ```bash
   $ mkdir my_tcbdemo && cd my_tcbdemo
   $ serverless create --template-url https://github.com/Jiachen0417/tencent-serverless-demo/edit/master/tcbdemo
   ```
   
   2.在项目模板中找到`.env.example`文件，修改名称为`.env`，并在其中配置对应的腾讯云 SecretId 和 SecretKey 信息：
    
   ```text
   # .env
   TENCENT_SECRET_ID=123
   TENCENT_SECRET_KEY=123
   ```
    
   找到**function->serverless.yaml**文件，填入自己的 SecretId 和 SecretKey。
   
   >说明:
     1. 如果没有腾讯云账号，请先[注册新账号](https://cloud.tencent.com/register)。
     2. 如果已有腾讯云账号，可以在[ API 密钥管理](https://console.cloud.tencent.com/cam/capi) 中获取**SecretId**和**SecretKey**。
   
   3.在`function->src`文件夹目录下，通过以下命令安装所需依赖：
   ```bash
   $ npm install
   ```
   
   ### 部署
   1. 配置完成后，首先进入mongodb目录下，通过以下命令进行部署，创建一个新的云开发环境，并可以参数查看部署过程中的信息：
   
   ```bash
   $ serverless --debug
   ```
   
   2. 接下来进入function目录下，同样通过`serverless --debug`进行云函数部署，部署成功结果如下：
   
   ```bash
   $ serverless --debug

   Initializing...
   Action: "deploy" - Stage: "dev" - App: "mongoDBAPP" - Instance: "mongoDBDemoSCF"
   Deploying...

   FunctionName: MongoDBDemo
   Description:  
   Namespace:    default
   Runtime:      Nodejs8.9
   Handler:      index.main
   MemorySize:   128
   Triggers: 
     apigw: 
       - https://service-dlq65ccq-1258834142.gz.apigw.tencentcs.com/release/users
   
   67s › mongoDBDemoSCF › Success
   ```
   3. 最后部署静态网站，进入website目录，通过`serverless --debug`进行云函数部署，部署成功结果如下：
   ```bash
   $ serverless --debug

   Initializing...
   Action: "deploy" - Stage: "dev" - App: "mongoDBAPP" - Instance: "mongoDBDemoWebsite"
   Deploying...

   website: http://my-bucket-1258834142.cos-website.ap-guangzhou.myqcloud.com


   8s › mongoDBDemoWebsite › Success
   ```
   访问命令行输出的 website url，即可查看您的 Serverless 站点。
   
   ### 移除
   
   可通过以下命令移除项目：
   
   ```bash
   $ sls remove --debug
   ```
   
   #### 更多组件
   您可在[Serverless Component Repo](https://github.com/serverless/components)中查看更多组件信息



