# Authentication

Learn how to authenticate with the TinyBrain API using API keys.

---

## Getting Your API Key

1. Sign up at [app.tinybrain.dev](https://app.tinybrain.dev)
2. Navigate to **Settings → API Keys**
3. Click **"Create New API Key"**
4. Give it a descriptive name (e.g., "Production", "Development")
5. Copy the key immediately (it won't be shown again)

**Your API key starts with:** `tb_`

---

## Storing Your API Key Securely

### Environment Variables (Recommended)

Create a `.env` file in your project root:

```bash
TINYBRAIN_API_KEY=tb_your_key_here
```

**Important:** Add `.env` to your `.gitignore`:

```bash
# .gitignore
.env
.env.local
.env.*.local
```

### TypeScript/Node.js

```typescript
import { TinyBrain } from '@tinybrain/sdk';

const client = new TinyBrain({
  apiKey: process.env.TINYBRAIN_API_KEY
});
```

### Python

```python
import os
from tinybrain_sdk import TinyBrain

client = TinyBrain(api_key=os.getenv('TINYBRAIN_API_KEY'))
```

---

## API Key Scopes

API keys can have different scopes:

| Scope | Description |
|-------|-------------|
| `memories:read` | Read memories |
| `memories:write` | Create/update memories |
| `memories:delete` | Delete memories |
| `intelligence:read` | Access intelligence features |
| `integrations:*` | Manage OAuth integrations |
| `*` | Full access (default) |

---

## Rate Limits

API keys are subject to rate limits based on your plan:

| Plan | Requests/Minute | Requests/Day |
|------|-----------------|--------------|
| Free | 100 | 10,000 |
| Startup | 500 | 100,000 |
| Growth | 2,000 | 1,000,000 |
| Enterprise | Custom | Custom |

**Rate limit headers** are included in every response:

```
X-RateLimit-Limit-Minute: 100
X-RateLimit-Remaining-Minute: 87
X-RateLimit-Reset-Minute: 1698249600000
```

---

## Security Best Practices

### ✅ DO

- Store API keys in environment variables
- Use different keys for development and production
- Rotate keys regularly (every 90 days recommended)
- Set minimum required scopes
- Revoke keys immediately if compromised

### ❌ DON'T

- Commit API keys to version control
- Share API keys in public channels
- Use production keys in development
- Hard-code keys in your application
- Expose keys in client-side code

---

## Rotating API Keys

To rotate your key without downtime:

1. Create a new API key in the dashboard
2. Update your production environment with the new key
3. Wait for all services to pick up the new key (check logs)
4. Revoke the old API key

**Tip:** Have overlapping keys during rotation for zero downtime.

---

## Troubleshooting

### "Invalid API key" Error

**Cause:** Key is incorrect or has been revoked

**Solution:**
1. Check the key starts with `tb_`
2. Verify no extra spaces or line breaks
3. Confirm the key hasn't been revoked in the dashboard
4. Generate a new key if needed

### "Unauthorized" Error

**Cause:** Key lacks required scopes

**Solution:**
1. Check the endpoint you're calling
2. Verify your key has the necessary scope
3. Create a new key with broader scopes if needed

---

## Next Steps

- [First API Call](./first-api-call.md) - Test your authentication
- [Quickstart Guide](./quickstart.md) - Complete tutorial
- [API Reference](../api-reference/rest-api.md) - All endpoints
