# forensic_probe.sh：逐段中文释义与完整流程说明

源文件：`scripts/forensic_probe.sh`。源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。本文件为阅读用中文说明，原 Bash 脚本保持原样。行号对应上述版本；参数、路径与程序标识符按原拼写保留。

## 1. 文件说明与调用方式（源文件第 1–5 行）

**词汇与术语**

- forensic /fəˈrensɪk/，形容词：取证的；probe /prəʊb/，名词或动词：探测、检查。
- output directory /ˈaʊtpʊt dəˈrektəri/，名词短语：输出目录，注释中为 `out_dir`；fps /ˌef piː ˈes/，名词性缩略语，Frames Per Second：每秒帧数。
- RMS /ˌɑːr em ˈes/，名词性缩略语，Root Mean Square /ruːt miːn skweə/：均方根；BPM /ˌbiː piː ˈem/，Beats Per Minute /biːts pə ˈmɪnɪt/：每分钟拍数。
- onset /ˈɒnset/，名词：音头；`macOS`、`Linux` 为操作系统名称，`bash` 为解释器名称。

**简体中文译文**

`forensic_probe.sh`——用于 macOS／Linux 的 H3 视频反推一键取证脚本。用法为 `bash forensic_probe.sh "IN.mp4" [out_dir] [fps]`，方括号表示可选参数。产出包括 `ffprobe` 信息、稀疏帧、4×4 网格、`audio.wav`、频谱图、由 `audio_probe.py` 生成的均方根／BPM 表，以及由 `onset_probe.py` 生成的音头／卡点表。第一行通过环境中的 `bash` 指定解释器。

## 2. 严格执行选项与参数（源文件第 6–11 行）

**词汇与术语**

- usage /ˈjuːsɪdʒ/，名词：用法；input /ˈɪnpʊt/，名词：输入，代码中为 `IN`；output /ˈaʊtpʊt/，名词：输出，代码中为 `OUT`。
- pipe /paɪp/，名词：管道；fail /feɪl/，动词：失败；`pipefail` 为 Bash 选项名称。
- here /hɪə/，副词：这里，变量 `HERE` 在本脚本中表示脚本所在目录；directory /dəˈrektəri/，名词：目录。

**简体中文译文**

`set -euo pipefail` 启用错误停止、未定义变量检查和管道失败传播。第一个参数为输入视频；缺少该参数时，`${1:?...}` 输出“用法：`bash forensic_probe.sh IN.mp4 [out_dir] [fps]`”并终止。第二个参数为输出目录，默认 `forensic_out`；第三个参数为抽帧率，默认 `2`。`HERE` 通过切换到脚本路径的目录后读取工作目录，得到同目录 Python 脚本的定位依据。第 7 行为空行。

## 3. 依赖检查与建目录（源文件第 12–15 行）

**词汇与术语**

- command /kəˈmɑːnd/，名词：命令；error /ˈerə/，名词：错误；found /faʊnd/，过去分词：找到的；exit /ˈeɡzɪt/，动词：退出。
- frame /freɪm/，名词：帧；`/dev/null` 为用于丢弃输出的设备路径；`mkdir` 为创建目录命令。

**简体中文译文**

分别检查能否找到 `ffmpeg` 和 `ffprobe`，常规检查输出丢弃。找不到前者时打印“错误：找不到 `ffmpeg`”，找不到后者时打印“错误：找不到 `ffprobe`”，均以状态码 `1` 退出。随后创建输出目录中的 `frames` 子目录；`-p` 允许补建父目录并兼容目录已存在的情况。第 14 行为空行。

## 4. 第 1／7 步：视频与音频元数据（源文件第 16–18 行）

**词汇与术语**

- format /ˈfɔːmæt/，名词：容器格式；duration /djʊˈreɪʃən/，名词：时长；bit rate /bɪt reɪt/，名词短语：比特率。
- stream /striːm/，名词：媒体流；index /ˈɪndeks/，名词：索引；codec /ˈkəʊdek/，名词：编解码器；type /taɪp/：类型；name /neɪm/：名称。
- width /wɪdθ/：宽度；height /haɪt/：高度；frame rate /freɪm reɪt/：帧率；sample rate /ˈsɑːmpəl reɪt/：采样率；channel /ˈtʃænəl/：声道，均为名词或名词短语。
- tee /tiː/，命令名：将输入同时写到标准输出和文件；wrapper /ˈræpə/，名词：包裹层、章节标记。

