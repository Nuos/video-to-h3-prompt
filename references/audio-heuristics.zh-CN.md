# H3 提示词的音频分析判据｜简体中文逐段释义版

> 对应源文件：[audio-heuristics.md](audio-heuristics.md)。源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。
> 本文是阅读用译本，按源文顺序先释义再翻译；不替代运行配置、英文提示词模板或原始技能入口。命令、字段键、标签及路径保持原写法，中文解释说明其含义。音标采用常见英式或美式读法；标识符按构成词解释，不杜撰整个标识符的读音。译注只指出源文歧义，不修改原规则。


### 译段 01（源文第 1 行）

**词汇与术语**

audio /ˈɔːdiəʊ/（n./adj.）音频；heuristic /hjʊəˈrɪstɪk/（n.，此处复数 heuristics）启发式判据，即用于初步判断的经验规则；prompt /prɒmpt/（n.）提示词。

**简体中文译文**

H3 提示词的音频分析判据。


### 译段 02（源文第 3 行）

**词汇与术语**

layer /ˈleɪə/（n.）层；forensic /fəˈrensɪk/（adj.）基于证据进行分析的；classification /ˌklæsɪfɪˈkeɪʃən/（n.）分类；track /træk/（n.）音轨；energy peak /ˈenədʒi piːk/（名词短语）能量峰；loudness /ˈlaʊdnəs/（n.）响度；recipe /ˈresəpi/（n.）配方，此处指音乐描述模板；mapping /ˈmæpɪŋ/（n.）映射；diegetic /ˌdaɪəˈdʒetɪk/（adj.）属于故事世界、可由场内人物听见的；`non_diegetic_music`（字段键）非叙事内音乐，即面向观众的配乐；field audio /fiːld ˈɔːdiəʊ/（名词短语）现场录音。

**简体中文译文**

音频分析分为两层：**（A）取证分类**——音轨究竟有没有音乐，以及能量峰出现在何处；**（B）响度→描述模板映射**——在确实存在音乐时，怎样填写 `non_diegetic_music`。先执行 A，再执行 B；如果音轨实际上只有现场录音，就不要为它编写音乐描述模板。


## A. 取证分类：先完成这一层


### 译段 03（源文第 5–7 行）

**词汇与术语**

forensic classification /fəˈrensɪk ˌklæsɪfɪˈkeɪʃən/（名词短语）取证分类；spectrogram /ˈspektrəɡræm/（n.）声谱图；versus /ˈvɜːsəs/（prep.，缩写 vs）与……相对、比较；music /ˈmjuːzɪk/（n.）音乐；field audio /fiːld ˈɔːdiəʊ/（名词短语）现场录音。

**简体中文译文**

A. 取证分类（先做这一步）。

A1. 声谱图——区分音乐与现场录音。


### 译段 04（源文第 9–12 行）

**词汇与术语**

`ffmpeg`（工具名）音视频处理程序；`-y` 覆盖输出；`-i` 指定输入；`-vn` 不输出视频；`-ac 1` 输出单声道；`-ar 22050` 采样率为 22050 Hz；`-lavfi` 指定滤镜图；spectrum /ˈspektrəm/（n.）频谱；legend /ˈledʒənd/（n.）图例；`showspectrumpic`（滤镜名）输出声谱图，`s=1000x400` 为图像尺寸，`legend=1` 开启图例；WAV /wæv/（文件格式名称）波形音频格式。

**简体中文译文**

先从 `IN.mp4` 提取单声道、22050 Hz 的 `audio.wav`；再生成尺寸为 1000×400、带图例的声谱图 `spectrum.jpg`。

命令原样保留：

```powershell
ffmpeg -y -i "IN.mp4" -vn -ac 1 -ar 22050 audio.wav
ffmpeg -y -i audio.wav -lavfi showspectrumpic=s=1000x400:legend=1 spectrum.jpg
```


### 译段 05（源文第 14 行）

**词汇与术语**

evenly spaced /ˈiːvənli speɪst/（形容词短语）等间距的；low-frequency /ˌləʊ ˈfriːkwənsi/（adj.）低频的；vertical stripe /ˈvɜːtɪkəl straɪp/（名词短语）竖直条纹；drum machine /drʌm məˈʃiːn/（n.）鼓机；beat /biːt/（n.）节拍。

**简体中文译文**

贯穿整段片子的等间距低频竖条纹→鼓机／节拍，说明存在音乐。


