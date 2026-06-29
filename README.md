# ASR & TTS Survey

本仓库用于整理和评估 **开源 ASR / TTS 模型** 与 **商业化 ASR / TTS 云 API**，重点面向以下产品场景：

- AI 视频翻译
- 自动字幕生成
- 多语种字幕本地化
- AI 配音
- 声音克隆
- 跨语言声音克隆
- 商品视频 / 短视频 / 课程视频 / 口播视频本地化

> Last updated: 2026-06-29  
> 说明：模型能力、API 价格、许可证和商用条款变化较快。商用前请务必复核官方文档、模型卡、价格页和 LICENSE。

---

## 1. TL;DR

### 1.1 开源模型推荐

| 方向 | 第一梯队 | 说明 |
|---|---|---|
| ASR | Qwen3-ASR, FireRedASR2S, faster-whisper + WhisperX, FunASR / SenseVoice | 适合字幕生成、中文识别、多语种识别、时间戳对齐 |
| TTS | Qwen3-TTS, IndexTTS2, CosyVoice, VoxCPM2, Chatterbox, Spark-TTS | 适合高质量配音、声音克隆、多语种生成 |

### 1.2 商业 API 推荐

| 方向 | 第一梯队 | 说明 |
|---|---|---|
| ASR API | OpenAI Transcribe, Deepgram, Google Speech-to-Text, AssemblyAI, 阿里云, 腾讯云, 火山引擎 | 适合快速产品化、批量字幕、实时字幕 |
| TTS API | ElevenLabs, OpenAI TTS, Google Cloud TTS, Azure Speech TTS, Amazon Polly, Deepgram Aura, 阿里 CosyVoice, 腾讯 TTS, 火山豆包语音 | 适合固定音色配音、声音克隆、视频配音 |

## 2. 开源 ASR 模型

### 2.1 推荐结论

| 场景 | 推荐模型 |
|---|---|
| 中文 / 中英混说识别 | Qwen3-ASR, FireRedASR2S, FunASR / SenseVoice |
| 多语种视频字幕 | Qwen3-ASR, faster-whisper, WhisperX |
| 字幕时间戳对齐 | Qwen3-ForcedAligner, WhisperX |
| 中文方言 / 口音 | FireRedASR2S, Qwen3-ASR, FunASR |
| 实时字幕 | Qwen3-ASR-0.6B, FunASR streaming, Voxtral Realtime |
| 端侧 / 离线部署 | whisper.cpp, sherpa-onnx, Vosk, Moonshine |
| 工程稳定基线 | faster-whisper + WhisperX |

### 2.2 模型列表