**简体中文译文**

打印“第 1／7 步：`ffprobe`”。请求容器时长、比特率，以及媒体流索引、编解码类型、编解码器名称、宽高、`r_frame_rate` 所报告的帧率、采样率和声道数。日志级别为错误，输出不显示章节包裹标记；结果通过 `tee` 同时显示并写入 `$OUT/probe.txt`。第 18 行为空行。

## 5. 第 2／7 步：稀疏帧（源文件第 19–22 行）

**词汇与术语**

- sparse /spɑːs/，形容词：稀疏的；frame /freɪm/，名词：帧；width /wɪdθ/，名词：宽度；scale /skeɪl/，动词：缩放。
- count /kaʊnt/，名词或动词：计数；`wc -l` 为按行计数的命令参数组合。

**简体中文译文**

打印“第 2／7 步：按〔FPS 值〕帧／秒抽取稀疏帧，宽度 480”。使用 `fps=${FPS},scale=480:-1`，将宽度缩放到 480，高度按比例计算，输出到 `$OUT/frames/f_%02d.jpg`。`-y` 表示覆盖同名输出。随后把帧目录的文件列表交给 `wc -l` 计数，打印“帧数：〔计数结果〕”。第 22 行为空行。

## 6. 第 3／7 步：总览网格（源文件第 23–26 行）

**词汇与术语**

- contact sheet /ˈkɒntækt ʃiːt/，名词短语：多帧缩略图总览；padding /ˈpædɪŋ/，名词：间距；yellow /ˈjeləʊ/，形容词：黄色的；tile /taɪl/，动词：平铺。
- framerate /ˈfreɪmreɪt/，名词：帧率；grid /ɡrɪd/，名词：网格。

**简体中文译文**

打印“第 3／7 步：4×4 总览图，黄色间距”。以每秒 1 张的图片序列读取已抽出的帧，缩放至宽 240、高度按比例取偶数；每 16 张拼成一张 4×4 网格，单元间留 4 像素黄色间距，输出到 `$OUT/grid_%03d.jpg`。第 24 行末尾的反斜线表示 Bash 命令续行；第 26 行为空行。

## 7. 第 4／7 步：音轨判定与提取（源文件第 27–29 行）

**词汇与术语**

- audio /ˈɔːdiəʊ/，名词：音频；mono /ˈmɒnəʊ/，形容词：单声道的；stream /striːm/，名词：媒体流；select /sɪˈlekt/，动词：选择。
- CSV /ˌsiː es ˈviː/，名词性缩略语，Comma-Separated Values：逗号分隔值格式；quiet /ˈkwaɪət/，形容词：静默的，对应 `grep -q` 的静默匹配用途。

**简体中文译文**

打印“第 4／7 步：22050 Hz 单声道音频”。先读取音频流的 `codec_type`，用 `grep -q audio` 检查是否存在音频。如果存在，则提取为 `$OUT/audio.wav`；`-vn` 排除视频，`-ac 1` 设为一个声道，`-ar 22050` 将采样率设为 22050 Hz。

## 8. 第 5／7 步：频谱图（源文件第 30–31 行）

**词汇与术语**

- spectrogram /ˈspektrəɡræm/，名词：时频谱图；spectrum /ˈspektrəm/，名词：频谱；legend /ˈledʒənd/，名词：图例、标注。

**简体中文译文**

打印“第 5／7 步：频谱图”。对刚提取的音频运行 `showspectrumpic` 滤镜，以 1000×400 的大小并启用图例标注输出 `$OUT/spectrum.jpg`。

## 9. 第 6／7 步：选择 Python 并分析均方根（源文件第 32–34 行）

**词汇与术语**

- credibility /ˌkredəˈbɪləti/，名词：可信度；RMS：均方根；BPM：每分钟拍数；statistics /stəˈtɪstɪks/，名词：统计，文件名中为 `stats`。
- interpreter /ɪnˈtɜːprɪtə/，名词：解释器；`PY` 是此脚本存放解释器命令名的变量。

**简体中文译文**

打印“第 6／7 步：均方根与 BPM 可信度”。先选择 `python3`；找不到 `python3` 命令时，改为 `python`。调用当前 Bash 脚本同目录的 `audio_probe.py`，输入 `$OUT/audio.wav`，并将输出同时显示、保存到 `$OUT/audio_stats.txt`。

## 10. 第 7／7 步：音头与卡点（源文件第 35–36 行）

