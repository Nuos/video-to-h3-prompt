# forensic_probe.ps1：逐段中文释义与完整流程说明

源文件：`scripts/forensic_probe.ps1`。源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。本文件是阅读用译本；原 PowerShell 脚本未改动，命令和参数保持源代码拼写。行号对应上述版本。

## 1. 帮助标题与产出概述（源文件第 1–7 行）

**词汇与术语**

- synopsis /sɪˈnɒpsɪs/，名词：概要；description /dɪˈskrɪpʃən/，名词：详细说明；`.SYNOPSIS`、`.DESCRIPTION` 为 PowerShell 注释式帮助标记。
- reverse-engineering /rɪˌvɜːs ˌendʒɪˈnɪərɪŋ/，名词：逆向工程；one-click /wʌn klɪk/，定语短语：一键的；forensics /fəˈrensɪks/，名词：取证分析。

**简体中文译文**

概要：H3 视频逆向工程的一键取证脚本，面向 Windows PowerShell。第 1 行开始多行帮助注释。

**词汇与术语**

- summary /ˈsʌməri/，名词：摘要；sparse /spɑːs/，形容词：稀疏的；frame /freɪm/，名词：帧；fps /ˌef piː ˈes/，Frames Per Second 的缩写：每秒帧数。
- contact sheet /ˈkɒntækt ʃiːt/，名词短语：按序拼接多帧的缩略图总览；mono /ˈmɒnəʊ/，形容词：单声道的；spectrogram /ˈspektrəɡræm/，名词：时频谱图。
- RMS /ˌɑːr em ˈes/，名词性缩略语，Root Mean Square /ruːt miːn skweə/：均方根；envelope /ˈenvələʊp/，名词：包络。
- BPM /ˌbiː piː ˈem/，名词性缩略语，Beats Per Minute /biːts pə ˈmɪnɪt/：每分钟拍数；credibility /ˌkredəˈbɪləti/：可信度。
- onset /ˈɒnset/，名词：音头；card point 为项目表示“卡点”的用语，point /pɔɪnt/，名词：点；detection /dɪˈtekʃən/，名词：检测。

**简体中文译文**

详细说明：输出 `ffprobe` 信息摘要、每秒 2 帧的稀疏帧、4×4 帧总览图、单声道 WAV 音频、频谱图、由 `audio_probe.py` 产生的均方根包络与 BPM 可信度分析，以及由 `onset_probe.py` 产生的音头／卡点检测结果；后者只依赖 `numpy` 和 `scipy`。

## 2. 运行后的人工复核与参数命名（源文件第 8–10 行）

**词汇与术语**

- dense /dens/，形容词：密集的；extraction /ɪkˈstrækʃən/，名词：提取；ambiguous /æmˈbɪɡjuəs/，形容词：有歧义的；window /ˈwɪndəʊ/，名词：时间窗口。
- reconcile /ˈrekənsaɪl/，动词：核对、对应；strong /strɒŋ/，形容词：强的；cut /kʌt/，名词：切镜。

**简体中文译文**

完成后，对有歧义的时间窗口按每秒 4–8 帧密集抽帧，并核对强音头是否与切镜相对应；参见 `references/06` 和 `references/07` 所指的两份参考文档。

**词汇与术语**

- parameter /pəˈræmɪtə/，名词：参数；automatic variable /ˌɔːtəˈmætɪk ˈveəriəbəl/，名词短语：自动变量；input /ˈɪnpʊt/，名词：输入。

**简体中文译文**

注意：参数名称是 `-Video`，不是 `-Input`，因为 `$Input` 是 PowerShell 的自动变量。这里翻译原注释的命名理由，不改参数名。

## 3. 调用示例与参数默认值（源文件第 11–19 行）

**词汇与术语**

- example /ɪɡˈzɑːmpəl/，名词：示例；mandatory /ˈmændətəri/，形容词：必填的；string /strɪŋ/，名词：字符串；integer /ˈɪntɪdʒə/，名词：整数。
- profile /ˈprəʊfaɪl/，名词：配置文件；execution policy /ˌeksɪˈkjuːʃən ˈpɒləsi/，名词短语：执行策略；bypass /ˈbaɪpɑːs/，动词或名词：绕过，在命令中为策略值。
- output directory /ˈaʊtpʊt dəˈrektəri/，名词短语：输出目录，代码中为 `OutDir`。

