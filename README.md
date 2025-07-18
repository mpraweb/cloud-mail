
<p align="center">
  <img src="doc/demo/logo.png" width="10%" />
</p>

<div align="center">
<h1>Cloud Mail</h1>
</div>
<div align="center">
    <h4>A minimalist and responsive email service developed with Vue3, supporting attachments for sending and receiving emails. Can be deployed on Cloudflare for free 🎉</h4> 
</div>


## Project Overview

All you need is a domain to create multiple different mailboxes, similar to platforms like QQ Mail and Gmail. This project is deployed on Cloudflare, uses Resend for email delivery, and requires no server fees — build your own email service.

## Live Demo

[**👉 Live Demo**](https://skymail.ink)

[**👉 Beginner-friendly Interface Deployment Tutorial**](https://doc.skymail.ink)

| ![](/doc/demo/demo1.png) | ![](/doc/demo/demo2.png) |
|--------------------------|---------------------|
| ![](/doc/demo/demo3.png) | ![](/doc/demo/demo4.png) |
| ![](/doc/demo/demo5.png) | ![](/doc/demo/demo6.png) |
| ![](/doc/demo/demo7.png) | ![](/doc/demo/demo8.png) |


## Features

- **💰Free to Use**: No server needed, deploy to Cloudflare Workers and use for free

- **💻Responsive Design**: Responsive layout adapts to PC and most mobile browsers

- **📧Email Sending**: Integrated with Resend, supports bulk sending, embedded images, attachments, and delivery status tracking

- **🛡️Admin Features**: Manage users and emails with RBAC permissions and usage restrictions

- **🔀Multi-account Mode**: One user can have multiple mailboxes (default is one user, one mailbox), like major email platforms

- **📦Attachments**: Send and receive attachments using R2 object storage

- **🔔Email Push**: Incoming emails can be forwarded to Telegram bots or other providers

- **📈Data Visualization**: Visual stats on system and user email growth via ECharts

- **⭐Starred Emails**: Mark important emails for quick access

- **🎨Customization**: Set site title, login background, transparency, etc.

- **⚙️Feature Toggles**: Enable/disable registration, email sending, adding users, etc. Set as private site

- **🤖Human Verification**: Integrated with Turnstile to prevent bulk bot registrations

- **📜More Features**: In development...


## Tech Stack

- **Frontend Framework**: [Vue3](https://vuejs.org/) + [Element Plus](https://element-plus.org/) 

- **Web Framework**: [Hono](https://hono.dev/)

- **ORM**: [Drizzle](https://orm.drizzle.team/)

- **Platform**: [Cloudflare Workers](https://developers.cloudflare.com/workers/)

- **Email Provider**: [Resend](https://resend.com/)

- **Cache**: [Cloudflare KV](https://developers.cloudflare.com/kv/)

- **Database**: [Cloudflare D1](https://developers.cloudflare.com/d1/)

- **File Storage**: [Cloudflare R2](https://developers.cloudflare.com/r2/)

## Setup Guide

### Requirements

Node.js v18.20+

Cloudflare account (with bound domain)


**Clone the project locally**
```shell
git clone https://github.com/LaziestRen/cloud-mail
cd cloud-mail/mail-worker
```

**Install dependencies**
```shell
npm i
```

**Configuration**

mail-worker/wrangler.toml

```toml
[[d1_databases]]
binding = "db"
database_name = ""
database_id = ""

[[kv_namespaces]]
binding = "kv"
id = ""

[[r2_buckets]]
binding = "r2"
bucket_name = ""

[assets]
binding = "assets"
directory = "./dist"

[vars]
orm_log = false
domain = []          # e.g. ["example1.com","example2.com"]
admin = ""           # e.g. admin@example.com
jwt_secret = ""
```

**Remote Deployment**

1. Create KV, D1, R2 on Cloudflare Console
2. Configure `wrangler.toml` with your environment values
3. Run:
```shell
npm run deploy
```
4. Cloudflare → Your Domain → Email → Routing → Catch-all → Route to Worker

5. Visit `https://your-domain/api/init/your_jwt_secret` in browser to init or update d1/kv

6. Log into the site, go to Settings (as admin) to set R2 domain, Turnstile key, etc.

[👉 Deploy with Github Action](/doc/github-action.md)

**Local Development**

1. Local databases and storage are automatically created in `.wrangler`
```shell
npm run dev
```
2. Visit `http://127.0.0.1:8787/api/init/your_jwt_secret`

3. For R2 URL in settings, use `http://127.0.0.1:8787/api/file`

**Email Sending via Resend**

1. Sign up at Resend, go to Domains → Add & verify domain
2. Go to API Keys → Create Key → Copy token → Paste in project settings

3. Go to Webhooks → Add `https://your-domain/api/webhooks` → Select all relevant events

## Directory Structure

```
cloud-mail
├── mail-worker
│   ├── src
│   │   ├── api
│   │   ├── const
│   │   ├── email
│   │   ├── entity
│   │   ├── error
│   │   ├── hono
│   │   ├── init
│   │   ├── model
│   │   ├── security
│   │   ├── service
│   │   ├── utils
│   │   └── index.js
│   ├── package.json
│   └── wrangler.toml
└── mail-vue
    ├── src
    │   ├── assets
    │   ├── axios
    │   ├── components
    │   ├── layout
    │   ├── request
    │   ├── router
    │   ├── store
    │   ├── utils
    │   ├── views
    │   ├── app.vue
    │   ├── main.js
    │   └── style.css
    ├── package.json
    └── env.dev
```

## License

This project is licensed under [MIT](LICENSE)

## Community

[Telegram](https://t.me/cloud_mail_tg)
