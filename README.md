# Radzor Component Spec (RCS)

The universal manifest standard for LLM-driven component integration.

## What is RCS?

RCS defines a JSON manifest format (`radzor.manifest.json`) that describes a component's inputs, outputs, actions, events, and composability — everything an LLM needs to integrate a component without reading source code.

## Schema

The JSON Schema is available at:
- [`radzor-manifest.schema.json`](./radzor-manifest.schema.json)
- `https://radzor.io/schema/manifest/1.0.0`

## Examples

See the [`examples/`](./examples) directory for real-world manifests:

| Component | Description |
|-----------|-------------|
| [Audio Capture](./examples/audio-capture.manifest.json) | Browser audio recording with MediaRecorder API |
| [OAuth](./examples/auth-oauth.manifest.json) | Multi-provider authentication flow |
| [Stripe Checkout](./examples/stripe-checkout.manifest.json) | Payment processing with Stripe |
| [Realtime Chat](./examples/realtime-chat.manifest.json) | WebSocket-based messaging |

## Quick Start

Add a `radzor.manifest.json` to the root of your component:

```json
{
  "radzor": "1.0.0",
  "name": "my-component",
  "version": "1.0.0",
  "description": "What this component does",
  "languages": ["typescript"],
  "category": "ui",
  "inputs": { ... },
  "outputs": { ... }
}
```

Validate against the schema:

```bash
npx ajv validate -s radzor-manifest.schema.json -d your-component/radzor.manifest.json
```

## Links

- [Radzor Platform](https://radzor.io)
- [Full Documentation](https://radzor.io/docs)

## License

MIT
