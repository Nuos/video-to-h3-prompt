# 01 — 取证命令库与音画交叉验证｜简体中文释义版

源文件：`references/01-forensics-commands.md`。源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。

本文件是独立的简体中文释义阅读版，按源文顺序先释义、后翻译；原始文件不作改动。命令、字段键、路径与引用标签保留原样，中文用于解释其含义；自然语言英文提示词均给出完整中文译文。此阅读版不是替代原始英文提示词或可执行技能的配置文件。音标采用常见英语读音；专有工具名、路径和代码符号不虚构统一读音。n.＝名词，v.＝动词，adj.＝形容词，adv.＝副词，phr.＝短语，abbr.＝缩略语。

## 01 · 标题与跨平台使用（源文第 1–3 行）

**词汇与术语**

- **PowerShell**，专有名词，Windows 常用的命令行与脚本环境；**bash** /bæʃ/，n.，命令行解释器，名称来自 Bourne Again SHell。
- **Windows / macOS / Linux**，操作系统名称；**cheatsheet** /ˈtʃiːt ʃiːt/，n.，速查表。
- `IN.mp4` 是输入视频文件名占位符；`IN` 在此作为输入代号。**input** /ˈɪnpʊt/，n.，输入；MP4 是媒体容器格式。

**简体中文译文**

# 01 — 取证命令库与音画交叉验证

跨平台使用方式：Windows 使用 PowerShell（本仓库的 `ffmpeg-cheatsheet.md` 也采用 PowerShell 风格），macOS/Linux 使用 bash。把 `IN.mp4` 替换为实际视频文件名；路径含空格或中文时必须加引号。原文建议中文路径先复制成使用纯英文路径的副本，并引用“§12”。

译注：保留原文的章节引用；本文件第 12 节实际为响度补充判据，路径问题另见 `07-onset-and-card-points.md`。

## 02 · 媒资建档命令（源文第 5–9 行）

**词汇与术语**

- **probe** /proʊb/，v./n.，探测；`ffprobe` 是媒体信息探测命令。
- **error** /ˈerər/，n.，错误；`-v error` 只显示错误级别日志。
- **show** /ʃoʊ/，v.，显示；**format** /ˈfɔːrmæt/，n.，格式；**stream** /striːm/，n.，媒体流。`-show_format` 与 `-show_streams` 输出容器和媒体流信息。
- **JSON** /ˈdʒeɪsən/，abbr.，JavaScript Object Notation，JavaScript 对象表示法；`-of json` 指定输出格式。

**简体中文译文**

## 1. 媒资建档

```powershell
ffprobe -v error -show_format -show_streams -of json "IN.mp4"
```

## 03 · 应记录的元数据（源文第 11–11 行）

**词汇与术语**

- **duration** /dʊˈreɪʃən/，n.，时长；**width** /wɪdθ/，n.，宽度；**height** /haɪt/，n.，高度。
- **frame rate** /freɪm reɪt/，名词短语，帧率；`r_frame_rate` 是原样保留的媒体字段键。
- **codec** /ˈkoʊdek/，n.，编解码器；**sample rate** /ˈsæmpəl reɪt/，名词短语，采样率，对应 `sample_rate`；**channels** /ˈtʃænəlz/，n. pl.，声道数。

**简体中文译文**

记录时长（`duration`）、宽×高（`width×height`）、帧率字段（`r_frame_rate`）、视频编码，以及音轨的编解码器（`codec`）、采样率（`sample_rate`）和声道数（`channels`）。原文按竖边更长归为 9:16，横边更长按 16:9、4:3 归类。

译注：这是源文的分类表述；仅凭横竖方向本身不能确定精确比例，精确比例仍需由宽高数值计算。

## 04 · 全片稀疏抽帧（源文第 13–18 行）

**词汇与术语**