| 模型 / 项目 | 类型 | 许可证 | 主要特点 | 优先级 |
|---|---|---:|---|---:|
| [Qwen3-ASR](https://github.com/QwenLM/Qwen3-ASR) | ASR / Forced Alignment | Apache-2.0 | 支持 52 种语言和方言；包含 Qwen3-ForcedAligner；适合多语种字幕和对齐 | ★★★★★ |
| [FireRedASR2S](https://github.com/FireRedTeam/FireRedASR2S) | ASR + VAD + LID + Punc | 需核对 | 一体化 ASR 系统，支持普通话、20+ 中文方言/口音、英文、中英混说、歌唱转写 | ★★★★★ |
| [faster-whisper](https://github.com/SYSTRAN/faster-whisper) | Whisper 高性能推理 | MIT | 基于 CTranslate2，速度快、显存低、工程成熟 | ★★★★★ |
| [WhisperX](https://github.com/m-bain/whisperX) | ASR + 对齐 + 说话人分离 | BSD-2-Clause | 词级时间戳、VAD、批处理、diarization | ★★★★★ |
| [FunASR](https://github.com/modelscope/FunASR) | ASR 工具链 | MIT / 模型协议需核对 | 工业级语音识别工具链，支持 VAD、标点、说话人分离、流式识别 | ★★★★☆ |
| [SenseVoice](https://github.com/FunAudioLLM/SenseVoice) | 语音理解模型 | 需核对 | ASR、语言识别、情绪识别、音频事件检测 | ★★★★☆ |
| [OpenAI Whisper](https://github.com/openai/whisper) | ASR | MIT | 多语种基线模型，生态成熟 | ★★★★☆ |
| [whisper.cpp](https://github.com/ggml-org/whisper.cpp) | Whisper 端侧推理 | MIT | C/C++ 实现，支持 CPU、移动端、量化部署 | ★★★★☆ |
| [NVIDIA Parakeet](https://huggingface.co/nvidia) | ASR | 多为 CC-BY-4.0 | 英语 / 欧洲语言识别强，支持时间戳 | ★★★☆☆ |
| [NVIDIA Canary](https://huggingface.co/nvidia) | ASR / AST | 多为 CC-BY-4.0 | 欧洲语言 ASR / 语音翻译 | ★★★☆☆ |
| [Voxtral](https://huggingface.co/mistralai) | Speech LLM / ASR | 需核对 | 实时语音理解和转写候选 | ★★★☆☆ |
| [WeNet](https://github.com/wenet-e2e/wenet) | ASR 工具链 | Apache-2.0 | 流式 / 非流式 ASR 训练与部署 | ★★★☆☆ |
| [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx) | ONNX 语音部署 | Apache-2.0 | ASR、TTS、VAD、KWS 离线部署 | ★★★☆☆ |
| [Vosk](https://github.com/alphacep/vosk-api) | 离线 ASR | Apache-2.0 | 传统离线 ASR，轻量、低资源 | ★★☆☆☆ |
| [ESPnet](https://github.com/espnet/espnet) | 语音研究工具箱 | Apache-2.0 | ASR、TTS、语音翻译、语音增强等 | ★★☆☆☆ |
| Moonshine | 端侧 ASR | 需核对 | 小型端侧 ASR 候选 | ★★☆☆☆ |

---

## 3. 开源 TTS 模型

### 3.1 推荐结论

| 场景 | 推荐模型 |
|---|---|
| 高质量多语种配音 | Qwen3-TTS, CosyVoice, VoxCPM2 |
| 中文 / 英文声音克隆 | IndexTTS2, Qwen3-TTS, CosyVoice, Spark-TTS |
| 多语种声音克隆 | VoxCPM2, Chatterbox Multilingual, CosyVoice |
| 视频配音时长控制 | IndexTTS2, Qwen3-TTS |
| 轻量部署 | Kokoro, MeloTTS |
| 社区生态 / 微调 | GPT-SoVITS |
| 效果对标 | F5-TTS, Fish Speech, XTTS-v2, MegaTTS3 |

### 3.2 模型列表

| 模型 / 项目 | 类型 | 许可证 | 主要特点 | 优先级 |
|---|---|---:|---|---:|
| [Qwen3-TTS](https://github.com/QwenLM/Qwen3-TTS) | 多语种 TTS | Apache-2.0 | 流式 TTS、声音设计、声音克隆、低延迟、多语种 | ★★★★★ |
| [IndexTTS2](https://github.com/index-tts/index-tts) | Zero-shot TTS | bilibili Model Use License | 情感控制、时长控制、声音克隆，适合视频配音 | ★★★★★ |
| [CosyVoice](https://github.com/FunAudioLLM/CosyVoice) | 多语种 TTS | Apache-2.0 / 模型协议需核对 | 零样本声音克隆、多语种、流式合成 | ★★★★★ |
| [VoxCPM2](https://github.com/OpenBMB/VoxCPM) | 多语种 TTS | Apache-2.0 | 30 种语言、48kHz、声音设计、可控声音克隆 | ★★★★★ |
| [Chatterbox](https://github.com/resemble-ai/chatterbox) | TTS / Voice cloning | MIT | 多语种、情绪控制、零样本声音克隆 | ★★★★☆ |
| [Spark-TTS](https://github.com/SparkAudio/Spark-TTS) | LLM-based TTS | Apache-2.0 | 说话人属性控制、语速 / 音高控制、声音克隆 | ★★★★☆ |
| [Kokoro](https://huggingface.co/hexgrad/Kokoro-82M) | 轻量 TTS | Apache-2.0 | 小模型、速度快、适合固定音色配音 | ★★★★☆ |
| [MeloTTS](https://github.com/myshell-ai/MeloTTS) | 多语种 TTS | MIT | 轻量、多语种、商用友好 | ★★★☆☆ |
| [OpenVoice](https://github.com/myshell-ai/OpenVoice) | 声音克隆 / 音色迁移 | MIT | 跨语言声音克隆，可与其他 TTS 组合 | ★★★☆☆ |
| [GPT-SoVITS](https://github.com/RVC-Boss/GPT-SoVITS) | TTS / Few-shot voice cloning | 需核对 | 社区生态强，支持少样本微调和跨语言合成 | ★★★☆☆ |
| [F5-TTS](https://github.com/SWivid/F5-TTS) | Flow matching TTS | 代码 MIT，模型多为非商用 | 效果强，适合研究和对标 | ★★★☆☆ |
| [Fish Speech](https://github.com/fishaudio/fish-speech) | TTS / Voice cloning | Research License | 高质量声音克隆和多语种能力 | ★★★☆☆ |
| [XTTS-v2](https://huggingface.co/coqui/XTTS-v2) | Voice cloning TTS | Coqui Public Model License | 经典跨语言声音克隆模型 | ★★☆☆☆ |
| [Dia](https://github.com/nari-labs/dia) | 对话式 TTS | Apache-2.0 | 对话语音、多人说话、情绪表达 | ★★☆☆☆ |
| [VibeVoice](https://github.com/microsoft/VibeVoice) | 长文本 / 多说话人 TTS | MIT | 长音频、播客、多角色语音 | ★★☆☆☆ |
| [Orpheus-TTS](https://github.com/canopyai/Orpheus-TTS) | LLM-based TTS | 需核对 | 自然度和情绪表达较强 | ★★☆☆☆ |
| [MegaTTS3](https://github.com/bytedance/MegaTTS3) | Voice cloning TTS | 需核对 | 高质量声音克隆，适合效果对标 | ★★☆☆☆ |
| X-Voice | 多语种 zero-shot voice cloning | 需核对 | 0.4B，多语种跨语言声音克隆研究候选 | ★★☆☆☆ |

## 4. 商业 ASR API

### 4.1 推荐结论

| 场景 | 推荐 API |
|---|---|
| 快速 MVP / LLM 链路集成 | OpenAI Transcribe |
| 实时字幕 / 低延迟 / diarization | Deepgram |
| 批量字幕 / 大厂稳定性 | Google Speech-to-Text |
| 英文 / 音频理解 / 会议播客 | AssemblyAI |
| AWS 生态 | Amazon Transcribe |
| Azure / 企业私有化 / 自定义模型 | Azure Speech to Text |
| 国内中文 / 电商 / 短视频 | 阿里云、腾讯云、火山引擎、百度智能云、讯飞开放平台 |

### 4.2 API 列表

| 服务商 | ASR 能力 | 计费口径 / 公开价格参考 | 适合场景 | 链接 |
|---|---|---:|---|---|
| OpenAI | 文件转写、实时转写、实时翻译 | `gpt-4o-mini-transcribe` 约 $0.003/min；`gpt-4o-transcribe` 约 $0.006/min | MVP、多语种字幕、和 LLM 翻译链路集成 | [Pricing](https://platform.openai.com/docs/pricing) |
| Deepgram | Nova / Flux，实时、预录音、自动语言检测、关键词增强、说话人分离 | Nova-3 Multilingual 约 $0.0058/min 预录音，$0.0092/min 流式；add-on 单独计费 | 实时字幕、语音机器人、字幕产品 | [Pricing](https://deepgram.com/pricing) |
| Google Speech-to-Text | V1/V2、Chirp、实时/批量、Dynamic Batch | V2 标准约 $0.016/min；Dynamic Batch 约 $0.003/min | 大规模批处理、GCP 生态 | [Pricing](https://cloud.google.com/speech-to-text/pricing) |
| Azure Speech to Text | 实时、Fast transcription、Batch transcription、自定义语音模型 | 按小时 / 秒计费，地区和功能差异较大 | 企业客户、微软生态、自定义模型 | [Pricing](https://azure.microsoft.com/en-us/pricing/details/speech/) |
| Amazon Transcribe | Streaming、Batch、Call Analytics、内容脱敏、语言识别、说话人分离 | Streaming 示例约 $0.01/min；Batch 视地区/阶梯变化 | AWS 生态、客服/会议转写 | [Pricing](https://aws.amazon.com/transcribe/pricing/) |
| AssemblyAI | Universal-2 / Universal-3 Pro、实时流式、音频理解、说话人分离 | Universal-3 Pro 公开页约 $0.15/hr 起，add-on 另计 | 播客、会议、英文音频理解 | [Pricing](https://www.assemblyai.com/pricing) |
| Speechmatics | 多语种 ASR，实时 / 批量 | 价格随套餐变化 | 欧洲市场、多语种转写 | [Pricing](https://www.speechmatics.com/pricing) |
| Rev.ai | 实时 / 预录音 ASR，人类转写 fallback | 价格随模型和服务变化 | 英文转写、人类校对兜底 | [Pricing](https://www.rev.ai/pricing) |
| Soniox | 多语种，实时 / 异步，转写 + 翻译 | 价格随套餐变化 | 低成本多语种字幕 | [Pricing](https://soniox.com/pricing) |
| Gladia | 多语种 STT，异步 / 实时 | 价格随套餐变化 | 欧洲合规、多语种 | [Pricing](https://www.gladia.io/pricing) |
| 阿里云智能语音交互 | 实时识别、录音文件识别、一句话识别、Paraformer | 实时 ASR、录音文件识别、Paraformer 分别计费 | 国内中文、电商、短视频 | [计费说明](https://help.aliyun.com/zh/isi/product-overview/billing-10) |
| 腾讯云 ASR | 录音文件识别、实时识别、大模型实时识别、说话人分离、实时翻译 | 预付费 / 后付费，按小时或调用时长计费 | 国内中文、腾讯生态、音视频平台 | [计费概述](https://cloud.tencent.com/document/product/1093/35686) |
| 火山引擎 / 豆包语音 | 大模型流式 ASR、录音文件识别、语音同传 | 按小时 / 资源包计费 | 短视频、内容平台、中文场景 | [计费说明](https://www.volcengine.com/docs/6561/1359370) |
| 百度智能云语音 | 短语音、实时识别、音频文件转写、EasyDL 语音识别 | 按调用时长 / 小时包 / 后付费 | 百度生态、中文语音应用 | [接口能力](https://ai.baidu.com/ai-doc/SPEECH/Tl9mh38eu) |
| 讯飞开放平台 | 语音听写、语音转写、实时识别、会议转写 | 套餐 / 调用时长计费 | 中文 ASR、政企、教育、会议 | [语音转写](https://www.xfyun.cn/service/lfasr) |

---

## 5. 商业 TTS API

### 5.1 推荐结论

| 场景 | 推荐 API |
|---|---|
| 高质量视频配音 / 声音克隆 | ElevenLabs, Azure Custom Voice, Google Instant Custom Voice, Resemble AI, Fish Audio |
| 快速 MVP / 固定音色 | OpenAI TTS, Google TTS, Amazon Polly, Deepgram Aura |
| 实时语音助手 / 低延迟 | Deepgram Aura, Cartesia, OpenAI TTS |
| 企业级稳定 / 多语言 | Google Cloud TTS, Azure Speech TTS, Amazon Polly |
| 国内中文配音 | 阿里 CosyVoice, 腾讯 TTS, 火山豆包语音, 百度 TTS, 讯飞 TTS |

### 5.2 API 列表

| 服务商 | TTS 能力 | 计费口径 / 公开价格参考 | 适合场景 | 链接 |
|---|---|---:|---|---|
| ElevenLabs | 高质量 TTS、声音克隆、视频配音、流式 API、STT | Multilingual v2/v3 约 $0.10/1k chars；Flash/Turbo 约 $0.05/1k chars | 高质量视频配音、声音克隆、多语种内容 | [API Pricing](https://elevenlabs.io/pricing/api) |
| OpenAI TTS | GPT-4o mini TTS，内置声音，支持流式输出和语气控制 | 按 token 计费，参考 OpenAI Pricing | 快速集成、固定音色、多语种配音 | [TTS Guide](https://platform.openai.com/docs/guides/text-to-speech) |
| Google Cloud TTS | Standard、WaveNet、Neural2、Chirp 3 HD、Instant Custom Voice、Gemini TTS | Standard / WaveNet 约 $4/M chars；Neural2 约 $16/M chars；Chirp 3 HD 约 $30/M chars；Instant Custom Voice 约 $60/M chars | 企业级 TTS、多语言、自定义音色 | [Pricing](https://cloud.google.com/text-to-speech/pricing) |
| Azure Speech TTS | Neural、Neural HD、Custom Voice、Personal Voice、Avatar、Video Translation | 按字符、训练、托管、视频输出等分别计费 | 企业 TTS、品牌音色、虚拟人 | [Pricing](https://azure.microsoft.com/en-us/pricing/details/speech/) |
| Amazon Polly | Standard、Neural、Long-Form、Generative voices、Speech Marks | Standard / Neural / Long-Form / Generative 分别计费 | AWS 生态、稳定 TTS、字幕时间标记 | [Pricing](https://aws.amazon.com/polly/pricing/) |
| Deepgram Aura | 低延迟 TTS，适合 voice agent | Aura-1 约 $0.015/1k chars；Aura-2 约 $0.030/1k chars | 实时对话、低延迟语音机器人 | [Pricing](https://deepgram.com/pricing) |
| Cartesia Sonic | Streaming TTS，低延迟，40+ 语言 | 套餐 / 销售报价 | 实时语音助手、低延迟产品 | [Pricing](https://cartesia.ai/pricing) |
| Resemble AI | TTS、声音克隆、声音设计、水印、on-prem | 按 voice / seat / usage 计费 | 企业安全、品牌音色、声音克隆 | [Pricing](https://www.resemble.ai/pricing) |
| PlayHT | TTS API、声音克隆、语音对话 | 套餐 / API 用量 | 内容创作者、配音、语音应用 | [API](https://github.com/playht/text-to-speech-api) |
| Fish Audio | TTS、ASR、Voice Design、Voice Cloning、Streaming | 按模型、字符/字节、音频时长计费 | 高质量声音克隆、TTS 产品化 | [Pricing](https://docs.fish.audio/developer-guide/models-pricing/pricing-and-rate-limits) |
| 阿里云 / 百炼语音 | 普通 TTS、长文本、流式 TTS、CosyVoice 大模型 | 通用语音 / 长文本 / CosyVoice 分别按字符计费 | 国内中文、电商口播、内容配音 | [计费说明](https://help.aliyun.com/zh/isi/product-overview/billing-10) |
| 腾讯云 TTS | 精品音色、大模型音色、超自然大模型音色、长文本 TTS、实时 TTS | 按字符 / 音色类型 / 资源包计费 | 国内中文、腾讯生态、虚拟人 | [计费说明](https://cloud.tencent.com/document/product/1073) |
| 火山引擎 / 豆包语音合成 | 大模型语音合成、流式合成、音色定制 | 按字符 / 资源包计费 | 短视频、电商、内容平台 | [豆包语音](https://www.volcengine.com/product/tts) |
| 百度智能云 TTS | 在线 TTS、长文本、声音复刻 | 按调用量 / 字符 / 套餐计费 | 百度生态、中文语音应用 | [接口能力](https://ai.baidu.com/ai-doc/SPEECH/Tl9mh38eu) |
| 讯飞开放平台 TTS | 在线 TTS、发音人、虚拟人相关能力 | 套餐 / 调用量计费 | 中文 TTS、政企、教育 | [开放平台](https://www.xfyun.cn/services/online_tts) |

## 6. 开源模型与商业 API 对比

| 维度 | 开源模型 | 商业 API |
|---|---|---|
| 初期开发速度 | 慢，需要部署、调参、工程封装 | 快，直接调用 API |
| 成本结构 | 主要是 GPU / 服务器 / 运维成本 | 按分钟、字符、token 或请求计费 |
| 数据安全 | 可私有化部署，数据不出域 | 需上传到云服务，依赖服务商数据政策 |
| 稳定性 | 依赖自建工程能力 | 服务商 SLA 更强 |
| 可控性 | 高，可微调、可替换、可定制 | 受 API 能力和条款限制 |
| 许可证风险 | 需要逐个核查模型权重和代码许可证 | 需要核查服务条款和声音克隆授权要求 |
| 扩展能力 | 可深度定制 | 快速扩展，但成本可能上升 |
| 推荐阶段 | 技术积累、成本优化、私有化 | MVP、快速上线、产品验证 |

---

## 7. 许可证 / 商用风险分级

| 风险等级 | 说明 | 示例 |
|---|---|---|
| 低风险 | Apache-2.0 / MIT，通常更适合商业化 | Qwen3-ASR, Qwen3-TTS, faster-whisper, Kokoro, MeloTTS, OpenVoice, VoxCPM2 |
| 中风险 | 代码开源，但模型权重协议或数据声明需要单独确认 | FunASR / SenseVoice, CosyVoice, GPT-SoVITS |
| 高风险 | 非商用、研究许可证、特殊商用限制 | F5-TTS pretrained weights, Fish Speech, XTTS-v2, 部分 MegaTTS3 组件 |
| 需法务确认 | 自定义模型许可证或大规模商用限制 | IndexTTS2 |
| API 合规风险 | 服务商条款、数据处理政策、声音克隆授权要求 | ElevenLabs, Azure Custom Voice, Google Instant Custom Voice, Resemble AI, Fish Audio |

---

## 8. Disclaimer

本仓库仅用于技术调研和实验评估。  
模型能力、许可证、API 价格和商用条款可能随时间变化。  
在商业产品中使用任何模型或 API 前，请务必复核官方 LICENSE、模型卡、价格页、服务条款、数据处理政策和声音克隆授权要求。
