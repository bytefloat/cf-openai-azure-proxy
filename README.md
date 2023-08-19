# cf-openai-azure-proxy with ⚡ Severless

[![serverless](http://public.serverless.com/badges/v3.svg)]()

<a href="./README_en.md">English</a> |
<a href="./README.md">中文</a>

> 大多数 OpenAI 客户端不支持 Azure OpenAI Service，但Azure OpenAI Service的申请和绑卡都非常简单，并且还提供了免费的额度。此脚本使用免费的 Cloudflare Worker 作为代理，使得支持 OpenAI 的客户端可以直接使用 Azure OpenAI Service。

> 本项目在源项目的基础上，使用 Serverless Framework 实现了自动部署与自动更新，无需手动部署，无需手动更新。

### 项目说明:

- 我没有服务器可以使用吗?
    - 这段脚本跑在Cloudflare Worker, 不需要服务器, 不需要绑卡, 每天 10W 次请求 免费
- 我没有自己的域名可以使用吗?
    - 也可以, 参考: https://github.com/haibbo/cf-openai-azure-proxy/issues/3
- 实现打印机模式：
    - Azure OpenAI Service's 回复是一段一段回复的
    - 返回给客户端的时候， 本项目拆出一条条的消息, 依次给， 达到打印机模式
- 项目支持 Serverless 部署（基于 Serverless Framework）

### 部署 (with Serverless)

代理 OpenAI 的请求到 Azure OpenAI Service，基于 Serverless 自动部署步骤：

1. 注册并登录到 Cloudflare 账户
2. 获得部署需要用到的 [CLOUDFLARE_AUTH_KEY] (Global API Key)、 [CLOUDFLARE_AUTH_EMAIL]、[CLOUDFLARE_ACCOUNT_ID] 和 [CLOUDFLARE_ZONE_ID]
3. 点击 'Fork' 按钮，创建一个新的 Worker 项目
4. 在你新创建的项目中，设置上面获得的环境变量到 `secrets` 中(设置 secrets 的方法见[下图](#使用说明))
5. 保存后切换到 `Actions` 选项卡，选中 `Cloudflare Workers`，点击 `Run workflow` 按钮，等待部署完成
6. https://github.com/haibbo/cf-openai-azure-proxy/issues/3 **可选**绑定自定义域名: 在 Worker 详情页 -> Trigger -> Custom Domains 中为这个 Worker 添加一个自定义域名

### 使用说明

先得到 `resourceName` 和 `deployment mapper`, 登录到Azure的后台:

<img width="777" src="https://user-images.githubusercontent.com/1295315/233124125-1ea95665-ffab-4b5c-a7ba-26f31f1bb0b3.png" alt="env" />

- 设置仓库的 `secrets`：

  <img width="777" src="https://github.com/Teakowa/cf-openai-azure-proxy/assets/27560638/79ec038e-6772-4818-936e-d2cba71d1a49"  alt="new repository secrets" />
  <img width="777" alt="new secret" src="https://github.com/Teakowa/cf-openai-azure-proxy/assets/27560638/773283b5-25ee-47a2-bf67-050cc760b3cd">

**需要设置的环境变量：**

- `CLOUDFLARE_AUTH_KEY`: Cloudflare 的 [Global API Key]
- `CLOUDFLARE_AUTH_EMAIL`: Cloudflare 账户的[邮箱]
- `CLOUDFLARE_ACCOUNT_ID`: Cloudflare 账户的 [ID]
- `CLOUDFLARE_ZONE_ID`: Cloudflare 账户的域名 [ID]
- `RESOURCE_NAME`：Azure OpenAI Service 的名称
- `DEPLOY_NAME_GPT35`: Azure OpenAI Service 的 GPT-3.5 部署名称
- `DEPLOY_NAME_GPT4`: Azure OpenAI Service 的 GPT-4 部署名称

### 客户端

以 OpenCat 为例: 自定义 API 域名填写 第六步绑定的域名:

<img width="339" src="https://user-images.githubusercontent.com/1295315/229820705-ab2ad1d1-8795-4670-97b4-16a0f9fdebba.png" alt="opencat" />

我已经尝试了多种客户端, 如果遇到其他客户端有问题, 欢迎创建issue.

### 更新

在你 fork 的仓库中, 点击 `sync fork` 按钮, 即可与本仓库同步。

[CLOUDFLARE_AUTH_KEY]: https://dash.cloudflare.com/profile/api-tokens
[Global API Key]: https://dash.cloudflare.com/profile/api-tokens
[CLOUDFLARE_AUTH_EMAIL]: https://dash.cloudflare.com/profile
[邮箱]: https://dash.cloudflare.com/profile
[CLOUDFLARE_ACCOUNT_ID]: https://developers.cloudflare.com/fundamentals/get-started/basic-tasks/find-account-and-zone-ids/
[CLOUDFLARE_ZONE_ID]: https://developers.cloudflare.com/fundamentals/get-started/basic-tasks/find-account-and-zone-ids/
[ID]: https://developers.cloudflare.com/fundamentals/get-started/basic-tasks/find-account-and-zone-ids/