- **fps** /ˌef piː ˈes/，abbr.，frames per second（frame /freɪm/，n.，帧；second /ˈsekənd/，n.，秒），即每秒帧数。
- **scale** /skeɪl/，v./n.，缩放；`scale=480:-1` 把宽度设为 480，并按比例计算高度。
- **frames** /freɪmz/，n. pl.，帧；`frames/` 是输出目录。`ffmpeg` 为媒体处理命令，`-y` 允许覆盖，`-i` 指定输入，`-vf` 指定视频滤镜；`%02d` 是两位十进制序号占位符。

**简体中文译文**

## 2. 全片稀疏抽帧（骨架层）

```powershell
# 2fps、统一宽 480
ffmpeg -y -i "IN.mp4" -vf "fps=2,scale=480:-1" frames/f_%02d.jpg
```

## 05 · 按片长选择抽帧间隔（源文第 20–20 行）

**词汇与术语**

- **s**，单位符号，second /ˈsekənd/（n.，秒）的简写；不是需要朗读的英文单词。

**简体中文译文**

按片长确定抽帧间隔：短于 5 秒取 0.2 秒；5–10 秒取 0.3–0.4 秒；10–15 秒取 0.15–0.2 秒；长于 15 秒取 0.2 秒，并在转折处补抽。

## 06 · 拼接缩略图网格（源文第 22–27 行）

**词汇与术语**

- **contact sheet** /ˈkɑːntækt ʃiːt/，名词短语，接触印样；这里指把视频帧排在一起的缩略图网格。
- **framerate** /ˈfreɪm reɪt/，n.，帧率；**tile** /taɪl/，v./n.，平铺、网格；**padding** /ˈpædɪŋ/，n.，留白间距；**color** /ˈkʌlər/，n.，颜色；**yellow** /ˈjeloʊ/，adj.，黄色的；**grid** /ɡrɪd/，n.，网格。

**简体中文译文**

## 3. 拼接缩略图网格，一次查看全片

以下命令生成 4 列×4 行的黄色间隔网格。输出文件名和命令参数保留原样。

```powershell
# 4 列 4 行，黄边便于读序；超过 16 帧会输出 grid_001/002 ...
ffmpeg -y -framerate 1 -i frames/f_%02d.jpg -vf "scale=240:-2,tile=4x4:padding=4:color=yellow" grid_%03d.jpg
```

## 07 · 转折区间密帧（源文第 29–35 行）

**词汇与术语**

- **fps** /ˌef piː ˈes/，abbr.，frames per second（frame /freɪm/，n.，帧；second /ˈsekənd/，n.，秒），即每秒帧数。
- **burst** /bɜːrst/，n.，短促爆发；此处指瞬时高速运镜或特效爆发。
- **scale** /skeɪl/，v.，缩放；**tile** /taɪl/，v.，平铺；**padding** /ˈpædɪŋ/，n.，间距；**yellow** /ˈjeloʊ/，adj.，黄色的。`seg/` 是片段帧目录，`-ss` 指起始时间，`-t` 指持续时间。

**简体中文译文**

## 4. 转折区间密帧（判别层）

从 8.5 秒开始抽取持续 2.5 秒的画面，按每秒 4 帧采样，并拼成网格。原注释中的 burst 指“短促爆发”；判断爆发、掰头或火光时，把帧率提高为 `fps=8`。命令原样保留：

```powershell
# -ss 起点 -t 持续；4fps，判别 burst/掰头/火光时上 fps=8
ffmpeg -y -ss 8.5 -t 2.5 -i "IN.mp4" -vf "fps=4,scale=360:-1" seg/c_%02d.jpg
ffmpeg -y -framerate 1 -i seg/c_%02d.jpg -vf "scale=200:355,tile=5x2:padding=3:color=yellow" seg/c_grid.jpg
```

## 08 · 导出原分辨率关键帧（源文第 37–41 行）

**词汇与术语**

- **key** /kiː/，adj.，关键的；文件名 `key_9_8.jpg` 表示 9.8 秒处的关键帧。
- **frames** /freɪmz/，n. pl.，帧；`-frames:v 1` 只输出一帧视频；`-q:v 2` 是视频图像质量参数，`-ss 9.8` 指定时间点。