### 译段 06（源文第 15 行）

**词汇与术语**

wide-band /ˈwaɪd bænd/（adj.）宽频带的；random /ˈrændəm/（adj.）随机的；harmonic /hɑːˈmɒnɪk/（adj.）谐波的；arc /ɑːk/（n.）弧线；speech /spiːtʃ/（n.）说话声；laugh /lɑːf/（n.）笑声；shout /ʃaʊt/（n.）叫喊声；Hz /hɜːts/（单位符号，hertz）赫兹；kHz（kilohertz，/ˈkɪləhɜːts/）千赫兹。

**简体中文译文**

宽频带随机能量，偶尔伴随上升的谐波弧线（约 800 Hz→3 kHz）→人声说话／笑声／叫喊。


### 译段 07（源文第 16 行）

**词汇与术语**

continuous /kənˈtɪnjuəs/（adj.）连续的；full-band /ˈfʊl bænd/（adj.）全频带的；low-level /ˌləʊ ˈlevəl/（adj.）低电平的；wash /wɒʃ/（n.）弥散、铺满背景的声层；ambient bed /ˈæmbiənt bed/（名词短语）环境底声；engine /ˈendʒɪn/（n.）发动机。

**简体中文译文**

连续的全频带低电平声层→环境底声，例如街道声、风声、发动机声。


### 译段 08（源文第 17 行）

**词汇与术语**

vertical bright column /ˈvɜːtɪkəl braɪt ˈkɒləm/（名词短语）竖直亮柱；freeze /friːz/（n.）定格；spray /spreɪ/（n.）喷射；transient /ˈtrænziənt/（adj./n.）瞬态的／瞬态声；SFX /ˌes ef ˈeks/（缩略语，sound effects /saʊnd ɪˈfekts/）音效；align /əˈlaɪn/（v.）对齐。

**简体中文译文**

定格／喷射时刻出现竖直亮柱→瞬态音效；应把它们与画面事件逐一对齐。


### 译段 09（源文第 19 行）

**词汇与术语**

RMS /ˌɑːr em ˈes/（缩略语，root mean square /ruːt miːn skweə/）均方根；envelope /ˈenvələʊp/（n.）包络；BPM /ˌbiː piː ˈem/（缩略语，beats per minute /biːts pə ˈmɪnɪt/）每分钟拍数；credibility /ˌkredəˈbɪləti/（n.）可信度。

**简体中文译文**

A2. 0.5 秒均方根包络与每分钟拍数的可信度。


### 译段 10（源文第 21–23 行）

**词汇与术语**

Python /ˈpaɪθən/（专有名词）Python 语言／解释器；probe /prəʊb/（n./v.）探测、检查；`scripts/audio_probe.py`（路径）音频探测脚本；`audio.wav` 为输入音频文件。

**简体中文译文**

运行音频探测脚本，检查输入 WAV 音频。

命令原样保留：

```powershell
python scripts/audio_probe.py audio.wav
```


### 译段 11（源文第 25 行）

**词汇与术语**

mark /mɑːk/（v.）标记；reconcile /ˈrekənsaɪl/（v.）对账、核对一致性；cause /kɔːz/（n.）成因；matrix /ˈmeɪtrɪks/（n.）矩阵；readout /ˈriːdaʊt/（n.）读数；trustworthy /ˈtrʌstwɜːði/（adj.）可信的；RMS（root mean square）均方根；BPM（beats per minute）每分钟拍数，读音分别为 /ˌɑːr em ˈes/、/ˌbiː piː ˈem/。

**简体中文译文**

标出每一个均方根能量峰，并核对它对应的画面成因，参见 `01-forensics-commands.md` 中的矩阵。只有以下条件**全部成立**时，每分钟拍数的读数才可信：


### 译段 12（源文第 27 行）

**词汇与术语**

onset /ˈɒnset/（n.）起音、音头；std（standard deviation /ˈstændəd ˌdiːviˈeɪʃən/ 的缩写）标准差；mean /miːn/（n.）均值；regular /ˈreɡjələ/（adj.）有规律的；beat /biːt/（n.）节拍。

**简体中文译文**

1. `onset std / onset mean < 0.8`，即起音间隔的标准差除以均值小于 0.8，表示节拍较有规律。


### 译段 13（源文第 28 行）

**词汇与术语**

