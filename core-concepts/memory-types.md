# Memory Types

TinyBrain supports 13 cognitive memory types, each optimized for different kinds of information.

---

## Overview

| Type | Purpose | Example Use Case |
|------|---------|------------------|
| **Episodic** | Specific events | "Had lunch with John on Monday" |
| **Semantic** | Facts and knowledge | "Paris is the capital of France" |
| **Procedural** | How-to processes | "Deploy: run tests → build → push" |
| **Working** | Temporary context | "Currently debugging OAuth issue" |
| **Prospective** | Future intentions | "Review Q4 budget by Friday" |
| **Emotional** | Feelings/reactions | "Frustrated with slow API" |
| **Contextual** | Situational context | "In team standup meeting" |
| **Identity** | Personal attributes | "I prefer concise responses" |
| **Relational** | People connections | "Sarah reports to John (CEO)" |
| **Event** | Calendar items | "All-hands Monday 10am" |
| **Predictive** | Forecasts | "Sarah usually responds in 2hrs" |
| **Task** | Action items | "Review PR #234" |
| **Decision** | Choices made | "Decided to use Fastify for API" |

---

## Detailed Descriptions

### Episodic Memory
**Purpose:** Store specific events that happened

**When to use:**
- Logging user actions
- Recording conversations
- Tracking interactions

**Example:**
```typescript
{
  type: 'episodic',
  content: 'User purchased Premium plan on 2025-10-25',
  tenantId: 'user_123',
  metadata: {
    action: 'purchase',
    plan: 'premium',
    date: '2025-10-25'
  }
}
```

### Semantic Memory
**Purpose:** Store facts, knowledge, and general information

**When to use:**
- Company information
- Product details
- General knowledge

**Example:**
```typescript
{
  type: 'semantic',
  content: 'Sarah Chen is VP of Sales at Acme Corp, based in San Francisco',
  tenantId: 'user_123',
  metadata: {
    entity: 'person',
    name: 'Sarah Chen',
    title: 'VP of Sales',
    company: 'Acme Corp'
  }
}
```

### Procedural Memory
**Purpose:** Store how-to processes and workflows

**When to use:**
- Standard operating procedures
- Workflows
- Repeated processes

**Example:**
```typescript
{
  type: 'procedural',
  content: 'Invoice approval process: Vendor check → Budget verify → Manager approval → Submit to accounting',
  tenantId: 'user_123',
  metadata: {
    workflowType: 'invoice_approval',
    steps: 4
  }
}
```

### Identity Memory
**Purpose:** Store user preferences, style, and attributes

**When to use:**
- Communication preferences
- User settings
- Behavioral traits

**Example:**
```typescript
{
  type: 'identity',
  content: 'User prefers detailed explanations with code examples',
  tenantId: 'user_123',
  metadata: {
    category: 'communication_style'
  }
}
```

### Predictive Memory
**Purpose:** Store forecasts and expected behaviors

**When to use:**
- Response time predictions
- Behavior forecasts
- Trend analysis

**Example:**
```typescript
{
  type: 'predictive',
  content: 'Sarah Chen typically responds to emails within 2 hours during work hours',
  tenantId: 'user_123',
  metadata: {
    predictionType: 'response_time',
    target: 'sarah@acmecorp.com',
    avgMinutes: 120,
    confidence: 0.87
  }
}
```

---

## Choosing the Right Type

Use this decision tree:

```
Is it about a specific event that happened?
  → YES: Use EPISODIC

Is it a fact or piece of knowledge?
  → YES: Use SEMANTIC

Is it a process or workflow?
  → YES: Use PROCEDURAL

Is it something to do in the future?
  → YES: Use TASK or PROSPECTIVE

Is it about user preferences or identity?
  → YES: Use IDENTITY

Is it a forecast or prediction?
  → YES: Use PREDICTIVE

Is it about a person or relationship?
  → YES: Use RELATIONAL

Is it about emotions or feelings?
  → YES: Use EMOTIONAL
```

---

## Memory Type Intelligence

Different memory types trigger different intelligence extractors:

| Memory Type | Triggers | Extracts |
|-------------|----------|----------|
| **Episodic** | VIP Detection | Frequent contacts |
| **Task** | Workflow Detection | Recurring processes |
| **Identity** | Preference Learning | User patterns |
| **Emotional** | Sentiment Analysis | Mood tracking |
| **Event** | Schedule Optimization | Meeting patterns |

---

## Best Practices

### ✅ DO

- Use specific types for better intelligence extraction
- Include rich metadata
- Be consistent with typing

### ❌ DON'T

- Default everything to EPISODIC
- Mix types (one memory = one type)
- Over-complicate type selection

---

## Next Steps

- [Semantic Search](./semantic-search.md) - How search works across types
- [Intelligence Layer](./intelligence-layer.md) - Automatic extraction
- [Architecture](./architecture.md) - Complete technical overview
