# FFmpeg 视频逆向工程速查：逐段词汇释义与简体中文译文

源文件：`references/ffmpeg-cheatsheet.md`。源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。本文件为阅读用译本，原文和原命令不改动；行号对应该版本。命令、字段、路径和文件扩展名保留原拼写，英文注释在对应正文中翻译。译注与原文译文分别标明。

## 1. 标题与命令环境（源文件第 1–4 行）

**词汇与术语**

- cheatsheet /ˈtʃiːtʃiːt/，名词：速查表、速查手册；video /ˈvɪdiəʊ/，名词：视频。
- reverse-engineering /rɪˌvɜːs ˌendʒɪˈnɪərɪŋ/，名词：逆向工程；`FFmpeg` 为工具名称，保留原名。

**简体中文译文**

用于视频逆向工程的 FFmpeg 速查手册。

**词汇与术语**

- assume /əˈsjuːm/，动词：假定；backtick /ˈbæktɪk/，名词：反引号；line-continuation /laɪn kənˌtɪnjuˈeɪʃən/，名词短语：续行。
- swap /swɒp/，动词：替换；loop /luːp/，名词：循环；pipeline /ˈpaɪplaɪn/，名词：处理流程；wrapped /ræpt/，过去分词：已封装。
- first-pass /fɜːst pɑːs/，定语短语：首轮的；`NUL` 与 `/dev/null` 分别是相关环境中丢弃输出的位置。

**简体中文译文**

所有命令都假定在 Windows 上的 PowerShell 中运行，反引号 `` ` `` 用来续行。在 Bash 中使用时，需要调整循环写法，并把 `NUL` 改为 `/dev/null`。完整的首轮处理流程也已封装在 `scripts/forensic_probe.ps1` 中。

## 2. 探测视频元数据（源文件第 5–10 行）

**词汇与术语**

- probe /prəʊb/，动词：探测；metadata /ˈmetədeɪtə/，名词：元数据；format /ˈfɔːmæt/，名词：容器格式；stream /striːm/，名词：媒体流。
- JSON /ˈdʒeɪsən/，名词性缩略语，JavaScript Object Notation：JavaScript 对象表示法；error /ˈerə/，名词：错误。

**简体中文译文**

探测视频元数据。下列命令只输出错误级日志，并以 JSON 格式列出容器信息和各媒体流信息；`<video.mp4>` 是需要替换的输入视频占位路径。

```powershell
ffprobe -v error -show_format -show_streams -of json "<video.mp4>"
```

## 3. 精简摘要命令（源文件第 11–18 行）

**词汇与术语**

- one-line /wʌn laɪn/，定语短语：一行式的、精简的；summary /ˈsʌməri/，名词：摘要；entry /ˈentri/，名词：条目。
- duration /djʊˈreɪʃən/：时长；bit rate /bɪt reɪt/：比特率；codec /ˈkəʊdek/：编解码器；type /taɪp/：类型；name /neɪm/：名称，均为名词或名词短语。
- width /wɪdθ/：宽度；height /haɪt/：高度；frame rate /freɪm reɪt/：帧率；sample rate /ˈsɑːmpəl reɪt/：采样率；channel /ˈtʃænəl/：声道。
- `nb_frames` 为帧数字段；`nw=1` 为不显示章节包裹标记的输出选项缩写，标识符不改写。

**简体中文译文**

精简摘要：读取容器时长和比特率，以及媒体流类型、编解码器名称、宽高、帧率、帧数、采样率和声道数。

```powershell
ffprobe -v error -show_entries format=duration,bit_rate `
  -show_entries stream=codec_type,codec_name,width,height,r_frame_rate,nb_frames,sample_rate,channels `
  -of default=nw=1 "<video.mp4>"