spectrogram /ˈspektrəɡræm/（n.）声谱图；kick /kɪk/（n.）底鼓声；grid /ɡrɪd/（n.）网格，此处指规律排列的节拍条纹。

**简体中文译文**

2. 声谱图显示规律的底鼓网格。


### 译段 14（源文第 29 行）

**词汇与术语**

RMS /ˌɑːr em ˈes/（root mean square）均方根；cyclically /ˈsɪklɪkli/（adv.）周期性地；isolated /ˈaɪsəleɪtɪd/（adj.）孤立的；spike /spaɪk/（n.）尖峰。

**简体中文译文**

3. 均方根包络呈周期性的起伏，而不是孤立的尖峰。


### 译段 15（源文第 31 行）

**词汇与术语**

false detection /fɔːls dɪˈtekʃən/（名词短语）误检；random transient /ˈrændəm ˈtrænziənt/（名词短语）随机瞬态声；stable /ˈsteɪbəl/（adj.）稳定的；BGM /ˌbiː dʒiː ˈem/（缩略语，background music /ˈbækɡraʊnd ˈmjuːzɪk/）背景音乐；diegetic /ˌdaɪəˈdʒetɪk/（adj.）叙事内的；explicit silence /ɪkˈsplɪsɪt ˈsaɪləns/（名词短语）明确声明静音；N/A /ˌen ˈeɪ/（常用于 not applicable）不适用，此处表示不设置配乐。

**简体中文译文**

否则，这个每分钟拍数就是把随机瞬态声误识别为节拍的结果→结论写为**没有稳定的背景音乐，只有叙事内现场录音**，并把 `non_diegetic_music` 设为明确静音／`N/A`。


> **译注：** 这里忠实保留源文的推断。它与 `07-onset-and-card-points.md` 中“自由散板仍可能是音乐”的判别存在适用范围上的冲突；不能把本段译文误读为已经证明所有不规则节奏都没有音乐。


### 译段 16（源文第 33 行）

**词汇与术语**

dialogue /ˈdaɪəlɒɡ/（n.）对白；music /ˈmjuːzɪk/（n.）音乐；ambience /ˈæmbiəns/（n.）环境声／氛围；listen /ˈlɪsən/（v.）聆听。

**简体中文译文**

A3. 对白、音乐与环境声的区分（无法直接听音频时）。


### 译段 17（源文第 35 行）

**词汇与术语**

visible speech /ˈvɪzəbəl spiːtʃ/（名词短语）画面可见的讲话行为；gesture /ˈdʒestʃə/（v.）打手势；mic /maɪk/（microphone /ˈmaɪkrəfəʊn/ 的简称，n.）麦克风；dialogue /ˈdaɪəlɒɡ/（n.）对白；language /ˈlæŋɡwɪdʒ/（n.）语言；text /tekst/（n.）文本；timeline /ˈtaɪmlaɪn/（n.）时间轴；`<d>…</d>`（标记）对白包装标签。

**简体中文译文**

**画面可见的讲话行为**，例如张嘴、打手势、麦克风入画→对白；在时间轴中用 `<d>[Language] text</d>` 包裹，其中 `[Language]` 填语言，`text` 填对白文本；音乐保持低音量或设为 `N/A`。


### 译段 18（源文第 36 行）

**词汇与术语**

synchronized /ˈsɪŋkrənaɪzd/（adj.）同步的；dance /dɑːns/（n.）舞蹈；coordinated movement /kəʊˈɔːdɪneɪtɪd ˈmuːvmənt/（名词短语）协调一致的动作；expect /ɪkˈspekt/（v.）预计、推测存在；`non_diegetic_music`（字段）非叙事内配乐。

**简体中文译文**

**同步舞蹈／协调一致的动作**→预计存在音乐；在 `non_diegetic_music` 中描述它。


### 译段 19（源文第 37 行）

**词汇与术语**

empty scene /ˈempti siːn/（名词短语）空场景；talking head /ˈtɔːkɪŋ hed/（名词短语）人物对镜头讲话的画面；prank /præŋk/（n.）恶作剧；ambience /ˈæmbiəns/（n.）环境声；underscore /ˈʌndəskɔː/（n.）衬底配乐；at most /ət məʊst/（副词短语）最多。

**简体中文译文**

**空场景／人物对镜讲话／安静的恶作剧**→最多配置环境声加轻微的衬底配乐。


