# Radzor Component Spec (RCS) 📜

The **universal manifest standard for LLM-driven component integration.**

RCS defines a structured JSON schema (`radzor.manifest.json`) that describes what a software component does, what data it requires, the events it emits, and the precise shape of its inputs and outputs. 

By standardizing this information, **AI coding agents (like Claude, Cursor, GitHub Copilot) can integrate complex logic with zero hallucinations.**

## Why RCS?

- **Anti-Hallucination:** LLMs often hallucinate SDK methods or use outdated API documentation when you ask them to "implement Stripe" or "use Whisper API". RCS provides the definitive, up-to-date interface.
- **Dependency Awareness:** Declares required environment variables (API keys) and npm/pip packages so the CLI can auto-install them.
- **Composability:** RCS manifests define strict `inputs` and `outputs` types, ensuring that an LLM can safely chain the output of `Component A` into the input of `Component B` (e.g., passing a microphone `Blob` from `audio-capture` into `speech-to-text`).

## The Schema

The official JSON Schema is available at:
- [`radzor-manifest.schema.json`](./radzor-manifest.schema.json)
- `https://radzor.io/schema/manifest/1.0.0`

## Structure

Every component using the RCS standard contains a `radzor.manifest.json` file at its root. 

```json
{
  "radzor": "1.0.0",
  "name": "@radzor/speech-to-text",
  "version": "0.1.0",
  "description": "Audio transcription using OpenAI Whisper or Deepgram APIs.",
  "languages": ["typescript", "python"],
  "category": "ai",
  "runtime": "server",
  "inputs": [
    {
      "name": "apiKey",
      "type": "string",
      "description": "API Key for the chosen provider",
      "envVar": "OPENAI_API_KEY",
      "required": true
    }
  ],
  "outputs": [
    {
      "name": "transcriptionResult",
      "type": "{ text: string; language: string; duration: number }",
      "description": "The final transcribed text and metadata."
    }
  ],
  "actions": [
    {
      "name": "transcribe",
      "params": [
        { "name": "audio", "type": "File | Blob | Buffer" }
      ],
      "returns": "Promise<{ text: string }>"
    }
  ],
  "llm": {
    "integrationPrompt": "llm/integration.md",
    "usageExamples": "llm/examples.md",
    "constraints": "Must run in a server environment. Buffer support requires Node.js."
  }
}
```

## Validate your Manifest

Use the Radzor CLI to validate any local directory containing a `radzor.manifest.json`:

```bash
npx radzor@latest validate .
```

## Learn More

- [Radzor Platform](https://radzor.io)
- [Official Components Catalog](https://radzor.io/components)
- [Radzor CLI](https://github.com/radzor-io/cli)

## License

MIT
