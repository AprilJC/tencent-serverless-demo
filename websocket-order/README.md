# Serverless 部署API网关+云函数的外卖订单系统

### 1. 安装Serverless Framework

```
npm install -g serverless
```

### 2. 初始化项目模板

```
sls init -t websocket-order
```

### 3. 查看项目目录
下载到本地后，查看项目目录结构，包含，DB，网关、函数等多个子模块。说明如下:
- db 目录用于创建 PG Serverless 数据库实例
- apigateway 用于创建对应的 API ：
	
  - /bill  下单 API，HTTP 类型
  - /get_shop_info，获取店铺菜单 API
  - /pgws，用于做消息推送的 websocket API
- 函数列表如下：
  - 消息推送相关函数：
    - 注册函数  ws_register.py， 配置DB的环境变量
    - 传输函数  ws_trans.py ，配置DB的环境变量以及apiid= 消息推送API
    - 注销函数  ws_unregister.py ，配置DB的环境变量以及apiid= 消息推送API
  - 下单函数  bill.py ，配置DB的环境变量以及apiid= 消息推送API
  - 拉取店铺信息函数  get_shop_info.py，配置DB的环境变量
  - 初始化DB函数 init_db.py ,配置DB的环境变量

### 4. 修改配置信息
将 .env.example 文件为 .env 文件，在 API 密钥管理 中获取 SecretId 和 SecretKey。

```
# secret for credential
TENCENT_SECRET_ID=xxxxxx
TENCENT_SECRET_KEY=xxxxxx

# global config
REGION=ap-shanghai
```

### 5. 项目部署
```
sls deploy --all
```

### 6. 更新函数 apiid 配置，再次部署

### 7. 更改客户端与厨房订单系统的地址

- order_page.html 更改29行 以及88 行中xxxx为 生成的API网关服务域名
- shop.html  更改17行 xxxx为API网关服务域名

### 附录：参考文档和配置：

安装 serverless framework https://cloud.tencent.com/document/product/583/44753
安装 Serverless DB https://cloud.tencent.com/document/product/1154/45447 
api 网关的 yaml 完整配置 https://github.com/serverless-components/tencent-apigateway/blob/master/docs/configure.md
scf 的 yaml 完整配置 https://github.com/serverless-components/tencent-scf/blob/master/docs/configure.md
