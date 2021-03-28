# 使用 Heroku 部署 Xray 高性能代理服务，通过 Vless + WS 协议传输

> 提醒： 滥用可能导致账户被BAN！！！ 

## 概述

用于在 Heroku 上部署 Vless + Websocket + Tls，每次部署自动选择最新的 alpine linux 和 Xray core 。
Vless 性能更加优秀，占用资源更少。

**Heroku 为我们提供了免费的容器服务，我们不应该滥用它，所以本项目不宜做为长期大流量使用。**

## 镜像

本镜像不会因为大量占用资源而被封号。注册好 Heroku 账号并登录后，点击下面按钮便可部署。

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https://github.com/wanjiji/heroku-xray)

### 路径

`WebSocket` 路径(配置文件中的 `path` )为 `/api` 。

### 端口

`端口` 为 `443` 。

### UUID

`UUID` 默认为 `63a6c4d6-a55d-44e6-b232-a0f6a6672eed` 可自行设置。

**Xray 将在部署时自动安装`最新版本`。**

**出于安全考量，除非使用 CDN，否则请不要使用自定义域名，而使用 Heroku 分配的二级域名，以实现 Xray Vless + Websocket + Tls。**

## 流量中转

<summary>可以使用 Cloudflare 的 Workers 来中转流量，配置为：</summary>

```js
addEventListener(
    "fetch", event => {
        let url = new URL(event.request.url);
        url.hostname = "xxx.herokuapp.com"; // 你的heroku域名
        let request = new Request(url, event.request);
        event.respondWith(
            fetch(request)
        )
    }
)
```