```

## 4. 支持后续判断的六项字段（源文件第 19–20 行）

**词汇与术语**

- field /fiːld/，名词：字段；drive /draɪv/，动词：驱动、决定；portrait /ˈpɔːtrət/，名词或定语：竖向画幅；landscape /ˈlændskeɪp/，名词或定语：横向画幅。
- sanity /ˈsænəti/，名词：这里指合理性检查；seek /siːk/，名词或动词：定位到媒体中的指定时刻；cleaner /ˈkliːnə/，形容词比较级：更干净的、更少杂误的。
- B-frame /ˈbiː freɪm/，名词：B 帧，即双向预测编码帧；`has_b_frames` 是程序字段，不能替换成中文。

**简体中文译文**

以下六项字段影响后续决策：`duration` 用于确定最终 H3 时长，原文给出误差范围 ±0.02；`width×height` 用于判断竖屏还是横屏；`r_frame_rate` 用于读取帧率；`nb_frames` 用来核对“时长×每秒帧数”是否合理；`codec_name` 给出编解码器名称；`has_b_frames` 大于零时，原文建议加入 `-noaccurate_seek`，以获得更干净的定位结果。

**词汇与术语**

- accurate /ˈækjərət/，形容词：精确的；disable /dɪsˈeɪbəl/，动词：禁用；option /ˈɒpʃən/，名词：选项。

**简体中文译文（译注）**

上述为源文建议的忠实翻译。`-noaccurate_seek` 的字面和功能含义是禁用精确定位；不能把它一概解释为提升时间精度。是否需要该选项应按输入、解码与定位方式核对；本译本不改写原命令。另：前一条精简命令没有显式列入 `has_b_frames`，需要从完整流信息或额外字段查询中读取它。

## 5. 固定间隔抽帧：稀疏骨架阶段（源文件第 21–32 行）

**词汇与术语**

- extract /ɪkˈstrækt/，动词：提取；fixed interval /fɪkst ˈɪntəvəl/，名词短语：固定间隔；sparse /spɑːs/，形容词：稀疏的；skeleton /ˈskelɪtən/，名词：骨架。
- count /kaʊnt/，名词：数量、计数；directory /dəˈrektəri/，名词：目录；force /fɔːs/，动词或参数词：强制；scale /skeɪl/，动词：缩放。
- `iw` 是滤镜中表示输入宽度的标识符；`F3` 是三位小数格式；`-frames:v 1` 指定输出一帧视频图像。

**简体中文译文**

按固定间隔提取帧，用于先建立稀疏骨架。示例把间隔设为 0.2 秒，计数上界设为 73，先创建输出目录，再从 `i=0` 到 `i=73` 逐次取帧；每个时间点保留三位小数，输出图像宽度为输入宽度的一半、高度保持比例，JPEG 质量参数为 `3`。

```powershell
$interval = 0.2; $count = 73; $out = "D:\path\frames"
New-Item -ItemType Directory -Force -Path $out | Out-Null
for ($i=0; $i -le $count; $i++) {
  $t = "{0:F3}" -f ($i * $interval)
  ffmpeg -y -ss $t -i "<video.mp4>" -frames:v 1 `
         -vf "scale=iw/2:-1" -q:v 3 "$out\f_$i.jpg" -loglevel error
}
```

## 6. 按片长选择间隔（源文件第 33–34 行）

**词汇与术语**

- duration /djʊˈreɪʃən/，名词：时长；targeted /ˈtɑːɡɪtɪd/，形容词：有针对性的；transition /trænˈzɪʃən/，名词：转折、过渡。
- lever /ˈliːvə/，名词：这里比喻影响结果的关键手段；re-extract /ˌriː ɪkˈstrækt/，动词：重新提取；missed /mɪst/，形容词：漏掉的；half /hɑːf/，名词或定语：一半。

**简体中文译文**

按时长选间隔：不足 5 秒时取 0.2 秒；5–10 秒时取 0.3–0.4 秒；10–15 秒时取 0.15–0.2 秒；超过 15 秒时取 0.2 秒，并对转折点做针对性补抽。最能提升质量的一项做法，是把间隔减半，重新抽取先前漏掉的转折。

## 7. 按连续帧率抽取：转折区间密帧（源文件第 35–43 行）

**词汇与术语**

- continuous-rate /kənˈtɪnjuəs reɪt/，定语短语：按连续固定速率的；dense pass /dens pɑːs/，名词短语：一轮密集检查。
- whole clip /həʊl klɪp/，名词短语：整个片段；ambiguous window /æmˈbɪɡjuəs ˈwɪndəʊ/，名词短语：有歧义的时间窗口；needed /ˈniːdɪd/，形容词：所需的。
- fps：每秒帧数；width /wɪdθ/，名词：宽度。

**简体中文译文**

按连续帧率抽取，用于密集检查转折区间。第一条英文注释意为“整段每秒 2 帧，宽度 480”。第二条意为“对一个 2.5 秒的歧义窗口按每秒 4 帧抽取，必要时用每秒 8 帧”；其示例窗口从 8.5 秒开始。命令和原注释保留如下。

```powershell
# whole clip at 2fps, width 480
ffmpeg -y -i "<video.mp4>" -vf "fps=2,scale=480:-1" frames/f_%02d.jpg
# a 2.5s ambiguous window at 4fps (8fps if needed)
ffmpeg -y -ss 8.5 -t 2.5 -i "<video.mp4>" -vf "fps=4,scale=360:-1" seg/c_%02d.jpg
```

## 8. 指定时间的单帧：原分辨率终核（源文件第 44–49 行）

**词汇与术语**

- single frame /ˈsɪŋɡəl freɪm/，名词短语：单帧；exact time /ɪɡˈzækt taɪm/，名词短语：准确时刻。
- full-resolution /fʊl ˌrezəˈluːʃən/，形容词：全分辨率的、原分辨率的；final check /ˈfaɪnəl tʃek/，名词短语：最终核对。

**简体中文译文**

在准确指定的时间提取单帧，用原分辨率做最终核对。示例从 9.800 秒定位，输出一帧 JPEG，不添加缩放滤镜，保存为 `key_9_8.jpg`。

```powershell
ffmpeg -y -ss 9.800 -i "<video.mp4>" -frames:v 1 -q:v 2 "key_9_8.jpg"
```

## 9. 帧总览与网格：一次读完整条时间线（源文件第 50–60 行）

**词汇与术语**

- contact sheet /ˈkɒntækt ʃiːt/，名词短语：帧总览图；grid /ɡrɪd/，名词：网格；timeline /ˈtaɪmlaɪn/，名词：时间线。
- padding /ˈpædɪŋ/，名词：间距；reading order /ˈriːdɪŋ ˈɔːdə/，名词短语：阅读顺序；obvious /ˈɒbviəs/，形容词：明显的；dense window /dens ˈwɪndəʊ/：密集抽帧窗口。

**简体中文译文**

生成帧总览／网格，一次查看整条时间线。第一条注释意为“4×4 网格，黄色间距让阅读顺序更清楚”；第二条意为“密集窗口使用 5×2 网格”。第一组每张小图宽 240，高度等比例取偶数，间距为 4；第二组每张小图固定为 200×355，间距为 3。原命令如下。

```powershell
# 4x4 grid, yellow padding makes reading order obvious
ffmpeg -y -framerate 1 -i frames/f_%02d.jpg `
  -vf "scale=240:-2,tile=4x4:padding=4:color=yellow" grid_%03d.jpg
# dense window 5x2
ffmpeg -y -framerate 1 -i seg/c_%02d.jpg `
  -vf "scale=200:355,tile=5x2:padding=3:color=yellow" seg/c_grid.jpg
```

## 10. 多张总览图输出（源文件第 61–62 行）

**词汇与术语**

- input /ˈɪnpʊt/，名词：输入；emit /iˈmɪt/，动词：输出；multiple /ˈmʌltɪpəl/，形容词：多张的；sheet /ʃiːt/，名词：图页。

**简体中文译文**

当输入帧多于 16 张时，FFmpeg 会输出多张 `grid_001/002...` 总览图。此处对应带 `%03d` 编号模式的 4×4 网格输出。

## 11. 音频导出与频谱图（源文件第 63–72 行）

**词汇与术语**

- audio dump /ˈɔːdiəʊ dʌmp/，名词短语：音频导出；spectrogram /ˈspektrəɡræm/，名词：时频谱图；analysis /əˈnæləsɪs/，名词：分析。
- grade /ɡreɪd/，名词：等级、用途级别；loudness /ˈlaʊdnəs/，名词：响度；volume /ˈvɒljuːm/，名词：音量；credibility /ˌkredəˈbɪləti/，名词：可信度。
- RMS /ˌɑːr em ˈes/，Root Mean Square：均方根；BPM /ˌbiː piː ˈem/，Beats Per Minute：每分钟拍数；legend /ˈledʒənd/：图例。

**简体中文译文**

导出音频并生成频谱图。第一个英文注释“analysis grade”意为“用于分析的规格”：导出 22050 Hz 单声道 WAV。随后生成带图例的 1000×400 频谱图。第二个注释“loudness grade”意为“用于响度检测的规格”：导出 8000 Hz 单声道 WAV，再运行 `volumedetect`，把输出合并后筛选包含 `volume` 的行。最后的注释“RMS + BPM credibility”意为“均方根与 BPM 可信度分析”，由本仓库 Python 脚本完成。

```powershell
ffmpeg -y -i "<video.mp4>" -vn -ac 1 -ar 22050 audio.wav         # analysis grade
ffmpeg -y -i audio.wav -lavfi showspectrumpic=s=1000x400:legend=1 spectrum.jpg
ffmpeg -y -i "<video.mp4>" -vn -ac 1 -ar 8000 -f wav out8k.wav   # loudness grade
ffmpeg -i out8k.wav -af "volumedetect" -f null NUL 2>&1 | Select-String volume
python scripts/audio_probe.py audio.wav                          # RMS + BPM credibility
```

## 12. 帧间差异序列：自动寻找硬切（源文件第 73–83 行）

**词汇与术语**

- visual /ˈvɪʒuəl/，形容词：视觉的；difference /ˈdɪfrəns/，名词：差异；strip /strɪp/，名词：连续排列的条带、序列。
- auto-locate /ˌɔːtəʊ ləʊˈkeɪt/，动词：自动定位；hard cut /hɑːd kʌt/，名词短语：硬切、直接切镜。
- previous /ˈpriːviəs/，形容词：前一个的，变量中缩写为 `prev`；blend /blend/，动词：混合；mode /məʊd/，名词：模式。

**简体中文译文**

建立视觉差异序列，用来自动定位硬切。先创建 `diff` 目录，然后对第 1 至第 73 张图片分别与前一张比较；`blend=all_mode=difference` 计算差异图，每对图片输出一帧到 `diff/d_$i.jpg`。

```powershell
New-Item -ItemType Directory -Force -Path diff | Out-Null
for ($i=1; $i -le 73; $i++) {
  $prev = $i - 1
  ffmpeg -y -i "f_$i.jpg" -i "f_$prev.jpg" `
         -filter_complex "blend=all_mode=difference" -frames:v 1 "diff/d_$i.jpg"
}
```

## 13. 差异图的解释（源文件第 84–85 行）

**词汇与术语**

- nearly /ˈnɪəli/，副词：几乎；identical /aɪˈdentɪkəl/，形容词：相同的；continuous /kənˈtɪnjuəs/，形容词：连续的；bright /braɪt/，形容词：明亮的。
- composition /ˌkɒmpəˈzɪʃən/，名词：构图；angle /ˈæŋɡəl/，名词：角度；focal length /ˈfəʊkəl leŋθ/，名词短语：焦距。
- push /pʊʃ/，名词或动词：推进；pull /pʊl/，名词或动词：后拉；pan /pæn/，名词或动词：水平摇摄；smooth /smuːð/，形容词：平滑的。

**简体中文译文**

接近全黑的 `diff` 表示画面相同、具有连续性；明亮输出表示硬切。构图跳变，例如角度或焦距突然变化，也会被读作切镜；平滑推进、后拉或水平摇摄属于相机运动，不是切镜。

**词汇与术语**

- candidate /ˈkændɪdət/，名词：候选项；flash /flæʃ/，名词：闪光；motion /ˈməʊʃən/，名词：运动。

**简体中文译文（译注）**

源段采用了简化的判读表述。明亮差异图只表明两帧差异较大，闪光、爆炸和快速运动也可能造成这种结果；应作为候选切点，并回看邻近密帧判断。本仓库其他章节也要求排除枪口火光等伪切镜。

## 14. 首帧与尾帧：图像锚点（源文件第 86–93 行）

**词汇与术语**

- first /fɜːst/，序数词或形容词：第一、起始的；last /lɑːst/，形容词：最后的；anchor /ˈæŋkə/，名词：锚点、约束基准。
- I2VA /ˌaɪ tuː viː ˈeɪ/、L2VA /ˌel tuː viː ˈeɪ/，模型模式标识符：本项目分别用于首帧图像条件生成和尾帧图像条件生成；源文件未在此展开全称，因此不补造官方全称。
- select /sɪˈlekt/，动词：选择；duration /djʊˈreɪʃən/，名词：时长，变量中为 `dur`。

**简体中文译文**

提取首帧与尾帧，作为 I2VA／L2VA 的锚点。第一条通过 `select=eq(n\,0)` 选择编号为零的第一帧，输出 `first.jpg`；随后读取视频总时长，再以该时长作为定位值，尝试输出 `last.jpg`。

```powershell
ffmpeg -y -i "<video.mp4>" -vf "select=eq(n\,0)" -frames:v 1 first.jpg
$dur = (ffprobe -v error -show_entries format=duration -of csv=p=0 "<video.mp4>")
ffmpeg -y -ss $dur -i "<video.mp4>" -frames:v 1 last.jpg
```

**词汇与术语**

- end /end/，名词：末尾；timestamp /ˈtaɪmstæmp/，名词：时间戳；available /əˈveɪləbəl/，形容词：可用的。

**简体中文译文（译注）**

源命令把定位时刻设在总时长处，这通常已经是媒体末尾，不保证仍有可解码帧。因而这条命令不能被视为已验证的可靠尾帧提取方案；实际尾帧时间戳通常早于总时长。译本保留原命令，不暗中修正。

## 15. 常见失败情况（源文件第 94–104 行）

**词汇与术语**

- common /ˈkɒmən/，形容词：常见的；failure mode /ˈfeɪljə məʊd/，名词短语：失败情况、故障模式。
- symptom /ˈsɪmptəm/，名词：现象；cause /kɔːz/，名词：原因；fix /fɪks/，名词或动词：修正办法、修正。

**简体中文译文**

常见失败情况。原表的“现象／原因／修正办法”逐行译为下表；每行先给词汇释义，再列中文内容，命令参数仍按原样保留。

| 源行 | 词汇与术语（先读） | 简体中文译文：现象 | 简体中文译文：原因 | 简体中文译文：修正办法 |
|---|---|---|---|---|
| 98 | ignored /ɪɡˈnɔːd/，过去分词：被忽略；output /ˈaʊtpʊt/，名词：输出 | `q=0`，且 `-q:v` 被忽略 | 输出格式是 `.png` | 使用 `.jpg`。 |
| 99 | black /blæk/，形容词：黑色的；seek /siːk/，名词：定位；placement /ˈpleɪsmənt/，名词：放置位置；accuracy /ˈækjərəsi/，名词：精度 | 开头出现黑帧 | `-ss` 的放置位置影响定位 | 为提高精度，将 `-ss` 移到 `-i` 后面；或按原文建议使用 `-noaccurate_seek`。 |
| 100 | permission /pəˈmɪʃən/，名词：权限；denied /dɪˈnaɪd/，过去分词：被拒绝；missing /ˈmɪsɪŋ/，形容词：缺失的 | 写帧时提示 `Permission denied`，即“权限被拒绝” | 目录不存在 | 先执行 `New-Item -ItemType Directory -Force`。 |
| 101 | off /ɒf/，副词：偏离；input seek /ˈɪnpʊt siːk/：输入侧定位；output seek /ˈaʊtpʊt siːk/：输出侧定位 | 帧时间偏差约 1 秒 | 输入侧定位与输出侧定位的差异 | 按原文建议加入 `-noaccurate_seek`，或把 `-ss` 移到 `-i` 后面。 |
| 102 | silent /ˈsaɪlənt/，形容词：无声的；audio stream /ˈɔːdiəʊ striːm/，名词短语：音频流；skip /skɪp/，动词：跳过 | 导出的音频无声 | 没有音频流 | 检查 `ffprobe -show_streams`；如果没有 `codec_type: audio`，则跳过音频分析。 |
| 103 | fixed /fɪkst/，形容词：固定的；pattern /ˈpætən/，名词：命名模式；multiple /ˈmʌltɪpəl/，形容词：多个的 | 网格只显示前 16 帧 | 平铺网格固定为 4×4 | 使用 `grid_%03d.jpg` 命名模式，输出多张图。 |
| 104 | path /pɑːθ/，名词：路径；space /speɪs/，名词：空格；quote /kwəʊt/，名词或动词：引号、加引号 | 含空格的路径运行失败 | 缺少引号 | 始终为完整路径加上引号。 |

**词汇与术语**

- diagnose /ˈdaɪəɡnəʊz/，动词：诊断；permission /pəˈmɪʃən/，名词：权限；verify /ˈverɪfaɪ/，动词：核实。

**简体中文译文（译注）**

故障表是源文的经验性对照，不能据单一报错确定唯一原因。例如“权限被拒绝”也可能确实涉及写入权限；音频无声也不必然等于没有音轨。第 99、101 行的 `-noaccurate_seek` 建议应结合第 4 节译注理解，并对实际抽出的时间点进行核对。