> **译注：** 源文用画面类型提供推测线索；同一文档开头又要求先确认是否有音乐，故本项不应代替音轨取证。


### 译段 20（源文第 38 行）

**词汇与术语**

off-camera /ˌɒf ˈkæmərə/（adj.）画外的；interact /ˌɪntərˈækt/（v.）互动；isolated spike /ˈaɪsəleɪtɪd spaɪk/（名词短语）孤立尖峰；pouring /ˈpɔːrɪŋ/（n.）倾倒；spray /spreɪ/（n.）喷射；choke /tʃəʊk/（n./v.）呛咳；laughter /ˈlɑːftə/（n.）笑声；kick grid /kɪk ɡrɪd/（名词短语）底鼓节拍网格。

**简体中文译文**

一条从画外伸入的手臂与人物互动，同时均方根包络只有孤立尖峰、没有底鼓网格→现场录音，例如倾倒、喷射、呛咳、笑声，**不是音乐**。


## B. 响度与音乐描述模板的对应关系


### 译段 21（源文第 40 行）

**词汇与术语**

loudness /ˈlaʊdnəs/（n.）响度；recipe /ˈresəpi/（n.）描述配方／模板；mapping /ˈmæpɪŋ/（n.）映射；volume /ˈvɒljuːm/（n.）音量；detect /dɪˈtekt/（v.）检测；`volumedetect`（滤镜名）音量统计滤镜。

**简体中文译文**

B. 响度→音乐描述模板映射（使用 `volumedetect`）。


### 译段 22（源文第 42–46 行）

**词汇与术语**

`-ar 8000` 设采样率为 8000 Hz；`-f wav` 指定 WAV 格式；`-af` 指定音频滤镜；`-f null` 使用空输出；`NUL` 为 Windows 空设备；`2>&1` 将标准错误合并到标准输出；Select /sɪˈlekt/（v.）选择；String /strɪŋ/（n.）字符串；`Select-String volume` 筛选含 volume（音量）的行；`grep volume` 是 Bash 示例中的对应文本筛选；PowerShell /ˈpaʊəʃel/、Bash /bæʃ/ 为命令行环境名称。

**简体中文译文**

将视频中的声音转为单声道 8000 Hz WAV 文件，再统计音量并筛出相关行。第一种写法用于 PowerShell；源文注释中的 `bash:` 意为“Bash 写法如下”。

命令原样保留：

```powershell
ffmpeg -y -i "IN.mp4" -vn -ac 1 -ar 8000 -f wav out8k.wav
ffmpeg -i out8k.wav -af "volumedetect" -f null NUL 2>&1 | Select-String volume   # PowerShell
# bash: ffmpeg -i out8k.wav -af volumedetect -f null - 2>&1 | grep volume
```


### 译段 23（源文第 48–51 行）

**词汇与术语**

metric /ˈmetrɪk/（n.）指标；meaning /ˈmiːnɪŋ/（n.）含义；mean /miːn/（n./adj.）平均值／平均的；max /mæks/（maximum /ˈmæksɪməm/ 的简称）最大值；volume /ˈvɒljuːm/（n.）音量；peak transient /piːk ˈtrænziənt/（名词短语）峰值瞬态；clipping /ˈklɪpɪŋ/（n.）削波；dB /ˌdiː ˈbiː/（decibel /ˈdesɪbel/，单位）分贝。

**简体中文译文**

| 指标 | 含义 |
|---|---|
| `mean_volume` | 整条音轨的平均响度。 |
| `max_volume` | 瞬态峰值；源文认为高于 −3 dB 有削波风险。 |


### 译段 24（源文第 53–55 行）

**词汇与术语**

likely /ˈlaɪkli/（adj.）可能的；content /ˈkɒntent/（n.）内容；club /klʌb/（n.）夜店；electronic /ɪˌlekˈtrɒnɪk/（adj.）电子的；EDM /ˌiː diː ˈem/（electronic dance music）电子舞曲；energetic /ˌenəˈdʒetɪk/（adj.）充满活力的；tempo /ˈtempəʊ/（n.）音乐速度；kick /kɪk/（n.）底鼓；layered /ˈleɪəd/（adj.）分层叠加的；synth /sɪnθ/（synthesizer /ˈsɪnθəsaɪzə/ 的简称，n.）合成器；lead /liːd/（n.）主旋律声部；side-chained /ˈsaɪd tʃeɪnd/（adj.）使用侧链处理的；bass /beɪs/（n.）低音。

