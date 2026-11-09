# Doubao TTS (豆包语音)

This Skill uses one TTS provider: Doubao (豆包) Seed-TTS 2.0 on Volcengine (火山引擎). There is no fallback provider.

## Access

1. Official pages (verify they are current before guiding the user):
   - Product: https://www.volcengine.com/products/Audio-editing-and-sound-processing
   - Console: https://console.volcengine.com/speech/app
   - Quick start: https://www.volcengine.com/docs/6561/163043?lang=zh
2. The user creates an application in the speech console and enables the Seed-TTS 2.0 (语音合成大模型 2.0) service.
3. The user stores credentials locally, never in chat:

```bash
# project .env (already ignored by .gitignore)
DOUBAO_TTS_APP_ID=...
DOUBAO_TTS_ACCESS_TOKEN=...
```

4. The Skill checks only that the variables exist and that one short test request succeeds. It never prints, logs, or copies their values.

## Calling rules

- Confirm the current endpoint, resource/cluster ID, parameters, and voice list from the official docs at the time of use; product labels and parameters change.
- Use Seed-TTS 2.0, not a legacy generation, unless the user explicitly chooses otherwise.
- Explain cost or quota impact before generating full narration.
- Request timestamps when available so STORYBOARD can use real sentence timing.
- Long scripts: split at sentence or paragraph boundaries, keep a stable segment ID, and concatenate in order. Do not cut inside a sentence.

## Audition and record

- Same ~20-second sample text for five to ten voices; file names `audio/auditions/voice-<voice_id>.mp3`.
- After the user picks a voice, three rate auditions (for example slower / default / faster) with the same text.
- Record in `PROJECT_STATE.json` decisions: `tts_provider` = `doubao` (fixed), `doubao_voice_id`, `speech_rate`, each with `source` and `status`.

## If Doubao fails

Report the actual error (quota, permission, network, parameter) without exposing secrets, keep VOICE at `待确认` or `需要返工`, and help the user fix Doubao access. Do not switch providers.
