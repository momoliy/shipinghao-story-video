# Doubao Story Video（豆包配音图片故事视频）

一个用于 Codex 和 WorkBuddy 的分步式 Skill，带你从选题、对标、文案、**豆包配音**、分镜、生图，一直做到预览和成片。

> 本项目基于 [aaronyi97/image-story-video-wizard](https://github.com/aaronyi97/image-story-video-wizard)（MIT 协议）修改，保留原版 16 阶段流程。主要改动：配音只用豆包 Seed-TTS 2.0，新增豆包接入与调用规范，状态文件固定记录豆包为唯一配音服务。详见 [CHANGELOG.md](CHANGELOG.md)。

## 它怎么带你往下做

每一轮都会说清楚五件事：

1. `现在进行到：`
2. `我现在会做：`
3. `你现在只需要：`
4. `完成后我会交付：`
5. `确认后下一步：`

完整阶段：

`START → BRIEF → BENCHMARKS → WRITING_PACK → SCRIPT → VOICE → STORYBOARD → VISUAL_STYLE → CHARACTER_ANCHORS → IMAGE_PROMPTS → IMAGE_GENERATION → ASSET_QC → MUSIC → PREVIEW → FINAL_RENDER → FEEDBACK`

关键确认点：

- 对标方向没确认，不做写作包。
- 文案没定稿，不生成完整配音。
- 画风、文字风格和样图没确认，不批量生图。
- 预览没通过，不渲染最终成片。
- 某一步失败时，只回到最早受影响的阶段，不把整个项目推倒重来。

## 配音：只用豆包

- 唯一配音服务：豆包 Seed-TTS 2.0（火山引擎）。不提供、也不会自动换成其他 TTS。
- 密钥只放本地：在项目 `.env` 里写 `DOUBAO_TTS_APP_ID` 和 `DOUBAO_TTS_ACCESS_TOKEN`。`.env` 已加入 `.gitignore`，不要发到对话里。
- 流程：用同一段约 20 秒的文字试听 5–10 个音色，先定音色，再试语速，最后生成整期配音并尽量带时间戳。
- 豆包没开通或调用失败时，Skill 会停在配音阶段，带你把豆包配好，不会偷偷换别的。

入口：

- [豆包语音官方产品页](https://www.volcengine.com/products/Audio-editing-and-sound-processing)
- [豆包语音控制台](https://console.volcengine.com/speech/app)
- [豆包语音官方快速入门](https://www.volcengine.com/docs/6561/163043?lang=zh)

调用细节见 [references/doubao-tts.md](references/doubao-tts.md)。

## 适合的项目

- AI 讲书、历史故事、情感故事和有声故事。
- 豆包配音加配图的图片联播视频。
- 需要人物一致性、固定画风、字幕和文字卡的静态图叙事视频。

只需要一篇文案、一张图或普通剪辑时，不需要用这个 Skill。

## 一句话安装

把下面这句话完整发给 Codex：

> 请使用 skill-installer 从 https://github.com/【你的GitHub用户名】/doubao-story-video 安装 Skill。Skill 位于仓库根目录，安装名使用 doubao-story-video。安装完成后告诉我下一轮可以直接启动。

装好后直接发：

> 使用 $doubao-story-video 开始一个新项目。我想做一期【选题】的图片联播视频，请主动带我往下做。

## 终端安装

```bash
git clone https://github.com/【你的GitHub用户名】/doubao-story-video.git ~/.codex/skills/doubao-story-video
```

## 其他阶段的默认路线

- 长文案：先用 Codex 完成对标学习和写作包，再交给 WorkBuddy 中的 Kimi K3；页面提供时选 Max 模式、最高思考强度和 1M 上下文。
- 生图：先做 3–5 张样图，锁画风、人物母版和文字样式；手动路线默认一个新对话只跑一条提示词、出一张图。
- 剪辑：素材齐全后优先用 HyperFrames 组装，先看预览，确认后再渲染成片。

项目用 `PROJECT_STATE.json` 记录当前阶段、已确认的决定、产物路径和下一个要你回答的问题，换宿主也能接着做。

## 验证

```bash
python3 -m unittest discover -s tests -v
```

## 致谢

流程框架、状态机、写作规范和状态脚本来自 [aaronyi97/image-story-video-wizard](https://github.com/aaronyi97/image-story-video-wizard)，作者 Aaron Yi。本项目在此基础上做了豆包专用化修改。

## License

[MIT](LICENSE)。保留原作者版权声明。
