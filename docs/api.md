# API Reference

## Authentication

If the `API_KEY` environment variable is set, all endpoints (except `GET /`) require an `Authorization: Bearer <key>` header.

## Endpoints

### `POST /v1/audio/speech`

Synthesize text to speech. Returns streaming `audio/mpeg` data.

**Request body** (JSON):

```json
{
  "model": "tts-1",
  "input": "Text to synthesize",
  "voice": "en-US-EmmaMultilingualNeural",
  "speed": 1.0,
  "response_format": "mp3"
}
```

- `input` (required): The text to synthesize.
- `voice` (optional): Edge TTS voice short name. Default: `en-US-EmmaMultilingualNeural`. Get the full list from `GET /v1/voices`.
- `speed` (optional): Float between 0.5 and 2.0. Default: `1.0`. Converted internally to Edge TTS rate format (e.g. 1.5 becomes `+50%`).
- `model` (optional): Accepted for OpenAI compatibility but ignored.
- `response_format` (optional): Only `mp3` is supported.

**Response**: Streaming `audio/mpeg` body.

**Errors**: Returns JSON in OpenAI error format:

```json
{
  "error": {
    "message": "description",
    "type": "invalid_request_error",
    "code": 400
  }
}
```

### `GET /v1/voices`

Returns the full list of available voices from Microsoft Edge TTS.

**Response**: JSON array of voice objects:

```json
[
  {
    "Name": "Microsoft Server Speech Text to Speech Voice (en-US, EmmaMultilingualNeural)",
    "ShortName": "en-US-EmmaMultilingualNeural",
    "Gender": "Female",
    "Locale": "en-US",
    "FriendlyName": "Microsoft Emma Online (Natural) - English (United States)",
    "VoiceTag": {
      "ContentCategories": ["General"],
      "VoicePersonalities": ["Friendly", "Positive"]
    }
  }
]
```

The voice list is cached in memory after the first request.

### `GET /`

Serves a minimal HTML test page for trying out TTS in the browser.

### `OPTIONS *`

Returns CORS preflight headers. All origins are allowed (`*`).
