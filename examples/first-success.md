# 第一次成功｜macOS 本地语音转文字项目路引

检查日期：2026-07-28

## 用户输入

```text
使用 $wanjie-luopan 帮我寻找适合 macOS 本地运行、用于研究语音转文字的开源项目。
只做快速发现，不安装运行。
```

## 本次假设

- “研究”同时接受底层推理引擎、Apple 平台 SDK 和可直接体验的桌面应用
- 必须能够在本地完成核心推理，不把云端 API 当作唯一入口
- 本次停在 E1 仓库表面证据，不克隆、不下载模型、不运行
- Star 只作为热度背景，不进入质量结论

## 直接结论

四个候选代表四种不同入口。想研究 Apple Silicon 原生集成，先看 `argmax-oss-swift` 和 `FluidAudio`；想直接体验离线桌面应用，先看 `Buzz`；想研究最通用的本地 C/C++ 推理底座，先看 `whisper.cpp`。

## 立即值得看

| 项目 | 真实形态 | 为什么值得看 | E1 证据 | 主要风险 |
| --- | --- | --- | --- | --- |
| [argmaxinc/argmax-oss-swift](https://github.com/argmaxinc/argmax-oss-swift) | Apple Silicon 本地语音 AI Swift SDK | 原 `WhisperKit` 入口已迁移到统一 Swift 仓库，适合研究 Apple 平台原生集成 | 仓库描述为 On-device Speech AI for Apple Silicon；MIT；公开 Release `v1.0.0` | 不是完整听写应用；系统、模型与准确率要求尚未运行验证 |
| [FluidInference/FluidAudio](https://github.com/FluidInference/FluidAudio) | Core ML 音频模型与 Swift SDK | 同时覆盖 STT、VAD、说话人分离等本地音频能力，适合研究更完整的 Apple 音频管线 | Swift 为主；Apache-2.0；公开 Release `v0.15.5` | 能力面较宽，集成成本和设备支持需要进一步查源码与示例 |
| [chidiwilliams/buzz](https://github.com/chidiwilliams/buzz) | 离线桌面转录应用 | 最接近“安装后直接体验”的产品入口，适合先判断完整工作流是否符合预期 | 仓库说明可在个人电脑离线转录与翻译；MIT；公开 Release `v1.4.4` | Python 桌面应用，不等于 macOS 原生 Swift；打包、性能和芯片兼容性未验证 |
| [ggml-org/whisper.cpp](https://github.com/ggml-org/whisper.cpp) | C/C++ 推理引擎与 CLI | 本地部署边界清楚、跨平台，适合研究推理、量化、Metal 和嵌入式集成 | C/C++ 为主；MIT；公开 Release `v1.9.1`；仓库包含 Metal 代码 | 更像底层能力而不是成品应用；需要自行构建上层交互 |

## 验证边界

已验证：

- 四个仓库均真实存在且未归档
- 当前仓库描述、主语言、许可证和最新公开 Release
- `WhisperKit` GitHub 入口当前指向 `argmaxinc/argmax-oss-swift`

未验证：

- 中文准确率、速度、功耗和 Apple 芯片代际差异
- 模型下载大小、首次运行体验和系统权限
- Buzz 当前 macOS 安装包的签名、公证和实际稳定性
- 四个候选的完整源码、Issue 与构建结果

本次未执行：

- 克隆、安装、编译、模型下载和本地运行

## 下一步

如果目标是二次开发 Apple 原生应用，对 `argmax-oss-swift` 与 `FluidAudio` 做星图比较；如果目标是先体验完整流程，开卷检查 `Buzz` 的 macOS 发行产物和近期 Issues。

这份样例展示的是一次真实 E1 路引，不是性能评测，也不把公开 Release 等同于本机已经可用。