**简体中文译文**

## 5. 原分辨率单帧终核

```powershell
ffmpeg -y -ss 9.8 -i "IN.mp4" -frames:v 1 -q:v 2 key_9_8.jpg
```

## 09 · 提取音频（源文第 43–47 行）

**词汇与术语**

- **audio** /ˈɔːdioʊ/，n.，音频；**WAV** /wæv/，音频文件格式名称。
- **k**，单位前缀 kilo /ˈkiːloʊ/，表示千；22.05k 与 8k 在这里分别指 22,050 与 8,000 赫兹的采样率。`-vn` 不输出视频，`-ac 1` 使用单声道，`-ar 22050` 设置音频采样率。

**简体中文译文**

## 6. 提取音频（22.05 千赫兹单声道足够用于分析；只分析响度时 8 千赫兹即可）

```powershell
ffmpeg -y -i "IN.mp4" -vn -ac 1 -ar 22050 audio.wav
```

## 10 · 生成频谱图（源文第 49–53 行）

**词汇与术语**

- **vs** /ˈvɜːrsəs/，abbr.，versus，相对于、与……对比。
- **spectrum** /ˈspektrəm/，n.，频谱；**legend** /ˈledʒənd/，n.，图例。`showspectrumpic` 是生成频谱图片的滤镜；`s=1000x400` 指定图像尺寸，`legend=1` 显示图例，`-lavfi` 指定滤镜图。

**简体中文译文**

## 7. 频谱图（判断音乐与现场声音）

```powershell
ffmpeg -y -i audio.wav -lavfi showspectrumpic=s=1000x400:legend=1 spectrum.jpg
```

## 11 · 频谱判据：规则低频条纹（源文第 55–55 行）

**词汇与术语**

- **BGM** /ˌbiː dʒiː ˈem/，abbr.，background music /ˈbækɡraʊnd ˈmjuːzɪk/，背景音乐。

**简体中文译文**

等间隔、等宽的低频竖纹贯穿全片 → 鼓机或规则节拍，存在背景音乐。

## 12 · 频谱判据：人声、底噪与瞬时音效（源文第 56–58 行）

**词汇与术语**

本段没有需要另行释义的英文词项。

**简体中文译文**

- **宽带随机能量 + 偶发上扬谐波曲线** → 人声说/笑/喊；
- **全频段持续铺底** → 环境底噪（街道、风、发动机）；
- **定格/喷溅/命中瞬间的竖向亮块** → 瞬时音效，与画面事件对齐。

## 13 · 粗粒度能量与速度可信度（源文第 60–64 行）

**词汇与术语**

- **RMS** /ˌɑːr em ˈes/，abbr.，root mean square /ruːt miːn skwer/，均方根；这里用来描述音频的短时能量包络。
- **BPM** /ˌbiː piː ˈem/，abbr.，beats per minute /biːts pər ˈmɪnɪt/，每分钟拍数。
- **Python** /ˈpaɪθɑːn/，编程语言名称；**probe** /proʊb/，n./v.，探测；`scripts/audio_probe.py` 是音频探测脚本路径。

**简体中文译文**

## 8. 均方根能量包络与每分钟拍数可信度（粗粒度：哪些位置更响）

```powershell
python scripts/audio_probe.py audio.wav
```

## 14 · 每分钟拍数误检判据（源文第 66–70 行）

**词汇与术语**