**简体中文译文**

示例调用如下，其中 `-NoProfile` 表示不加载 PowerShell 配置，`-ExecutionPolicy Bypass` 是源示例为此次进程设置的执行策略，`-File` 指定脚本，`-Video` 指定源视频，`-OutDir` 指定输出目录。

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File forensic_probe.ps1 -Video ".\clip.mp4" -OutDir forensic_out
```

**词汇与术语**

- video /ˈvɪdiəʊ/，名词：视频；default /dɪˈfɔːlt/，名词：默认值；fps：每秒帧数，见第 1 节。

**简体中文译文**

第 13 行结束帮助注释。参数区定义：`Video` 是必填字符串；`OutDir` 是字符串，默认 `forensic_out`；`Fps` 是整数，默认 `2`。因此帮助中所说的每秒 2 帧是默认值，可以通过 `-Fps` 改变。第 19 行为空行。

## 4. 工具、文件与目录检查（源文件第 20–29 行）

**词汇与术语**

- error /ˈerə/，名词：错误；action /ˈækʃən/，名词：动作；preference /ˈprefərəns/，名词：偏好、配置值；stop /stɒp/，动词：停止。
- assert /əˈsɜːt/，动词：断言、检查前提；command /kəˈmɑːnd/，名词：命令，函数名中缩写为 `Cmd`。
- found /faʊnd/，过去分词：找到的；PATH /pɑːθ/，环境变量名：命令搜索路径；literal /ˈlɪtərəl/，形容词：按字面解释的。

**简体中文译文**

设置 PowerShell 的错误处理偏好为 `Stop`。`Assert-Cmd` 使用 `Get-Command` 检查命令是否存在，找不到时抛出“错误：在 PATH 中找不到〔命令名〕”。它检查 `ffmpeg` 和 `ffprobe`。随后用 `Test-Path -LiteralPath` 检查视频路径，找不到时抛出“错误：找不到视频：〔视频路径〕”。最后创建输出目录中的 `frames` 子目录，并抑制建目录命令的常规输出。第 26、29 行为空行。

## 5. 第 1／7 步：媒体元数据（源文件第 30–34 行）

**词汇与术语**

- probe /prəʊb/，动词：探测；format /ˈfɔːmæt/，名词：容器格式；duration /djʊˈreɪʃən/，名词：时长；bit rate /bɪt reɪt/，名词短语：比特率。
- stream /striːm/，名词：媒体流；index /ˈɪndeks/，名词：索引；codec /ˈkəʊdek/，名词：编解码器；type /taɪp/：类型；name /neɪm/：名称。
- width /wɪdθ/：宽度；height /haɪt/：高度；frame rate /freɪm reɪt/：帧率；sample rate /ˈsɑːmpəl reɪt/：采样率；channel /ˈtʃænəl/：声道，均为名词或名词短语。
- tee /tiː/，命令名：将输入同时写往屏幕或管道与文件；wrapper /ˈræpə/，名词：包裹层、章节标记。

**简体中文译文**

打印“第 1／7 步：`ffprobe`”。请求容器时长、比特率，以及媒体流索引、类型、编解码器名称、宽度、高度、`r_frame_rate` 所报告的帧率、采样率和声道数。`-v error` 只显示错误级日志，`noprint_wrappers=1` 隐去默认输出的章节包裹标记。结果经 `Tee-Object` 同时显示并保存到 `probe.txt`。第 34 行为空行。

## 6. 第 2／7 步：稀疏抽帧（源文件第 35–39 行）

**词汇与术语**

- sparse frames /spɑːs freɪmz/，名词短语：稀疏帧；scale /skeɪl/，动词：缩放；width /wɪdθ/，名词：宽度；count /kaʊnt/，名词：数量。

**简体中文译文**

打印“第 2／7 步：按〔Fps 值〕帧／秒稀疏抽帧，宽度 480”。`ffmpeg` 使用 `fps=$Fps,scale=480:-1`，将图像宽度缩放至 480，自动计算等比例高度，保存为 `frames/f_%02d.jpg`。`-y` 允许覆盖同名输出。之后统计该目录中所有 `.jpg` 文件并打印“帧数：〔数量〕”。第 39 行为空行。

## 7. 第 3／7 步：4×4 总览图（源文件第 40–43 行）

**词汇与术语**

- contact sheet /ˈkɒntækt ʃiːt/，名词短语：多帧总览图；padding /ˈpædɪŋ/，名词：间距、填充；yellow /ˈjeləʊ/，形容词：黄色的。
- tile /taɪl/，动词或名词：平铺、拼图单元；framerate /ˈfreɪmreɪt/，名词：帧率。

**简体中文译文**

打印“第 3／7 步：4×4 总览图，使用黄色间距”。以每秒 1 张的输入图像序列读取 `frames/f_%02d.jpg`，把每帧缩到宽 240、高度按比例取偶数，再以 4×4 排列，单元之间留 4 像素黄色间距，输出为 `grid_%03d.jpg`。这里的 `-framerate 1` 用于读取已抽出的图片序列，不重新决定源视频抽帧频率。第 43 行为空行。

## 8. 第 4／7 步：判定音轨并提取单声道（源文件第 44–48 行）

**词汇与术语**

- audio extraction /ˈɔːdiəʊ ɪkˈstrækʃən/，名词短语：音频提取；mono /ˈmɒnəʊ/，形容词：单声道的；select /sɪˈlekt/，动词：选择；match /mætʃ/，动词：匹配。
- stream /striːm/，名词：媒体流；CSV /ˌsiː es ˈviː/，名词性缩略语，Comma-Separated Values：逗号分隔值格式。

**简体中文译文**

打印“第 4／7 步：提取 22050 Hz 单声道音频”。先让 `ffprobe` 只选择音频流，读取其 `codec_type`；输出包含 `audio` 时进入音频分析分支。`ffmpeg -vn -ac 1 -ar 22050` 表示不输出视频、输出一个声道并使用每秒 22050 次采样，将音频保存为 `audio.wav`。第 48 行为空行。

## 9. 第 5／7 步：频谱图（源文件第 49–52 行）

**词汇与术语**

- spectrogram /ˈspektrəɡræm/，名词：时频谱图；spectrum /ˈspektrəm/，名词：频谱；legend /ˈledʒənd/，名词：图例、标注。

**简体中文译文**

打印“第 5／7 步：频谱图”。读取 `audio.wav`，用 `showspectrumpic` 滤镜生成 1000×400 的频谱图，启用图例标注，保存为 `spectrum.jpg`。第 52 行为空行。

## 10. 第 6／7 步：均方根与 BPM（源文件第 53–56 行）

**词汇与术语**

- envelope /ˈenvələʊp/，名词：包络；credibility /ˌkredəˈbɪləti/，名词：可信度；script root /skrɪpt ruːt/，名词短语：脚本所在根目录。
- RMS：均方根；BPM：每分钟拍数。`PSScriptRoot` 是 PowerShell 中表示当前脚本所在目录的自动变量；`stats` 为 statistics /stəˈtɪstɪks/（名词，统计）的简写。

**简体中文译文**

打印“第 6／7 步：均方根包络与 BPM 可信度”。以 `python` 调用本脚本同目录的 `audio_probe.py`，输入 `audio.wav`；其标准输出同时显示并保存到 `audio_stats.txt`。第 56 行为空行。

## 11. 第 7／7 步：音头和卡点（源文件第 57–59 行）

**词汇与术语**

- onset /ˈɒnset/，名词：音头；detection /dɪˈtekʃən/，名词：检测；card point：本项目的卡点用语；CSV：逗号分隔值格式。

**简体中文译文**

打印“第 7／7 步：音头／卡点检测”。以 `python` 调用本脚本同目录的 `onset_probe.py`，输入 `audio.wav`；通过 `--csv` 保存 `onsets.csv`，并将标准输出同时显示、保存为 `onsets.txt`。

## 12. 没有音轨的分支（源文件第 60–64 行）

**词汇与术语**

- stream /striːm/，名词：媒体流；skip /skɪp/，动词：跳过；audio /ˈɔːdiəʊ/，名词：音频；onset /ˈɒnset/：音头。

**简体中文译文**

如果没有检测到音频流，则打印“没有音频流——跳过频谱图、均方根和音头分析”。第 62 行结束条件分支，第 63 行为空行，第 64 行输出空白行。

## 13. 完成消息与后续操作（源文件第 65–67 行）

**词汇与术语**

- done /dʌn/，过去分词：已完成；inspect /ɪnˈspekt/，动词：检查、查看；skeleton /ˈskelɪtən/，名词：骨架。
- dense-extract /dens ɪkˈstrækt/，动词短语：密集抽取；ambiguous window /æmˈbɪɡjuəs ˈwɪndəʊ/：有歧义的时间窗口。
- start /stɑːt/，名词：起始时刻；duration /djʊˈreɪʃən/，名词：时长，占位符中缩写为 `dur`。

**简体中文译文**

打印：“完成。查看〔输出目录〕下的 `grid_*.jpg` 建立骨架，然后：1）对有歧义的时间窗口密集抽帧。”随后显示如下结构的命令；原代码会将视频和输出目录变量代入显示，并不会自动执行它。

```powershell
ffmpeg -ss <start> -t <dur> -i "$Video" -vf 'fps=4,scale=360:-1' $OutDir\seg\seg_%02d.jpg
```

**词汇与术语**

- reconcile /ˈrekənsaɪl/，动词：核对；cut /kʌt/，名词：切镜；hit /hɪt/，名词：击打；triage /ˈtriːɑːʒ/，动词：分类分流；film type /fɪlm taɪp/，名词短语：片型。

**简体中文译文**

“2）将 `onsets.txt` 中的强音头与切镜／击打核对，并判断片型，参见 `references/06`。”

## 14. 输出清单与运行边界（译者流程归纳）

**词汇与术语**

- output /ˈaʊtpʊt/，名词：输出；metadata /ˈmetədeɪtə/，名词：元数据；conditional /kənˈdɪʃənəl/，形容词：有条件产生的。

**简体中文译文**

完整流程是检查工具和视频→建目录→读取媒体信息→抽稀疏帧→拼总览图→检查音轨→有音轨时提取音频、生成频谱图并运行两项 Python 分析→显示人工密帧复核建议。输出对应如下：

| 位置（相对于 `OutDir`） | 内容 | 产生条件 |
|---|---|---|
| `probe.txt` | 媒体信息 | 元数据步骤完成 |
| `frames/f_%02d.jpg` | 稀疏源帧 | 抽帧步骤完成 |
| `grid_%03d.jpg` | 4×4 总览图 | 拼图步骤完成 |
| `audio.wav` | 22050 Hz 单声道音频 | 有音轨且提取成功 |
| `spectrum.jpg` | 频谱图 | 有音轨且频谱步骤成功 |
| `audio_stats.txt` | 均方根、频带统计和可选 BPM 结果 | Python 分析成功 |
| `onsets.txt` | 音头和逐秒轮廓文字结果 | 音头分析成功 |
| `onsets.csv` | 全部已分级音头 | 音头分析成功并写入 |

**词汇与术语**

- dependency /dɪˈpendənsi/，名词：依赖；native command /ˈneɪtɪv kəˈmɑːnd/，名词短语：外部可执行命令；exit code /ˈeɡzɪt kəʊd/：退出码；stale /steɪl/，形容词：上次遗留的。

**简体中文译文（译注）**

脚本启动时只明确检查 `ffmpeg` 和 `ffprobe`，没有预检 `python`、`numpy`、`scipy`；音频步骤需要这些依赖。它不清空上次输出，旧图片可能影响帧计数或拼图。末尾建议的 `seg` 目录并未自动创建，需要执行补抽命令的人先准备目录。Windows PowerShell 对外部程序非零退出码的处理与 PowerShell 自身错误不完全相同；源脚本没有逐条检查外部命令退出码，因此完成提示本身不能替代检查输出是否完整。