**词汇与术语**

- onset /ˈɒnset/，名词：音头；detection /dɪˈtekʃən/，名词：检测；card point：项目中的卡点用语；CSV：逗号分隔值格式。

**简体中文译文**

打印“第 7／7 步：音头／卡点检测”。用同一个 Python 解释器调用 `onset_probe.py`，输入 `$OUT/audio.wav`，将全部音头写入 `$OUT/onsets.csv`，同时把标准输出显示并保存到 `$OUT/onsets.txt`。

## 11. 无音轨分支（源文件第 37–41 行）

**词汇与术语**

- skip /skɪp/，动词：跳过；audio stream /ˈɔːdiəʊ striːm/，名词短语：音频流；spectrogram /ˈspektrəɡræm/：时频谱图；onset /ˈɒnset/：音头。

**简体中文译文**

没有检测到音频流时打印：“没有音频流——跳过频谱图、均方根和音头分析。”随后结束条件分支。第 40 行为空行，第 41 行打印一个空白行。

## 12. 完成提示与补抽命令（源文件第 42–44 行）

**词汇与术语**

- done /dʌn/，过去分词：已完成；inspect /ɪnˈspekt/，动词：查看、检查；dense-extract /dens ɪkˈstrækt/，动词短语：密集抽取。
- ambiguous window /æmˈbɪɡjuəs ˈwɪndəʊ/，名词短语：有歧义的时间窗口；reconcile /ˈrekənsaɪl/，动词：核对、对应。
- strong /strɒŋ/，形容词：强的；cut /kʌt/，名词：切镜；hit /hɪt/，名词：击打；start /stɑːt/：起点；duration /djʊˈreɪʃən/：时长，命令中缩写为 `dur`。

**简体中文译文**

打印：“完成。查看 `$OUT/grid_*.jpg`，再密集抽取有歧义的时间窗口，将 `$OUT/onsets.txt` 中的强音头与切镜／击打核对，参见 `references/06` 和 `references/07`。”最后显示如下补抽命令结构；运行时 `$IN` 和 `$OUT` 会被代入。源脚本只打印这个建议，不会执行补抽。

```bash
ffmpeg -ss <start> -t <dur> -i "$IN" -vf 'fps=4,scale=360:-1' $OUT/seg/seg_%02d.jpg
```

## 13. 完整输入输出关系与适用边界（译者流程归纳）

**词汇与术语**

- input /ˈɪnpʊt/，名词：输入；output /ˈaʊtpʊt/，名词：输出；pipeline /ˈpaɪplaɪn/，名词：处理流程。

**简体中文译文**

完整顺序为：读取视频、输出目录和抽帧率参数→检查媒体工具→建帧目录→探测媒体信息→稀疏抽帧→拼接网格→检查音轨→有音轨时提取音频并完成三项音频分析→打印密帧复核建议。输出对应如下：

| 输出路径（相对于 `OUT`） | 中文含义 |
|---|---|
| `probe.txt` | 媒体元数据摘要 |
| `frames/f_%02d.jpg` | 默认每秒 2 帧的稀疏帧图片 |
| `grid_%03d.jpg` | 按序拼接的 4×4 帧总览图 |
| `audio.wav` | 22050 Hz 单声道音频，仅在有音轨时产生 |
| `spectrum.jpg` | 音频时频谱图 |
| `audio_stats.txt` | 均方根、频带统计和可选 BPM 分析 |
| `onsets.txt` | 音头候选卡点及逐秒强度轮廓 |
| `onsets.csv` | 全部已分级音头的时间、强度与等级 |

**词汇与术语**

- dependency /dɪˈpendənsi/，名词：依赖；directory /dəˈrektəri/，名词：目录；stale /steɪl/，形容词：遗留的；quote /kwəʊt/，名词或动词：引号、加引号。

**简体中文译文（译注）**

脚本没有预先检查输入视频是否存在，也没有验证帧率参数；由相关命令在运行时处理错误。有音轨时需安装 Python、`numpy` 和 `scipy`，`librosa` 仅用于可选 BPM 分析。脚本不会清空旧输出，目录中遗留文件可能影响统计或拼图；其“帧数”统计实际上按目录列表的行数计数。建议的 `seg` 目录未自动创建，补抽前需创建；最后打印的输出路径没有引号，若输出目录含空格，还需按实际路径补上引号。以上均是源脚本行为说明，未改动源代码。