**简体中文译文**

音乐模板表第一行：`mean_volume` 为 −8 至 −12 dB，`max_volume` 为 0 至 −2 dB；可能内容为响亮的夜店音乐／电子音乐／电子舞曲。

`non_diegetic_music` 译文：一首充满活力、速度较快的电子乐，具有厚重的底鼓、层层叠加的合成器主旋律和使用侧链处理的低音。


### 译段 25（源文第 56 行）

**词汇与术语**

pop /pɒp/（n.）流行乐；dance-pop /ˈdɑːns pɒp/（n.）舞曲流行乐；K-pop /ˈkeɪ pɒp/（Korean pop）韩国流行乐；bright /braɪt/（adj.）明亮的；moderate /ˈmɒdərət/（adj.）适中的；four-on-the-floor /ˌfɔː ɒn ðə ˈflɔː/（名词／定语短语）四拍中每拍都有底鼓的节奏；clap /klæp/（n.）拍手声；synth lead /sɪnθ liːd/（名词短语）合成器主旋律。

**简体中文译文**

`mean_volume` 为 −10 至 −15 dB，`max_volume` 为 −1 至 −3 dB；可能内容为流行乐／舞曲流行乐／韩国流行乐。

模板译文：一首明亮、速度适中的流行乐，带有合成器主旋律、每拍一下的四拍底鼓和清亮的拍手声。


### 译段 26（源文第 57 行）

**词汇与术语**

anime /ˈænɪmeɪ/（n.）日本动画；chiptune /ˈtʃɪptjuːn/（n.）芯片音乐；cute /kjuːt/（adj.）可爱的；Japanese-style /ˌdʒæpəˈniːz staɪl/（adj.）日式的；bouncy /ˈbaʊnsi/（adj.）轻快跳跃的；flourish /ˈflʌrɪʃ/（n.）装饰乐句；synth lead /sɪnθ liːd/（名词短语）合成器主旋律；four-on-the-floor /ˌfɔː ɒn ðə ˈflɔː/（节奏术语）四拍每拍一记底鼓。

**简体中文译文**

`mean_volume` 为 −13 至 −17 dB，`max_volume` 为 −3 至 −6 dB；可能内容为动画音乐／芯片音乐／可爱风流行乐。

模板译文：一首明亮的日式动画舞曲流行乐，速度适中，配有轻快跳跃的合成器主旋律、每拍一下的四拍底鼓，以及可爱的芯片音乐装饰乐句。


### 译段 27（源文第 58 行）

**词汇与术语**

live show /laɪv ʃəʊ/（名词短语）现场演出；restaurant /ˈrestrɒnt/（n.）餐馆；cafe /ˈkæfeɪ/（n.）咖啡馆；vlog /vlɒɡ/（video blog 的缩合词，n.）视频日志；backing track /ˈbækɪŋ træk/（名词短语）伴奏；relaxed /rɪˈlækst/（adj.）舒缓的；acoustic guitar /əˈkuːstɪk ɡɪˈtɑː/（名词短语）原声吉他；arpeggio /ɑːˈpedʒiəʊ/（n.）琶音；brushed snare /brʌʃt sneə/（名词短语）刷奏小军鼓；subtle /ˈsʌtəl/（adj.）轻微、不突出的；piano lead /piˈænəʊ liːd/（名词短语）钢琴主旋律。

**简体中文译文**

`mean_volume` 为 −16 至 −20 dB，`max_volume` 为 −5 至 −8 dB；可能内容为现场演出／餐馆／咖啡馆视频日志。

模板译文：一首温暖的轻流行伴奏，速度舒缓，具有柔和的原声吉他琶音、轻柔的刷奏小军鼓和若隐若现的钢琴主旋律。


### 译段 28（源文第 59 行）

**词汇与术语**

cinematic /ˌsɪnəˈmætɪk/（adj.）电影式的；score /skɔː/（n.）配乐；underscore /ˈʌndəskɔː/（n.）衬底配乐；restrained /rɪˈstreɪnd/（adj.）克制的；orchestral /ɔːˈkestrəl/（adj.）管弦乐的；sustained /səˈsteɪnd/（adj.）持续的；low strings /ləʊ strɪŋz/（名词短语）低音弦乐；swell /swel/（n.）渐强、音量膨胀。

**简体中文译文**

