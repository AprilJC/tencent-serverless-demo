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



