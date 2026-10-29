# 项目英文内容：简体中文逐段释义版总目录

## 核心说明

本次以 [源提交 `7371c753ff4a087ca411e12033a3314231bd28c8`](https://github.com/Nuos/video-to-h3-prompt/tree/7371c753ff4a087ca411e12033a3314231bd28c8) 为基准，为仓库全部 **20 个源文件**各新增一份中文对应文档，放在源文件同目录。原始文件的内容与路径保持不变。

译本按源文的语义段落、列表项、表格行或脚本处理步骤组织，先列出**词汇与术语**，说明国际音标、词性、缩略语及其上下文含义，再给出**简体中文译文**。已经是中文的部分保留完整意义，夹杂的英文同样解释；源文中的英文提示词样例均给出中文全文。

音标使用常见英式或美式读法，并保留每个词条的具体标注；不把文件路径、字段键、库名或非标准缩合词虚构成具有统一读音的普通英语单词。对这类标识，解释组成词或通行的对应术语，保持准确拼写。

## 范围与数量

| 源文件类型 | 数量 | 处理方式 |
|---|---:|---|
| Markdown 文档 | 13 | 新建同目录 `原名.zh-CN.md`，完整逐段释义与翻译。 |
| 许可证 | 1 | 新建 `LICENSE.zh-CN.md`，逐段翻译授权、条件和责任条款。 |
| 配置／规则文件 | 2 | 新建 `原文件全名.zh-CN.md`，逐项解释键、值、规则与英文注释。 |
| Python、PowerShell、Shell 脚本 | 4 | 新建 `原脚本全名.zh-CN.md`，翻译英文说明、注释、帮助及消息，并说明完整处理流程。 |
| TXT、HTML 文件 | 0 | 此源版本未包含这两类文件。 |
| **合计** | **20** | **20 份一一对应的新译本**。 |

本总目录和 [`translations-manifest.json`](translations-manifest.json) 是新增的导航与核对材料，不计入这 20 份对应译本。

## 一、项目说明、技能入口与配置

| 源文件 | 中文对应版本 | 主要内容 |
|---|---|---|
| [README.md](README.md) | [README.zh-CN.md](README.zh-CN.md) | 功能、六条检查、逆问题、目录、依赖、启动命令和触发语。 |
| [SKILL.md](SKILL.md) | [SKILL.zh-CN.md](SKILL.zh-CN.md) | 元数据、输入输出、证据通道、硬性原则、十步流程及全部资源说明。 |
| [LICENSE](LICENSE) | [LICENSE.zh-CN.md](LICENSE.zh-CN.md) | MIT 许可证全部条款。 |
| [.gitignore](.gitignore) | [.gitignore.zh-CN.md](.gitignore.zh-CN.md) | 操作系统、编辑器、缓存、中间产物和生成结果的忽略规则。 |
| [agents/openai.yaml](agents/openai.yaml) | [agents/openai.yaml.zh-CN.md](agents/openai.yaml.zh-CN.md) | 显示名称、简短说明和完整默认提示词。 |

## 二、参考文档

| 源文件 | 中文对应版本 |
|---|---|
| [references/01-forensics-commands.md](references/01-forensics-commands.md) | [01-forensics-commands.zh-CN.md](references/01-forensics-commands.zh-CN.md) |
| [references/02-h3-field-mapping.md](references/02-h3-field-mapping.md) | [02-h3-field-mapping.zh-CN.md](references/02-h3-field-mapping.zh-CN.md) |
| [references/03-edit-effects.md](references/03-edit-effects.md) | [03-edit-effects.zh-CN.md](references/03-edit-effects.zh-CN.md) |
| [references/04-coser-replacement.md](references/04-coser-replacement.md) | [04-coser-replacement.zh-CN.md](references/04-coser-replacement.zh-CN.md) |
| [references/05-pitfalls-checklist.md](references/05-pitfalls-checklist.md) | [05-pitfalls-checklist.zh-CN.md](references/05-pitfalls-checklist.zh-CN.md) |
| [references/06-film-type-and-state-machine.md](references/06-film-type-and-state-machine.md) | [06-film-type-and-state-machine.zh-CN.md](references/06-film-type-and-state-machine.zh-CN.md) |
| [references/07-onset-and-card-points.md](references/07-onset-and-card-points.md) | [07-onset-and-card-points.zh-CN.md](references/07-onset-and-card-points.zh-CN.md) |
| [references/08-multi-image-and-segmentation.md](references/08-multi-image-and-segmentation.md) | [08-multi-image-and-segmentation.zh-CN.md](references/08-multi-image-and-segmentation.zh-CN.md) |
| [references/audio-heuristics.md](references/audio-heuristics.md) | [audio-heuristics.zh-CN.md](references/audio-heuristics.zh-CN.md) |
| [references/ffmpeg-cheatsheet.md](references/ffmpeg-cheatsheet.md) | [ffmpeg-cheatsheet.zh-CN.md](references/ffmpeg-cheatsheet.zh-CN.md) |
| [references/shot-syntax.md](references/shot-syntax.md) | [shot-syntax.zh-CN.md](references/shot-syntax.zh-CN.md) |

## 三、脚本译释与完整流程

| 源脚本 | 中文对应版本 | 覆盖内容 |
|---|---|---|
| [scripts/audio_probe.py](scripts/audio_probe.py) | [audio_probe.py.zh-CN.md](scripts/audio_probe.py.zh-CN.md) | 输入、依赖、均方根包络、频带计算、BPM 判断、全部英文消息及调用链。 |
| [scripts/onset_probe.py](scripts/onset_probe.py) | [onset_probe.py.zh-CN.md](scripts/onset_probe.py.zh-CN.md) | 说明字符串、参数默认值、短时傅里叶变换、频谱通量、音头分级、自相关、统计与 CSV 输出。 |
| [scripts/forensic_probe.ps1](scripts/forensic_probe.ps1) | [forensic_probe.ps1.zh-CN.md](scripts/forensic_probe.ps1.zh-CN.md) | 帮助、参数、依赖检查、七步取证、日志、无音轨分支及输出清单。 |
| [scripts/forensic_probe.sh](scripts/forensic_probe.sh) | [forensic_probe.sh.zh-CN.md](scripts/forensic_probe.sh.zh-CN.md) | 参数、严格模式、七步流程、Python 选择、英文提示、输出和实际运行边界。 |

## 阅读约定

1. **术语先行。** `n.` 表示名词，`v.` 表示动词，`adj.` 表示形容词，`adv.` 表示副词，`phr.` 表示短语；译本也直接使用这些词性的中文名称。`IPA` 是 International Phonetic Alphabet，即国际音标。
2. **命令和标识按原样保留。** 可执行命令、参数、字段键、模式标识、参考标签和路径供核对使用。英文注释或消息在相邻释义中翻译，不通过修改原命令来实现中文化。
3. **自然语言样例完整翻译。** 提示词模板中的英文叙述给出完整中文对应；其中保留的 `<Subject 1>`、`[Shot 1]`、`non_diegetic_music` 等是格式标识，并在对应段落解释。
4. **原文与译注分开。** 时间戳小数位、音乐要素项数、交叉引用、经验判断与实际代码行为等存在疑点时，保留源文表述，并以“译注”说明，不替作者改写原规则。
5. **源行号用于追溯。** 每份译本标明对应源版本及行号范围。脚本按函数、注释、消息或相邻步骤组合说明，覆盖输入→处理→输出及错误分支。
6. **译本用于阅读。** `SKILL.zh-CN.md` 不是新的技能入口，`openai.yaml.zh-CN.md` 不是替代配置，脚本的 `.zh-CN.md` 不是可执行副本；原文件继续承担原来的运行作用。

## 核对清单

机器可读清单记录每个源文件的 Git 内容哈希、译本路径、译本 SHA-256、源行号映射和释义单元数量。核对内容包括：20 个原文件均与基准提交逐字节一致、20 份译本一一对应、词汇释义与中文译文顺序成对、代码围栏完整、文档中的 31 个可执行命令块原样保留，以及相对链接有效。行号覆盖用于检查导航与遗漏，不单独充当语义翻译正确性的证明；正文另经逐文件对照审校。

日期：2026-10-29。
