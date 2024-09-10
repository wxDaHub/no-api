# NO-API

> [!NOTE]
> 本项目在[New-API](https://github.com/Calcium-Ion/new-api/)基础上调整，只更改了前端，后端同步New-API最新版，所以完全适配New，数据库可共用。

> [!IMPORTANT]
> 使用者必须在遵循 OpenAI 的[使用条款](https://openai.com/policies/terms-of-use)以及**法律法规**的情况下使用，不得用于非法用途。
> 本项目仅供个人学习使用，不保证稳定性，且不提供任何技术支持。
> 根据[《生成式人工智能服务管理暂行办法》](http://www.cac.gov.cn/2023-07/13/c_1690898327029107.htm)的要求，请勿对中国地区公众提供一切未经备案的生成式人工智能服务。

> [!TIP]
> 最新版Docker镜像：`wxdadadada/no-api:latest`
> 默认账号root 密码123456


## 主要变更

1. 前端界面调整

## 项目文档

[https://docs.qq.com/doc/p/af2a94ff20cd066dc642d20179a04006c9cba162](https://docs.qq.com/doc/p/af2a94ff20cd066dc642d20179a04006c9cba162)

## 演示地址

[api.openai.sn](https://api.openai.sn)


## 演示截图

<img width="1499" alt="image" src="https://github.com/user-attachments/assets/07c84333-23ff-4bde-8591-42f91114dd1e">


## docker-compose.yml

```shell
version: '3.4'

services:
  no-api:
    image: wxdadadada/no-api:latest
    # build: .
    container_name: no-api
    restart: always
    command: --log-dir /app/logs
    ports:
      - "3000:3000"
    volumes:
      - ./data:/data
      - ./logs:/app/logs
    environment:
      - TZ=Asia/Shanghai
      # - SQL_DSN=root:123456@tcp(127.0.0.1:3306)/new-api  # 修改此行，或注释掉以使用 SQLite 作为数据库
      # - REDIS_CONN_STRING=redis://127.0.0.1:6379
      # - SESSION_SECRET=random_string  # 修改为随机字符串      
      # - NODE_TYPE=slave  # 多机部署时从节点取消注释该行
      # - SYNC_FREQUENCY=60  # 需要定期从数据库加载数据时取消注释该行
    healthcheck:
      test: [ "CMD-SHELL", "wget -q -O - http://localhost:3000/api/status | grep -o '\"success\":\\s*true' | awk -F: '{print $2}'" ]
      interval: 30s
      timeout: 10s
      retries: 3
```
