# cf-openai-azure-proxy with ⚡ Severless

[![serverless](http://public.serverless.com/badges/v3.svg)]()

<a href="./README_en.md">English</a> |
<a href="./README.md">中文</a>

> Most OpenAI clients do not support Azure OpenAI Service, but the application for Azure OpenAI Service is very simple, and it also provides free quotas. This script uses a free Cloudflare Worker as a proxy, allowing OpenAI-supported clients to directly use Azure OpenAI Service.

> Building upon the original project, this project incorporates the Serverless Framework to achieve automated deployment and updates, eliminating the need for manual deployment and updates.

### Description:

- Do I need my own server?
  - This script runs on Cloudflare Worker, eliminating the need for a server and card binding, with a free daily quota of 100,000 requests.
- Do I need my own domain?
  - Not necessary. Refer to: https://github.com/haibbo/cf-openai-azure-proxy/issues/3
- Implementing a printer mode:
  - Azure OpenAI Service's responses are segmented.
  - When returning to the client, this project separates the messages into individual segments, achieving a printer-like mode.
- Project supports Serverless deployment (based on Serverless Framework).

### Deployment (with Serverless)

Proxying requests from OpenAI to Azure OpenAI Service through Serverless automated deployment steps:

1. Register and log in to your Cloudflare account.
2. Obtain the required [CLOUDFLARE_AUTH_KEY] (Global API Key), [CLOUDFLARE_AUTH_EMAIL], [CLOUDFLARE_ACCOUNT_ID], [CLOUDFLARE_ZONE_ID].
3. Click the `Fork` button to create a new Worker project.
4. In your newly created project, set the obtained environment variables in the secrets section (see [figure below](#instructions) for how to set secrets).
5. After saving, switch to the `Actions` tab, select `Cloudflare Workers`, click the `Run workflow` button, and wait for the deployment to complete.
6. Optionally, bind a custom domain by following these steps: In the Worker details page -> Trigger -> Custom Domains, add a custom domain for this Worker.

## Instructions
First obtain the `resourceName` and `deployment mapper`, and log in to the Azure portal:

<img width="777" src="https://user-images.githubusercontent.com/1295315/233124125-1ea95665-ffab-4b5c-a7ba-26f31f1bb0b3.png" alt="env" />

- Set up repository `secrets`:

  <img width="777" src="https://github.com/Teakowa/cf-openai-azure-proxy/assets/27560638/79ec038e-6772-4818-936e-d2cba71d1a49"  alt="new repository secrets" />
  <img width="777" alt="new secret" src="https://github.com/Teakowa/cf-openai-azure-proxy/assets/27560638/773283b5-25ee-47a2-bf67-050cc760b3cd">

**Required environment variables:**

- `CLOUDFLARE_AUTH_KEY`: Cloudflare's [Global API Key]
- `CLOUDFLARE_AUTH_EMAIL`: Cloudflare account [email]
- `CLOUDFLARE_ACCOUNT_ID`: Cloudflare account [ID]
- `CLOUDFLARE_ZONE_ID`: Cloudflare account zone [ID]
- `RESOURCE_NAME`: Azure OpenAI Service name
- `DEPLOY_NAME_GPT35`: Azure OpenAI Service GPT-3.5 deployment name
- `DEPLOY_NAME_GPT4`: Azure OpenAI Service GPT-4 deployment name

## Client

Take OpenCat as an example: fill in the custom API domain name with the domain name bound in step 6:

<img width="339" src="https://user-images.githubusercontent.com/1295315/229820705-ab2ad1d1-8795-4670-97b4-16a0f9fdebba.png" alt="opencat" />

I have tried multiple clients. If you encounter problems with other clients, please feel free to create an issue.

### Update

In your forked repository, click the `sync fork` button to synchronize with this repository.

[CLOUDFLARE_AUTH_KEY]: https://dash.cloudflare.com/profile/api-tokens
[Global API Key]: https://dash.cloudflare.com/profile/api-tokens
[CLOUDFLARE_AUTH_EMAIL]: https://dash.cloudflare.com/profile
[email]: https://dash.cloudflare.com/profile
[CLOUDFLARE_ACCOUNT_ID]: https://developers.cloudflare.com/fundamentals/get-started/basic-tasks/find-account-and-zone-ids/
[CLOUDFLARE_ZONE_ID]: https://developers.cloudflare.com/fundamentals/get-started/basic-tasks/find-account-and-zone-ids/
[ID]: https://developers.cloudflare.com/fundamentals/get-started/basic-tasks/find-account-and-zone-ids/