- **BPM** /ˌbiː piː ˈem/，abbr.，beats per minute /biːts pər ˈmɪnɪt/，每分钟拍数。
- **BGM** /ˌbiː dʒiː ˈem/，abbr.，background music /ˈbækɡraʊnd ˈmjuːzɪk/，背景音乐。
- **RMS** /ˌɑːr em ˈes/，abbr.，root mean square /ruːt miːn skwer/，均方根；这里用来描述音频的短时能量包络。
- **onset** /ˈɑːnset/，n.，起始、起音；本项目中指音头，即一个声音事件开始的时刻。
- **std**，abbr.，standard deviation /ˈstændərd ˌdiːviˈeɪʃən/，标准差；**mean** /miːn/，n.，平均值；**kick** /kɪk/，n.，底鼓或低频鼓击。
- `librosa` 为音频分析库名称。`onset std / onset mean` 表示音头相关统计量的标准差与均值之比，表达式保留原样；源文未在这行明确说明统计对象。

**简体中文译文**

**每分钟拍数的误检判据（同时满足时，判为“没有稳定的背景音乐”）**：

1. 音头相关统计量的标准差与均值之比大于 0.8，即 `onset std / onset mean > 0.8`；源文据此解释为节拍不规律。
2. 频谱中没有等间隔的底鼓网格。
3. 均方根能量的高峰是彼此分离的瞬时峰，而非周期性起伏。

三条同时满足时，原文认为 librosa 得到的每分钟拍数，是把随机音头误认成了规则节拍；结论写为“没有稳定的背景音乐”。

译注：仓库 `scripts/audio_probe.py` 的第 47–50 行实际计算的是音头**强度包络**的均值和标准差，不是音头间隔的统计量；因此本译本不将两者等同。该比值与频谱、画面核对结合使用，不单独证明背景音乐有无。

## 15 · 音头检测与卡点的必要性（源文第 72–74 行）

**词汇与术语**

- **onset** /ˈɑːnset/，n.，起始、起音；本项目中指音头，即一个声音事件开始的时刻。
- **RMS** /ˌɑːr em ˈes/，abbr.，root mean square /ruːt miːn skwer/，均方根；这里用来描述音频的短时能量包络。

**简体中文译文**

## 9. 音头检测与卡点（细粒度：每个重音位于哪一帧）

0.5 秒一格的均方根能量分析过于粗略。卡点剪辑要求切镜、定格、命中或爆发与音乐对齐，因此必须使用音头时刻。

## 16 · 音头检测命令（源文第 76–79 行）

**词汇与术语**

- **onset** /ˈɑːnset/，n.，起始、起音；本项目中指音头，即一个声音事件开始的时刻。
- **CSV** /ˌsiː es ˈviː/，abbr.，comma-separated values /ˈkɑːmə ˈsepəreɪtɪd ˈvæljuːz/，逗号分隔值格式；`--csv onsets.csv` 指定表格输出文件。
- **probe** /proʊb/，v.，探测；`scripts/onset_probe.py` 为音头探测脚本路径。

**简体中文译文**

```powershell
python scripts/onset_probe.py audio.wav
python scripts/onset_probe.py audio.wav --csv onsets.csv
```

## 17 · 音头检测输出及限制（源文第 81–81 行）

**词汇与术语**

- **S / H**，本项目输出等级标签，分别表示 strong /strɔːŋ/（adj.，强的）与 hard /hɑːrd/（adj.，硬的、明显的）；`.` 为弱音头标记。
- **tempo** /ˈtempoʊ/，n.，音乐速度；`numpy`、`scipy`、`librosa` 均为 Python 库名称，保留拼写。

**简体中文译文**

输出内容包括：强音头（S）与硬音头（H）的时间，作为卡点候选；用 `.` 标记的轮指弱音；逐秒密度与强度轮廓，用于描述乐句形状；以及由自相关估计的参考音乐速度。**自由散板或轮指独奏（如琵琶独奏）的速度估计置信度低，不能把它当作节拍器。**详见 `07-onset-and-card-points.md`。该脚本仅依赖 numpy 和 scipy，不需要 librosa。

## 18 · 硬切检测命令（源文第 83–88 行）

**词汇与术语**

