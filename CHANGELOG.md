# 更新记录

## 0.1.0 · 2026-11-09 · 基于 image-story-video-wizard 创建
- 改名为 doubao-story-video，16 阶段流程保持不变。
- 配音阶段只使用豆包 Seed-TTS 2.0，禁止换用其他 TTS。
- 新增 `references/doubao-tts.md`：开通、本地密钥、调用、试听、失败处理。
- `PROJECT_STATE.json` 初始化时固定 `tts_provider = doubao`，校验脚本会检查该值。
- 宿主能力新增 `doubao_tts`。
- 新增测试：配音阶段只用豆包、状态文件记录豆包。
- README 重写，加入来源与致谢。

上游项目历史见 git log（保留了原仓库提交记录）。
