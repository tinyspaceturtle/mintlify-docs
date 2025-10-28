---
title: 'Quickstart'
description: 'Get started with TinyBrain in 5 minutes'
---

# Get Started in 5 Minutes

TinyBrain is a memory infrastructure for AI applications. This guide will get you up and running quickly.

## Step 1: Get Your API Key

1. Sign up at [tinybrainlab.ai](https://tinybrainlab.ai/sign-up)
2. Navigate to **API Platform** in the dashboard
3. Click **Create API Key**
4. Copy your key (starts with `tb_`)

<Warning>
  Keep your API key secure! Never commit it to version control.
</Warning>

## Step 2: Install the SDK

<CodeGroup>

```bash npm
npm install @tinybrain/sdk
```

```bash yarn
yarn add @tinybrain/sdk
```

```bash pnpm
pnpm add @tinybrain/sdk
```

```bash Python
pip install tinybrain
```

</CodeGroup>

## Step 3: Store Your First Memory

<CodeGroup>

```typescript TypeScript
import { TinyBrain } from '@tinybrain/sdk';

const tb = new TinyBrain({
  apiKey: process.env.TINYBRAIN_API_KEY,
  tenantId: 'user-123' // Your user identifier
});

// Store a memory
const memory = await tb.memory.create({
  type: 'EMAIL',
  title: 'Product Launch Discussion',
  content: 'Discussed Q4 launch timeline with Sarah. Target: Nov 15.',
  importance: 0.85,
  metadata: {
    sender: 'sarah@company.com',
    timestamp: Date.now()
  }
});

console.log('Memory stored:', memory.id);
```

```python Python
from tinybrain import TinyBrain

tb = TinyBrain(
    api_key=os.environ['TINYBRAIN_API_KEY'],
    tenant_id='user-123'
)

# Store a memory
memory = tb.memory.create(
    type='EMAIL',
    title='Product Launch Discussion',
    content='Discussed Q4 launch timeline with Sarah. Target: Nov 15.',
    importance=0.85,
    metadata={
        'sender': 'sarah@company.com',
        'timestamp': int(time.time() * 1000)
    }
)

print(f'Memory stored: {memory.id}')
```

```bash cURL
curl -X POST https://api.tinybrain.dev/api/v1/memory \
  -H "Authorization: Bearer $TINYBRAIN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "tenantId": "user-123",
    "type": "EMAIL",
    "title": "Product Launch Discussion",
    "content": "Discussed Q4 launch timeline with Sarah. Target: Nov 15.",
    "importance": 0.85,
    "metadata": {
      "sender": "sarah@company.com"
    }
  }'
```

</CodeGroup>

## Step 4: Search Memories

TinyBrain uses semantic search - find by meaning, not exact text:

<CodeGroup>

```typescript TypeScript
// Semantic search
const results = await tb.memory.search({
  query: 'When is the product launch?',
  limit: 5
});

results.forEach(memory => {
  console.log(`${memory.title} (score: ${memory.score})`);
  console.log(memory.content);
});
```

```python Python
# Semantic search
results = tb.memory.search(
    query='When is the product launch?',
    limit=5
)

for memory in results:
    print(f"{memory.title} (score: {memory.score})")
    print(memory.content)
```

```bash cURL
curl -X POST https://api.tinybrain.dev/api/v1/memory/search \
  -H "Authorization: Bearer $TINYBRAIN_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "tenantId": "user-123",
    "query": "When is the product launch?",
    "limit": 5
  }'
```

</CodeGroup>

**Response:**
```json
{
  "success": true,
  "data": [
    {
      "id": "mem_abc123",
      "title": "Product Launch Discussion",
      "content": "Discussed Q4 launch timeline with Sarah. Target: Nov 15.",
      "score": 0.92,
      "type": "EMAIL"
    }
  ]
}
```

## Step 5: Use Memory in AI Chat

Build an AI assistant that remembers:

<CodeGroup>

```typescript TypeScript
// Get relevant context
const context = await tb.memory.search({
  query: userMessage,
  limit: 10
});

// Build prompt with memory
const prompt = `
Context from memory:
${context.map(m => `- ${m.title}: ${m.content}`).join('\n')}

User: ${userMessage}
Assistant:
`;

// Send to your LLM
const response = await openai.chat.completions.create({
  model: 'gpt-4',
  messages: [
    { role: 'system', content: prompt },
    { role: 'user', content: userMessage }
  ]
});

// Store the conversation
await tb.memory.create({
  type: 'CHAT',
  title: `Chat: ${userMessage.slice(0, 50)}`,
  content: `User: ${userMessage}\nAssistant: ${response.choices[0].message.content}`,
  importance: 0.6
});
```

```python Python
# Get relevant context
context = tb.memory.search(
    query=user_message,
    limit=10
)

# Build prompt with memory
context_text = '\n'.join([f"- {m.title}: {m.content}" for m in context])
prompt = f"""
Context from memory:
{context_text}

User: {user_message}
Assistant:
"""

# Send to your LLM
response = openai.chat.completions.create(
    model='gpt-4',
    messages=[
        {'role': 'system', 'content': prompt},
        {'role': 'user', 'content': user_message}
    ]
)

# Store the conversation
tb.memory.create(
    type='CHAT',
    title=f"Chat: {user_message[:50]}",
    content=f"User: {user_message}\nAssistant: {response.choices[0].message.content}",
    importance=0.6
)
```

</CodeGroup>

## You're Done! 🎉

You now have:
- ✅ Memory storage with semantic search
- ✅ AI context that remembers past interactions
- ✅ Automatic deduplication and importance scoring

## Next Steps

<CardGroup cols={2}>

<Card title="View Examples" icon="code" href="/examples/ai-assistant">
  See complete working applications
</Card>

<Card title="Core Concepts" icon="book" href="/core-concepts/memory-types">
  Learn about memory types and intelligence
</Card>

<Card title="API Reference" icon="terminal" href="/api-reference/rest-api">
  Explore all endpoints
</Card>

<Card title="Best Practices" icon="lightbulb" href="/resources/best-practices">
  Optimization tips and patterns
</Card>

</CardGroup>

## Common Use Cases

### Personal AI Assistant
```typescript
// Store user preferences
await tb.memory.create({
  type: 'IDENTITY',
  title: 'Communication Preference',
  content: 'User prefers concise, bullet-point responses',
  importance: 0.9
});

// Later, retrieve for context
const prefs = await tb.memory.search({ query: 'How does user prefer to communicate?' });
```

### Meeting Notes Intelligence
```typescript
// Store meeting transcript
await tb.memory.create({
  type: 'EVENT',
  title: 'Q4 Planning Meeting',
  content: 'Attendees: Sarah, John, Alex. Topics: Revenue targets, hiring plan...',
  importance: 0.8,
  metadata: {
    eventDate: '2025-11-01',
    attendees: ['sarah@co.com', 'john@co.com']
  }
});

// Find related past meetings
const related = await tb.memory.search({ query: 'Previous Q4 planning discussions' });
```

### Customer Support Memory
```typescript
// Track customer interactions
await tb.memory.create({
  type: 'TASK',
  title: 'Customer Issue: Payment Failed',
  content: 'Customer ID 456. Issue: Payment declined. Resolution: Updated card.',
  importance: 0.7,
  metadata: {
    customerId: '456',
    status: 'resolved'
  }
});
```

## Need Help?

- 💬 [Join our Discord](https://discord.gg/tinybrain)
- 📧 Email: support@tinybrain.dev
- 📖 [Read the full docs](/)
- 🐛 [Report a bug](https://github.com/tinybrain/tinybrain/issues)