`mean_volume` 为 −20 至 −25 dB，`max_volume` 为 −8 至 −12 dB；可能内容为电影配乐／衬底配乐。

模板译文：一段克制、速度缓慢的管弦配乐，采用持续的低音弦乐，没有渐强。


### 译段 29（源文第 60 行）

**词汇与术语**

ambient /ˈæmbiənt/（adj.）氛围性的；drone /drəʊn/（n.）持续长音；nature /ˈneɪtʃə/（n.）自然；room tone /ruːm təʊn/（名词短语）空间底噪；melodic development /məˈlɒdɪk dɪˈveləpmənt/（名词短语）旋律发展。

**简体中文译文**

`mean_volume` 为 −25 至 −35 dB，`max_volume` 为 −12 至 −18 dB；可能内容为氛围持续音／自然声。

模板译文：安静的氛围持续长音，伴随柔和的空间底噪，没有旋律发展。


### 译段 30（源文第 61 行）

**词汇与术语**

near-silent /ˌnɪə ˈsaɪlənt/（adj.）接近无声的；N/A /ˌen ˈeɪ/（not applicable）不适用，此处不设置配乐。

**简体中文译文**

`mean_volume < −35 dB`，`max_volume < −18 dB`；可能内容为接近无声；`non_diegetic_music` 填 `N/A`。


> **译注：** 这一整组响度到类型的对应关系是源文的经验模板，并非对具体输入音轨已经完成的分类结果；本译本完整保留其数字与顺序。


## 整体声景的描述模板


### 译段 31（源文第 63–66 行）

**词汇与术语**

overall /ˌəʊvərˈɔːl/（adj.）整体的；soundscape /ˈsaʊndskeɪp/（n.）声景；recipe /ˈresəpi/（n.）模板；venue /ˈvenjuː/（n.）场所；template /ˈtempleɪt/（n.）模板；`overall_soundscape`（字段键）整体声景。

**简体中文译文**

`overall_soundscape` 的描述模板。原表按“场所→模板”排列如下。


### 译段 32（源文第 67 行）

**词汇与术语**

indoor /ˈɪndɔː/（adj.）室内的；restaurant /ˈrestrɒnt/（n.）餐馆；cafe /ˈkæfeɪ/（n.）咖啡馆；type /taɪp/（n.）类型；faint /feɪnt/（adj.）微弱的；ceiling fan /ˈsiːlɪŋ fæn/（n.）吊扇；hum /hʌm/（n.）嗡嗡声；muffled /ˈmʌfəld/（adj.）闷沉的；clatter /ˈklætə/（n.）碗碟等碰撞的咔嗒声；neighboring /ˈneɪbərɪŋ/（adj.）相邻的；distant /ˈdɪstənt/（adj.）远处的；shout /ʃaʊt/（n.）叫喊。

**简体中文译文**

**场所：室内餐馆／咖啡馆。** 模板：柔和的室内 `<type>`（类型）环境声充满空间：微弱的吊扇嗡嗡声、邻桌传来闷沉的碗碟碰撞声，以及厨房远处一声短促的叫喊。


### 译段 33（源文第 68 行）

**词汇与术语**

outdoor /ˈaʊtdɔː/（adj.）室外的；urban /ˈɜːbən/（adj.）城市的；steady /ˈstedi/（adj.）持续稳定的；alley /ˈæli/（n.）巷子；traffic hum /ˈtræfɪk hʌm/（名词短语）交通嗡鸣；scooter /ˈskuːtə/（n.）踏板车；idle /ˈaɪdəl/（n./adj.）怠速／怠速的；vibration /vaɪˈbreɪʃən/（n.）振动；damp /dæmp/（adj.）潮湿的；pavement /ˈpeɪvmənt/（n.）路面；room tone /ruːm təʊn/（名词短语）空间底噪。

**简体中文译文**

**场所：城市户外夜景。** 模板：持续的夜间小巷环境声：远处的交通嗡鸣、轻微的踏板车怠速振动，以及潮湿路面的环境底声。


> **译注：** 源文把“潮湿路面”与 room tone 连用，是描述氛围的写法；译文保留其意，不补写未说明的实际发声机制。


### 译段 34（源文第 69 行）

**词汇与术语**

