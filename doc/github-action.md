
## GitHub Action Deployment

**Configure Your GitHub Repository**

1. Fork or clone the repository [https://github.com/eoao/cloud-mail](https://github.com/eoao/cloud-mail)
2. Go to your GitHub repository settings
3. Navigate to Settings → Secrets and variables → Actions → New repository secret
4. Add the following secrets:

| Secret Name            | Required | Purpose                                                       |
|------------------------|:--------:|---------------------------------------------------------------|
| `CLOUDFLARE_API_TOKEN` |    ✅    | Cloudflare API token (requires Workers & related resource permissions) |
| `CLOUDFLARE_ACCOUNT_ID`|    ✅    | Your Cloudflare account ID                                   |
| `D1_DATABASE_ID`       |    ✅    | The ID of your D1 database                                   |
| `KV_NAMESPACE_ID`      |    ✅    | The ID of your KV namespace                                  |
| `R2_BUCKET_NAME`       |    ✅    | Your R2 bucket name                                          |
| `DOMAIN`               |    ✅    | Domain(s) for your email service (e.g., `["xx.xx"]`, separate multiple with commas) |
| `ADMIN`                |    ✅    | Admin email address (e.g., `admin@example.com`)             |
| `JWT_SECRET`           |    ✅    | A long random string for generating and verifying JWT tokens |
| `INIT_URL`             |    ❌    | (Optional) Worker URL to initialize database after deployment (see manual init example below) |

---

**Get Your Cloudflare API Token**

1. Visit the [Cloudflare Dashboard](https://dash.cloudflare.com/profile/api-tokens)
2. Create a new API token
3. Use the "Edit Cloudflare Workers" template and add required permissions as shown below:
   ![dc2e1dc8dcd217644759c46c6c705de1](https://i.miji.bid/2025/07/07/dc2e1dc8dcd217644759c46c6c705de1.png)
4. Save and copy the token to `CLOUDFLARE_API_TOKEN` in your GitHub secrets

**Get Your Cloudflare Account ID**

1. Your account ID can be found in the account settings of the Cloudflare dashboard.
2. Copy it to `CLOUDFLARE_ACCOUNT_ID` in GitHub secrets

**Run the Workflow**

1. Go to the Actions tab and manually run the workflow. Once set up, future updates will auto-deploy to Cloudflare Workers.  
   If you didn't set `INIT_URL`, manually visit `https://your-domain/api/init/your_jwt_secret` in the browser to initialize the database.

2. To sync upstream changes automatically, use a bot or click the "Sync Upstream" button manually.