- **cut** /kʌt/，n./v.，切镜、剪切；**scene** /siːn/，n.，场景，代码中是场景变化检测分数。
- **select** /sɪˈlekt/，v.，选择；**show info** /ʃoʊ ˈɪnfoʊ/，动词短语，显示信息；`showinfo` 为滤镜名，`gt` 表示 greater than /ˈɡreɪtər ðæn/（大于），`null` /nʌl/ 表示空输出。
- **PTS** /ˌpiː tiː ˈes/，abbr.，presentation timestamp /ˌprezənˈteɪʃən ˈtaɪmstæmp/，呈现时间戳；`pts_time` 为时间字段。`Select-String` 是 PowerShell 文本匹配命令，`NUL` 是 Windows 空设备。

**简体中文译文**

## 10. 硬切检测与“火光造成的伪切镜”排除

命令注释中的 scene 指场景变化分数：阈值 0.4 用于寻找硬切，0.3 则放宽阈值以寻找候选。命令保留原样：

```powershell
# scene 阈值 0.4 找硬切（0.3 宽松找候选）
ffmpeg -i "IN.mp4" -filter:v "select='gt(scene,0.4)',showinfo" -f null NUL 2>&1 | Select-String "pts_time"
```

## 19 · 排除闪光引发的伪切镜（源文第 90–90 行）

**词汇与术语**

- **cut** /kʌt/，n.，切镜；**false cut** /fɔːls kʌt/，名词短语，误检出的切镜。

**简体中文译文**

**枪口火光、爆炸闪光、能量光束与白闪可能被误报为切镜**，因为亮度突然改变，但机位仍连续。对每个候选切点用密帧核对：闪光前后机位、角度和景别连续，说明仍为同一镜头；只有机位真正发生跳变，才算硬切。战斗片齐射瞬间常出现成簇的伪切镜，不能全部采纳。最终计算：`镜头数 = 真硬切数 + 1`。

## 20 · 烧录时间码的缩略图网格（源文第 92–97 行）

**词汇与术语**

- **contact sheet** /ˈkɑːntækt ʃiːt/，名词短语，缩略图网格；**timecode** /ˈtaɪmkoʊd/，n.，时间码。
- **fps** /ˌef piː ˈes/，abbr.，frames per second（frame /freɪm/，n.，帧；second /ˈsekənd/，n.，秒），即每秒帧数。
- **onset** /ˈɑːnset/，n.，起始、起音；本项目中指音头，即一个声音事件开始的时刻。
- **draw text** /drɔː tekst/，动词短语，绘制文字；`drawtext` 为文字叠加滤镜。**font color** /fɑːnt ˈkʌlər/，名词短语，字体颜色；**font size** /fɑːnt saɪz/，名词短语，字号；**box** /bɑːks/，n.，文字底框；**black** /blæk/，adj.，黑色的。`hms` 表示小时、分钟、秒的显示格式，`pts` 表示呈现时间戳；`black@0.6` 为带透明度的黑色底框设置。

**简体中文译文**

## 11. 烧录时间码的缩略图网格（在一张图上核对机位与卡点）

命令每秒抽取 4 帧，把时间码烧录在左上角，再拼为 4×4 网格，每张图覆盖 4 秒。逐段确定机位，然后与音头时刻对账。命令中的英文键名保留原样：

```powershell
# 4fps、左上烧时间码、拼 4x4（每张覆盖 4 秒），逐段定机位再与 onset 对账
ffmpeg -y -i "IN.mp4" -vf "fps=4,scale=320:-1,drawtext=text='%{pts\:hms}':x=6:y=6:fontcolor=yellow:fontsize=18:box=1:boxcolor=black@0.6,tile=4x4:padding=3:color=yellow" -vsync 0 sb_%02d.jpg
```

## 21 · 响度补充分析（源文第 99–105 行）

**词汇与术语**

