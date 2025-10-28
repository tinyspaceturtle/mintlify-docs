# Installation

Install the TinyBrain SDK for your preferred language.

---

## TypeScript / Node.js

### Requirements
- Node.js 18 or higher
- npm, yarn, or pnpm

### Install via npm

```bash
npm install @tinybrain/sdk
```

### Install via yarn

```bash
yarn add @tinybrain/sdk
```

### Install via pnpm

```bash
pnpm add @tinybrain/sdk
```

### Verify Installation

```typescript
import { TinyBrain } from '@tinybrain/sdk';

console.log('TinyBrain SDK loaded successfully!');
```

---

## Python

### Requirements
- Python 3.9 or higher
- pip

### Install via pip

```bash
pip install tinybrain-sdk
```

### Install from source

```bash
git clone https://github.com/tinybrain/sdk-python
cd sdk-python
pip install -e .
```

### Verify Installation

```python
from tinybrain_sdk import TinyBrain

print('TinyBrain SDK loaded successfully!')
```

---

## Next Steps

- [Authentication](./authentication.md) - Set up your API key
- [First API Call](./first-api-call.md) - Make your first request
- [Quickstart Guide](./quickstart.md) - Complete 5-minute tutorial