concert /ˈkɒnsət/（n.）音乐会；club /klʌb/（n.）夜店；live performance /laɪv pəˈfɔːməns/（名词短语）现场演出；crowd murmur /kraʊd ˈmɜːmə/（名词短语）人群低语；beneath /bɪˈniːθ/（prep.）在……之下，此处指音量低于音乐。

**简体中文译文**

**场所：音乐会／夜店。** 模板：现场演出的环境声，音乐下方铺着轻柔的人群低语。


### 译段 35（源文第 70 行）

**词汇与术语**

quiet room /ˈkwaɪət ruːm/（名词短语）安静房间；room tone /ruːm təʊn/（名词短语）空间底噪；soft /sɒft/（adj.）柔和的；ambient detail /ˈæmbiənt ˈdiːteɪl/（名词短语）环境声细节。

**简体中文译文**

**场所：安静房间。** 模板：安静的空间底噪，带有柔和的环境声细节。


### 译段 36（源文第 71 行）

**词汇与术语**

forest /ˈfɒrɪst/（n.）森林；nature /ˈneɪtʃə/（n.）自然；birdsong /ˈbɜːdsɒŋ/（n.）鸟鸣；breeze /briːz/（n.）微风；filter through /ˈfɪltə θruː/（动词短语）穿过、透过；leaves /liːvz/（leaf 的复数，n.）树叶。

**简体中文译文**

**场所：森林／自然环境。** 模板：鸟鸣和轻柔的微风穿过树叶。


### 译段 37（源文第 73–76 行）

**词汇与术语**

diegetic /ˌdaɪəˈdʒetɪk/（adj.）叙事内的；action sound /ˈækʃən saʊnd/（名词短语）动作声；visible action /ˈvɪzəbəl ˈækʃən/（名词短语）可见动作；add /æd/（v.）添加；line /laɪn/（n.）一句文本。

**简体中文译文**

为每个可见动作添加一项**叙事内动作声**。原表两列为“可见动作”和“补充这句话”。


### 译段 38（源文第 77 行）

**词汇与术语**

pour /pɔː/（v.）倾倒；liquid /ˈlɪkwɪd/（n.）液体；foot /fʊt/（n.）脚；ground /ɡraʊnd/（n.）地面；audible /ˈɔːdəbəl/（adj.）可听见的；wet patch /wet pætʃ/（名词短语）湿斑；spread /spred/（v.）扩散。

**简体中文译文**

**动作：把液体倒在脚上／地面。** 补充：能听见倒水声，一块深色湿斑正在扩散。


### 译段 39（源文第 78 行）

**词汇与术语**

hit /hɪt/（v.）击中；plastic /ˈplæstɪk/（adj.）塑料的；visor /ˈvaɪzə/（n.）面罩；wet splat /wet splæt/（名词短语）湿润的啪嗒撞击声／喷溅；burst /bɜːst/（v.）迸开；across /əˈkrɒs/（prep.）遍及、横过。

**简体中文译文**

**动作：液体打在塑料面罩上。** 补充：伴随湿润的“啪”一声，液体在塑料面罩上迸溅开。


### 译段 40（源文第 79 行）

**词汇与术语**

spin /spɪn/（v.）旋转；turn /tɜːn/（v.）转身；costume /ˈkɒstjuːm/（n.）服装；fabric /ˈfæbrɪk/（n.）布料；rustle /ˈrʌsəl/（v.）发出沙沙声；softly /ˈsɒftli/（adv.）轻柔地；Subject /ˈsʌbdʒɪkt/（n.）主体，`<Subject 1>` 是固定引用标签。

**简体中文译文**

**动作：旋转／转身。** 补充：`<Subject 1>` 转身时，服装布料发出轻微的沙沙声。


### 译段 41（源文第 80 行）

**词汇与术语**

walk /wɔːk/（v.）走路；wet ground /wet ɡraʊnd/（名词短语）湿地面；footstep /ˈfʊtstep/（n.）脚步；splash /splæʃ/（n.）溅水声；heel /hiːl/（n.）脚跟／鞋跟。

**简体中文译文**

**动作：在湿地面行走。** 补充：鞋跟下传来轻微的脚步溅水声。


### 译段 42（源文第 81 行）

**词汇与术语**

choke /tʃəʊk/（v.）呛到；sip /sɪp/（n.）一小口；cough /kɒf/（n.）咳嗽；spit /spɪt/（n./v.）吐出；spurt /spɜːt/（v.）喷出；lip /lɪp/（n.）嘴唇；cough-spit（源文组合写法）边呛咳边喷吐。