- **volume** /ˈvɑːljuːm/，n.，音量；**detect** /dɪˈtekt/，v.，检测；`volumedetect` 为响度分析滤镜。
- **WAV** /wæv/，音频格式名称；**null** /nʌl/，n.／输出格式标识，空输出；`grep` /ɡrep/ 是文本匹配命令。`-af` 指定音频滤镜，`2>&1` 合并错误与标准输出，竖线 `|` 把输出传给下一命令。

**简体中文译文**

## 12. 响度补充判据（音量检测滤镜 `volumedetect`）

第一条命令提取 8 千赫兹单声道 WAV。第二条在 PowerShell 中筛选含“volume”的日志；最后一行注释给出 bash 中相应的筛选方式。命令原样保留：

```powershell
ffmpeg -y -i "IN.mp4" -vn -ac 1 -ar 8000 -f wav out8k.wav
ffmpeg -i out8k.wav -af "volumedetect" -f null NUL 2>&1 | Select-String volume   # PowerShell
# bash: ... -f null - 2>&1 | grep volume
```

## 22 · 响度与配乐方案的对应（源文第 107–107 行）

**词汇与术语**

- **mean** /miːn/，adj./n.，平均的、均值；**max** /mæks/，abbr.（名词／形容词），maximum /ˈmæksɪməm/ 的缩写，最大值；**volume** /ˈvɑːljuːm/，n.，音量。
- **recipe** /ˈresəpi/，n.，配方；此处指可组合的配乐设计方案。

**简体中文译文**

平均音量、最大音量与配乐方案的对应关系，见 `audio-heuristics.md`。

## 23 · 音画交叉验证矩阵（源文第 109–118 行）

**词汇与术语**

- **RMS** /ˌɑːr em ˈes/，abbr.，root mean square /ruːt miːn skwer/，均方根；这里用来描述音频的短时能量包络。
- **onset** /ˈɑːnset/，n.，起始、起音；本项目中指音头，即一个声音事件开始的时刻。
- **BPM** /ˌbiː piː ˈem/，abbr.，beats per minute /biːts pər ˈmɪnɪt/，每分钟拍数。
- **editing** /ˈedɪtɪŋ/，n.，剪辑；**camera** /ˈkæmərə/，n.，相机或运镜；**integrated** /ˈɪntɪɡreɪtɪd/，adj.，综合的，此处为综合描述字段的简称；**soundscape** /ˈsaʊndskeɪp/，n.，声景；**lighting** /ˈlaɪtɪŋ/，n.，灯光。
- **RGB** /ˌɑːr dʒiː ˈbiː/，abbr.，red /red/、green /ɡriːn/、blue /bluː/（红、绿、蓝）三色通道；**boom** /buːm/，n.，轰鸣冲击声。
- **non-diegetic music** /ˌnɑːn ˌdaɪəˈdʒetɪk ˈmjuːzɪk/，名词短语，非叙事空间内的音乐，即画外配乐；`fully_copy` 意为完整复制；**rubato** /ruːˈbɑːtoʊ/，n.，弹性速度；原文用其描述自由散板。
- S/H 为强/硬音头等级；**cut** /kʌt/，n.，切镜；**kick** /kɪk/，n.，底鼓；**music** /ˈmjuːzɪk/，n.，音乐。

**简体中文译文**

## 13. 音画交叉验证矩阵（工作模板）

