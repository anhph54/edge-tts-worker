# edge-tts-worker

Deploy Microsoft Edge TTS as an OpenAI-compatible API on your own Cloudflare account. Free.

[![Deploy to Cloudflare Workers](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https://github.com/user/edge-tts-worker)

## Deploy

```bash
npm install
npx wrangler deploy
```

Optionally set an API key to protect your endpoint:

```bash
npx wrangler secret put API_KEY
```

## API

### `POST /v1/audio/speech`

OpenAI-compatible text-to-speech endpoint.

```bash
curl -X POST https://your-worker.workers.dev/v1/audio/speech \
  -H "Content-Type: application/json" \
  -d '{
    "model": "tts-1",
    "input": "Hello, world!",
    "voice": "en-US-EmmaMultilingualNeural",
    "speed": 1.0,
    "response_format": "mp3"
  }' \
  --output speech.mp3
```

| Parameter | Description | Default |
|---|---|---|
| `model` | Ignored (accepted for compatibility) | — |
| `input` | Text to synthesize (required) | — |
| `voice` | Edge TTS voice name | `en-US-EmmaMultilingualNeural` |
| `speed` | Speech rate, 0.5–2.0 | `1.0` |
| `response_format` | Only `mp3` supported | `mp3` |

If `API_KEY` is set, include `Authorization: Bearer <key>` header.

### `GET /v1/voices`

Returns the list of available voices as JSON.

```bash
curl https://your-worker.workers.dev/v1/voices
```

### `GET /`

A minimal HTML test page with text input, voice selector, speed slider, and play button.

## Development

```bash
npm install
npm run dev
```

## Disclaimer

This project uses Microsoft's unofficial Edge TTS endpoint. There is no SLA or uptime guarantee. Use at your own risk.

## License

AGPL-3.0