**简体中文译文**

**动作：喝一口后呛到。** 补充：一声呛咳伴随喷吐，水从嘴唇间喷出。


### 译段 43（源文第 82 行）

**词汇与术语**

freeze-frame /ˈfriːz freɪm/（n.）定格；gag /ɡæɡ/（n.）喜剧桥段；record scratch /ˈrekɔːd skrætʃ/（名词短语）唱片刮擦；squeal /skwiːl/（n.）尖叫般的刺耳声；punchy /ˈpʌntʃi/（adj.）有冲击力的；impact hit /ˈɪmpækt hɪt/（名词短语）冲击音；half-second /ˌhɑːf ˈsekənd/（n./adj.）半秒／半秒的；near-silence /ˌnɪə ˈsaɪləns/（n.）近乎静音；ambient snap-back /ˈæmbiənt ˈsnæp bæk/（名词短语）环境声突然恢复。

**简体中文译文**

**动作：定格笑点。** 补充：刺耳的唱片刮擦声→有力的冲击音→半秒近乎静音→环境声骤然恢复。参见 `03-edit-effects.md`。


## 源片静音或只有现场录音时


### 译段 44（源文第 84–86 行）

**词汇与术语**

silent /ˈsaɪlənt/（adj.）无声的；pure /pjʊə/（adj.）纯粹的；field audio /fiːld ˈɔːdiəʊ/（名词短语）现场录音；non-diegetic /ˌnɒn daɪəˈdʒetɪk/（adj.）非叙事内的；explicit /ɪkˈsplɪsɪt/（adj.）明确的；throughout /θruːˈaʊt/（adv.）贯穿全程；soundtrack /ˈsaʊndtræk/（n.）音轨；comedic /kəˈmiːdɪk/（adj.）喜剧性的；sonic detail /ˈsɒnɪk ˈdiːteɪl/（名词短语）声音细节；SFX /ˌes ef ˈeks/（sound effects）音效；`overall_soundscape` 为整体声景字段。

**简体中文译文**

源片静音或只有现场录音时，设置 `non_diegetic_music: N/A`。

14 字段格式中的完整句子译为：**没有非叙事内配乐。整个片子的音乐层明确保持静音；音轨仅由叙事内现场录音以及定格喜剧音效的冲击声组成。**

将**所有**声音细节放入 `overall_soundscape`。


## 禁止事项


### 译段 45（源文第 88–90 行）

**词汇与术语**

Do not /duː nɒt/（否定祈使结构）不要／禁止；name /neɪm/（v.）点名、写出名称；song /sɒŋ/（n.）歌曲；artist /ˈɑːtɪst/（n.）艺人；copyrighted /ˈkɒpiraɪtɪd/（adj.）受版权保护的；score /skɔː/（n.）配乐；transcribe /trænˈskraɪb/（v.）转写；lyrics /ˈlɪrɪks/（n.，复数）歌词。

**简体中文译文**

禁止事项：不要写出歌曲、艺人或受版权保护的配乐名称；不要转写歌词。


### 译段 46（源文第 91 行）

**词汇与术语**

mix /mɪks/（v.）混在一起；music /ˈmjuːzɪk/（n.）音乐；ambience /ˈæmbiəns/（n.）环境声；block /blɒk/（n.）文本块；field /fiːld/（n.）字段。

**简体中文译文**

不要把音乐与环境声混在同一个文本块；分别放入各自的字段。


### 译段 47（源文第 92 行）

**词汇与术语**

louder /ˈlaʊdə/（loud 的比较级）更响的；original /əˈrɪdʒənəl/（n.）原片；scale up /skeɪl ʌp/（动词短语）放大、提高；automatically /ˌɔːtəˈmætɪkli/（adv.）自动地。

**简体中文译文**

不要把音乐写得比原片更响——源文称 H3 会自动把音乐放大。


> **译注：** “H3 会自动放大音乐”属于源作者的描述，本译本未另行验证这一行为。


### 译段 48（源文第 93 行）

**词汇与术语**

trust /trʌst/（v.）信任；BPM /ˌbiː piː ˈem/（beats per minute）每分钟拍数；condition /kənˈdɪʃən/（n.）条件；check /tʃek/（n.）核查。

**简体中文译文**

未通过 A2 的三项条件检查时，不要相信每分钟拍数这一数字。