| 均方根峰／强音头时刻 | 密帧画面证据（谁先动／方向／结果／机位） | 候选解释 → 裁决结论 | 对应字段及含义 |
|---|---|---|---|
| 1.75 秒（强音头 S） | 反打受害者正面警觉，机位跳变 | 连续运镜？×／硬切？√ | `editing(cut)`（剪辑中的切镜）＋`camera`（相机） |
| 6.6–7.0 秒（强音头 S＋均方根峰） | 枪口火舌，随后贴臀机位冒火花 | 火光伪切镜？√（机位连续）／真切镜？× | `integrated`（综合描述）＋`soundscape`（声景） |
| 11–12.5 秒（密集强／硬音头 S/H＋均方根最高峰） | 双枪齐射、高俯拍趴地连中 | 火力高潮，一串卡点 | `integrated`（综合描述）＋`editing`（剪辑）＋`music`（音乐） |
| 22.55 秒（硬音头 H） | 硬切背肩近景、转暖调、开始回头 | 关键硬切，情绪转场 √ | `editing`（剪辑）＋`camera`（相机）＋`lighting`（灯光） |
| 28.51 秒（强音头 S） | 白光＋红绿蓝通道故障效果＋黑翼爆发 | 后期特效爆发，对齐尾音 √ | `editing`（特效）＋`soundscape(boom)`（声景中的轰鸣冲击声） |
| 全程 | 音头间隔不匀，没有底鼓网格 | 72.8 拍／分钟属于误检 → 自由散板，不填写每分钟拍数 | `non_diegetic_music=fully_copy+rubato`（配乐＝完整复制＋弹性速度／散板） |

## 24 · 交叉验证矩阵规则（源文第 120–120 行）

**词汇与术语**

- **RMS** /ˌɑːr em ˈes/，abbr.，root mean square /ruːt miːn skwer/，均方根；这里用来描述音频的短时能量包络。
- **onset** /ˈɑːnset/，n.，起始、起音；本项目中指音头，即一个声音事件开始的时刻。
- **S/H**，强／硬音头等级标签；**s** 为秒的单位符号。

**简体中文译文**

规则：**每个硬切、定格、冲击或爆发，都要在前后 0.1 秒内找到强／硬音头（S/H）；每个均方根能量峰，都要在画面里找到成因；每个关键动作，都要在音频里找到印证。**无法对应的行应返回第 4 节进行密帧核对，或进入提问流程。

## 25 · 一键取证命令（源文第 122–131 行）

**词汇与术语**

- **forensic** /fəˈrensɪk/，adj.，取证的；**probe** /proʊb/，n./v.，探测。
- **profile** /ˈproʊfaɪl/，n.，配置档；`-NoProfile` 不加载个人配置。**execution policy** /ˌeksɪˈkjuːʃən ˈpɑːləsi/，名词短语，执行策略；**bypass** /ˈbaɪpæs/，v./n.，绕过，在此是 `-ExecutionPolicy` 的参数值。
- **file** /faɪl/，n.，文件；**video** /ˈvɪdioʊ/，n.，视频；**out dir**，output directory /ˈaʊtpʊt dəˈrektəri/ 的简写，输出目录。`-File`、`-Video`、`-OutDir` 均为原样保留的参数。

**简体中文译文**

## 14. 一键取证

Windows 使用以下 PowerShell 命令；macOS/Linux 使用 bash 命令。命令原样保留：

```powershell
# Windows PowerShell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/forensic_probe.ps1 -Video "IN.mp4" -OutDir forensic_out
```
```bash
# macOS / Linux
bash scripts/forensic_probe.sh "IN.mp4" forensic_out
```

## 26 · 一键取证产物与后续工作（源文第 133–133 行）

**词汇与术语**

- **fps** /ˌef piː ˈes/，abbr.，frames per second（frame /freɪm/，n.，帧；second /ˈsekənd/，n.，秒），即每秒帧数。
- **RMS** /ˌɑːr em ˈes/，abbr.，root mean square /ruːt miːn skwer/，均方根；这里用来描述音频的短时能量包络。
- **BPM** /ˌbiː piː ˈem/，abbr.，beats per minute /biːts pər ˈmɪnɪt/，每分钟拍数。
- **onset** /ˈɑːnset/，n.，起始、起音；本项目中指音头，即一个声音事件开始的时刻。
- **probe** /proʊb/，n.，探测结果；`audio.wav` 为输出音频文件名。

**简体中文译文**

产出每秒 2 帧的图像、全片网格、`audio.wav` 音频、频谱图、媒体探测信息、均方根能量／每分钟拍数表，以及**音头卡点表**。之后由人工继续进行密帧判别、片型分流（`06` 号参考文件）与因果重建。
