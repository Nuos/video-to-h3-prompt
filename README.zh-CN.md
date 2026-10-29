# video-to-h3-prompt：逐段词汇释义与简体中文译文

源文件：[`README.md`](README.md)；源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。本译本按原文顺序完整呈现说明、列表、目录和示例。每一语义段先释义，再翻译；文件名、命令、字段和引用标签保留原样。音标采用国际音标（IPA）；`n.`＝名词，`v.`＝动词，`adj.`＝形容词，`adv.`＝副词，`phr.`＝短语。代码或产品标识不擅自虚构固定读音。完整译本目录见 [`TRANSLATIONS.zh-CN.md`](TRANSLATIONS.zh-CN.md)。

## 1. 项目名称与概述（原文第 1–3 行）

**词汇与术语**

- **video** /ˈvɪdioʊ/，n.：视频；项目名 `video-to-h3-prompt` 的含义是“视频转 H3 提示词”。
- **prompt** /prɑːmpt/，n.：提示词、给生成模型的任务说明。
- **forensically** /fəˈrenzɪkli/，adv.：以取证分析的方式，即依据可核验的音视频证据。
- **reverse-engineer** /rɪˌvɜːrs endʒɪˈnɪr/，v.：逆向分析，从成品倒推生成它的结构和过程。
- **reference** /ˈrefərəns/，n./adj.：参考、参考用的。
- **ready-to-paste** /ˌredi tə ˈpeɪst/，adj. phr.：可以直接粘贴使用的。
- **vibe** /vaɪb/，n.，口语：氛围、总体感觉。
- **evidence pipeline** /ˈevɪdəns ˈpaɪplaɪn/，n. phr.：证据处理流程。
- **reconstruct / causal event chain** /ˌriːkənˈstrʌkt/、/ˈkɔːzəl ɪˈvent tʃeɪn/，v.／n. phr.：重建／因果事件链。
- **triage** /triːˈɑːʒ/，v.：分类分流；这里指按片型选择处理机制。
- **camera state machine** /ˈkæmərə steɪt məˈʃiːn/，n. phr.：相机状态机，用状态及切换条件组织镜头。
- **reconcile** /ˈrekənsaɪl/，v.：核对、使彼此吻合。
- **cut / onset** /kʌt/、/ˈɑːnset/，n.：切镜／音头，即声音事件的起始时刻。
- **live action / edit-effects / sound layer** /laɪv ˈækʃən/、/ˈedɪt ɪˈfekts/、/saʊnd ˈleɪər/，n. phr.：现场实拍动作／剪辑特效／声音层。
- **compile / field / input mode** /kəmˈpaɪl/、/fiːld/、/ˈɪnpʊt moʊd/，v./n./n. phr.：编排／字段／输入模式。

**简体中文译文**

本项目把参考视频通过取证式逆向分析，转化为完整、可直接粘贴的 **MiniMax H3 提示词**。这一过程并非“看几帧就写一段氛围描述”，而是一套证据处理流程：重建因果事件链，根据片型选择合适的相机状态机，将切镜与音乐音头逐一对账，分离现场动作、相机运动、剪辑特效和声音各层，并为每种输入模式准确编排 H3 所需字段。

## 2. 项目功能（原文第 5–14 行）

### 2.1 密集帧取证（第 7 行）

**词汇与术语**

- **What it does** /wʌt ɪt dʌz/，标题短语：它能做什么，即“项目功能”。
- **dense frame forensics** /dens freɪm fəˈrenzɪks/，n. phr.：密集视频帧取证分析。
- **sparse / contact sheet / skeleton** /spɑːrs/、/ˈkɑːntækt ʃiːt/、/ˈskelɪtən/，adj./n. phr./n.：稀疏的／缩略帧接触印样式拼图／结构骨架。
- **fps** /ˌef piː ˈes/：缩略语，frames per second，每秒帧数；这里指抽帧密度。
- **extraction / ambiguous window** /ɪkˈstrækʃən/、/æmˈbɪɡjuəs ˈwɪndoʊ/，n.／n. phr.：提取／存在歧义的时间区间。
- **adjudicate / competing hypothesis** /əˈdʒuːdɪkeɪt/、/kəmˈpiːtɪŋ haɪˈpɑːθəsɪs/，v.／n. phr.：裁决／相互竞争的解释假设。
- **plot / full-res / key frame** /plɑːt/、/fʊl rez/、/kiː freɪm/，n./缩略表达/n. phr.：剧情／full resolution（全分辨率）／关键帧。
- **timecode-burned sheet** /ˈtaɪmkoʊd bɜːrnd ʃiːt/，n. phr.：将时间码直接叠印在画面上的帧拼图。

**简体中文译文**

**密集帧取证**：用稀疏采样的帧拼图建立结构骨架；对有歧义的时间区间按每秒 4–8 帧密集抽取，以裁决相互竞争的剧情或相机解释；最终用原分辨率关键帧和叠印时间码的帧拼图进行确认。

### 2.2 片型与相机状态机分流（第 8 行）

**词汇与术语**

- **film type / triage** /fɪlm taɪp/、/triːˈɑːʒ/，n. phr./n.：片型／分类分流。
- **continuous take** /kənˈtɪnjuəs teɪk/，n. phr.：连续长镜头、一镜到底。
- **editorial snap-lock** /ˌedɪˈtɔːriəl snæp lɑːk/，n. phr.：原文对编辑式快照的命名，指短促重构图后立即锁定静止。
- **HARD LOCK / INSTANT BURST** /hɑːrd lɑːk/、/ˈɪnstənt bɜːrst/，状态标签：硬锁定／瞬时爆发。
- **mutually exclusive** /ˈmjuːtʃuəli ɪkˈskluːsɪv/，adj. phr.：相互排斥、不能同时成立的。
- **multi-shot montage** /ˈmʌlti ʃɑːt mɑːnˈtɑːʒ/，n. phr.：多镜头蒙太奇；此处指多镜头快剪。
- **named camera setup / cut discipline** /neɪmd ˈkæmərə ˈsetʌp/、/kʌt ˈdɪsəplɪn/，n. phr.：具名机位／切镜规范。
- **suppress / static hero frame / drift** /səˈpres/、/ˈstætɪk ˈhɪroʊ freɪm/、/drɪft/，v./n. phr./v.：压制／突出主体的静态展示画面／漂移。

**简体中文译文**

**片型→相机状态机分流**：将每个片段归为三类之一：（A）连续长镜头；（B）编辑式快照锁定，采用 `HARD LOCK ↔ INSTANT BURST`，即“硬锁定↔瞬时爆发”两个互斥状态；（C）多镜头蒙太奇快剪，采用具名机位与切镜规范。这样可以避免错误使用锁定／爆发模板来压制真实切镜，也能避免本应静止的主体展示画面发生漂移。

### 2.3 音乐音头与卡点同步（第 9 行）

**词汇与术语**

- **music onset** /ˈmjuːzɪk ˈɑːnset/，n. phr.：音乐音头。
- **card-point sync** /kɑːrd pɔɪnt sɪŋk/，n. phr.：原文用语，指卡点同步；**sync** 是 synchronization /ˌsɪŋkrənəˈzeɪʃən/ 的简称。
- **RMS** /ˌɑːr em ˈes/：root mean square /ruːt miːn skwer/ 的缩写，均方根；用于衡量信号幅度。
- **envelope** /ˈenvəloʊp/，n.：包络，显示能量随时间的总体起伏。
- **graded note onset** /ˈɡreɪdɪd noʊt ˈɑːnset/，n. phr.：按强弱分级的音符起始点。
- **freeze / impact / volley / aura-burst** /friːz/、/ˈɪmpækt/、/ˈvɑːli/、/ˈɔːrə bɜːrst/，n.：定格／冲击／齐射或一轮连射／能量光环爆发。
- **strong accent** /strɔːŋ ˈæksent/，n. phr.：强重音。
- **fixed tempo / free-tempo rubato** /fɪkst ˈtempoʊ/、/friː ˈtempoʊ ruːˈbɑːtoʊ/，n. phr.：固定速度／自由速度的弹性节奏或自由散板。
- **BPM** /ˌbiː piː ˈem/：beats per minute，每分钟拍数。
- **muzzle flash / explosion / false cut** /ˈmʌzəl flæʃ/、/ɪkˈsploʊʒən/、/fɔːls kʌt/，n. phr./n./n. phr.：枪口火光／爆炸／被错误检测为切镜的变化。
- **numpy / scipy / librosa**：软件包标识，原样保留；其中 **numerical** /nuːˈmerɪkəl/（adj.，数值的）、**scientific** /ˌsaɪənˈtɪfɪk/（adj.，科学的）有助于理解前两者的数值计算用途。

**简体中文译文**

**音乐音头／卡点同步**：除 0.5 秒均方根能量包络外，`onset_probe.py` 还会检测分级音符起始点，只依赖 numpy 和 scipy，不需要 librosa；它把每次切镜、定格、冲击、齐射和能量光环爆发与强重音核对，区分固定速度与自由速度的弹性节奏，避免虚构 BPM，并过滤枪口火光或爆炸造成的伪切镜。

### 2.4 因果事件链重建（第 10 行）

**词汇与术语**

- **causal / reconstruction** /ˈkɔːzəl/、/ˌriːkənˈstrʌkʃən/，adj./n.：因果的／重建。
- **trigger → action → reaction** /ˈtrɪɡər/ → /ˈækʃən/ → /riˈækʃən/，三个 n.：触发→行动→反应。
- **state change** /steɪt tʃeɪndʒ/，n. phr.：状态变化。
- **off-camera actor** /ɔːf ˈkæmərə ˈæktər/，n. phr.：画外行动者；不一定完整入镜，但参与因果过程。
- **sleeve / hand / scooter fairing** /sliːv/、/hænd/、/ˈskuːtər ˈferɪŋ/，n./n./n. phr.：袖子／手／踏板车导流罩。
- **track / agent / clutter** /træk/、/ˈeɪdʒənt/、/ˈklʌtər/，v./n./n.：追踪／行动主体／杂乱物件。

**简体中文译文**

**因果事件链重建**：对每次状态变化建立“触发→行动→反应”的关系；把仅以袖子、手或踏板车导流罩等线索出现的画外行动者作为真实参与者追踪，而不是把这些线索当作可忽略的杂物。

### 2.5 剪辑层分离（第 11 行）

**词汇与术语**

- **edit-layer separation** /ˈedɪt ˈleɪər ˌsepəˈreɪʃən/，n. phr.：剪辑层分离。
- **freeze-frame gag** /ˈfriːz freɪm ɡæɡ/，n. phr.：以定格制造的视觉笑料。
- **white flash / manga overlay** /waɪt flæʃ/、/ˈmæŋɡə ˈoʊvərleɪ/，n. phr.：白闪／漫画式叠加层。
- **RGB** /ˌɑːr dʒiː ˈbiː/：red /red/、green /ɡriːn/、blue /bluː/ 的首字母缩写，红、绿、蓝三通道。
- **glitch / energy burst** /ɡlɪtʃ/、/ˈenərdʒi bɜːrst/，n.／n. phr.：故障失真／能量爆发。
- **post-SFX** /poʊst ˌes ef ˈeks/：后期特效音；**SFX** 在此声音语境中指 sound effects /saʊnd ɪˈfekts/，而非另行引入的视觉特效软件。
- **editing / overall soundscape / on-set action** /ˈedɪtɪŋ/、/ˌoʊvərˈɔːl ˈsaʊndskeɪp/、/ɑːn set ˈækʃən/，n./n. phr./n. phr.：剪辑／整体声景／拍摄现场动作。

**简体中文译文**

**剪辑层分离**：定格笑料、白闪、漫画叠加、RGB 通道故障与能量爆发等效果，以及相应的后期特效音，应分别写入 `editing`（剪辑）或 `overall_soundscape`（整体声景），绝不能误写成拍摄现场发生的动作。

### 2.6 多图锁定与长片分段（第 12 行）

**词汇与术语**

- **multi-image locking / long-clip segmentation** /ˈmʌlti ˈɪmɪdʒ ˈlɑːkɪŋ/、/lɔːŋ klɪp ˌseɡmenˈteɪʃən/，n. phr.：多图锁定／长片段切分。
- **picture / character / identity / costume** /ˈpɪktʃər/、/ˈkærəktər/、/aɪˈdentəti/、/ˈkɑːstuːm/，n.：图片／角色／身份特征／服装。
- **environment / prop / appearance prose** /ɪnˈvaɪrənmənt/、/prɑːp/、/əˈpɪrəns proʊz/，n./n./n. phr.：环境／道具／外貌文字描述。
- **per-segment clock / non-restarting / hand-off state** /pər ˈseɡmənt klɑːk/、/nɑːn riːˈstɑːrtɪŋ/、/ˈhændɔːf steɪt/，n. phr./adj./n. phr.：各段独立计时／不重新开始的／衔接两段的交接状态。

**简体中文译文**

**多图锁定与长片分段**：`<Picture 1>` 锁定角色 1，`<Picture 2>` 锁定角色 2；图片只负责身份与服装，环境和道具仍用文字描述，正文不再书写外貌描述。超过约 15 秒的片段拆成多个段落，各段使用自己的计时，音乐连续而不重启，并明确前后段交接状态。

### 2.7 五种 H3 模式（第 13 行）

**词汇与术语**

- **mode / template / section / label discipline** /moʊd/、/ˈtempleɪt/、/ˈsekʃən/、/ˈleɪbəl ˈdɪsəplɪn/，n./n./n./n. phr.：模式／模板／章节／标签使用规范。
- **T2VA / I2VA / FL2VA / L2VA / Ref2VA**：模式标识，本文按仓库语境释为文本、首帧图像、首尾帧、尾帧、参考素材驱动的音视频生成；`2` 代表 **to** /tuː/，VA 对应 **video/audio** /ˈvɪdioʊ/ /ˈɔːdioʊ/。这是语义释义，不把未在本文件给出的英文展开宣称为官方命名。
- **text / image / first / last / reference** /tekst/、/ˈɪmɪdʒ/、/fɜːrst/、/læst/、/ˈrefərəns/，n./n./adj./adj./n.：文本／图像／首个／最后的／参考。
- **subject / picture / video / audio** /ˈsʌbdʒɪkt/、/ˈpɪktʃər/、/ˈvɪdioʊ/、/ˈɔːdioʊ/，n.：主体／图片／视频／音频；尖括号内的标签须原样保留。

**简体中文译文**

**覆盖全部五种 H3 模式**：T2VA、I2VA、FL2VA 和 L2VA 使用 14 字段模板；Ref2VA 使用六部分模板，并遵守 `<Subject>`、`<Picture>`、`<Video>`、`<Audio>` 标签规范。

### 2.8 保持剧情的角色替换（第 14 行）

**词汇与术语**

- **coser**：n.，角色扮演者的非正式称呼；源文未提供统一规范读音，本译本不另造音标。通行的对应词为 **cosplayer** /ˈkɑːzpleɪər/。
- **replacement / plot / swap / appearance** /rɪˈpleɪsmənt/、/plɑːt/、/swɑːp/、/əˈpɪrəns/，n./n./v./n.：替换／剧情／交换替换／外观。
- **action compatibility** /ˈækʃən kəmˌpætəˈbɪləti/，n. phr.：动作兼容性，即新角色及服饰能否支持原动作。
- **tier / prop inclusion** /tɪr/、/prɑːp ɪnˈkluːʒən/，v.／n. phr.：分级／道具是否纳入画面。
- **anime / real-human cosplay** /ˈænɪmeɪ/、/riːəl ˈhjuːmən ˈkɑːzpleɪ/，n.／n. phr.：动漫／真人角色扮演。
- **emit / table** /ɪˈmɪt/、/ˈteɪbəl/，v./n.：输出／表格。

**简体中文译文**

**不改变剧情的角色扮演者／角色替换**：只替换外观，执行动作兼容性检查，对道具入画实行分级，将动漫设计转译为真人角色扮演，并输出替换对照表。

## 3. 六条可复用检查（原文第 16–23 行）

### 3.1 先区分连续运动与离散切换（第 18 行）

**词汇与术语**

- **reusable check** /ˌriːˈjuːzəbəl tʃek/，n. phr.：可重复使用的检查项。
- **continuous move / discrete cut** /kənˈtɪnjuəs muːv/、/dɪˈskriːt kʌt/，n. phr.：连续运动／离散切镜。
- **dense-sample / transition / motion / fully still / step** /dens ˈsæmpəl/、/trænˈzɪʃən/、/ˈmoʊʃən/、/ˈfʊli stɪl/、/step/，v./n./n./adj. phr./n.：密集采样／转折区间／运动／完全静止／台阶式突变。
- **fps** /ˌef piː ˈes/：frames per second，每秒帧数。

**简体中文译文**

首先判断是连续运镜还是离散切镜；对转折区间按每秒至少 8 帧密集采样，寻找“运动→完全静止”的台阶式变化。

### 3.2 用音频核对时间轴（第 19 行）

**词汇与术语**

- **reconcile / timeline / audio** /ˈrekənsaɪl/、/ˈtaɪmlaɪn/、/ˈɔːdioʊ/，v./n./n.：核对／时间轴／音频。
- **cut / freeze / impact / onset** /kʌt/、/friːz/、/ˈɪmpækt/、/ˈɑːnset/，n.：切镜／定格／冲击／音头。
- **land on** /lænd ɑːn/，v. phr.：落在某个时间点上、对齐。
- **editorial / card-point editing / free camera timing** /ˌedɪˈtɔːriəl/、/kɑːrd pɔɪnt ˈedɪtɪŋ/、/friː ˈkæmərə ˈtaɪmɪŋ/，adj./n. phr./n. phr.：由剪辑形成的／卡点剪辑／相机运动自主的时间安排。

**简体中文译文**

用音频核对时间轴：每次切镜、定格或冲击是否落在音头上？若是，则属于编辑式或卡点剪辑；完成这一步判断后，再考虑相机运动是否采用自由的时间安排。

> 译注：原文 `only then` 没有明确写出“否”的分支；仓库 `SKILL.md` 第 22 行明确写作“否→才考虑自由运镜”。这里保留本文件的表述，并指出两处措辞差异。

### 3.3 参考图承担外观锁定（第 20 行）

**词汇与术语**

- **reference image / appearance / lock / looks** /ˈrefərəns ˈɪmɪdʒ/、/əˈpɪrəns/、/lɑːk/、/lʊks/，n. phr./n./v./复数 n.：参考图／外貌／锁定／外观。
- **prose / timing / state machine / environment / props** /proʊz/、/ˈtaɪmɪŋ/、/steɪt məˈʃiːn/、/ɪnˈvaɪrənmənt/、/prɑːps/，n.：文字描述／时间安排／状态机／环境／道具。

**简体中文译文**

有参考图时，不再描述外貌；图片负责锁定外观，文字只承担相机、时间、状态机、环境与道具的说明。

### 3.4 静态和爆发互斥（第 21 行）

**词汇与术语**

- **static / burst / mutually exclusive** /ˈstætɪk/、/bɜːrst/、/ˈmjuːtʃuəli ɪkˈskluːsɪv/，adj./n./adj. phr.：静态的／爆发／互斥的。
- **slow-mo** /ˈsloʊ moʊ/：slow motion /sloʊ ˈmoʊʃən/ 的口语缩写，慢动作。
- **drift / residual motion / ban** /drɪft/、/rɪˈzɪdʒuəl ˈmoʊʃən/、/bæn/，n./n. phr./n.：漂移／残余运动／禁止要求。

**简体中文译文**

把静态与爆发写成两个互斥状态；在所有静态段落中反复明确“禁止慢动作、漂移和残余运动”。

### 3.5 横置画面先核查相机滚转（第 22 行）

**词汇与术语**

- **sideways / suspect / Roll** /ˈsaɪdweɪz/、/səˈspekt/、/roʊl/，adv./v./n.：侧向或横置地／怀疑并优先检查／滚转，即相机绕光轴旋转。
- **horizon / body / declare / lying / turning** /həˈraɪzən/、/ˈbɑːdi/、/dɪˈkler/、/ˈlaɪɪŋ/、/ˈtɜːrnɪŋ/，n./n./v./现在分词：地平线／身体／判定／躺着或躺下／转动。

**简体中文译文**

画面横置时，首先怀疑相机滚转；在判定角色躺下或转身之前，先比较地平线与身体的相对关系。

### 3.6 冲击必须可数（第 23 行）

**词汇与术语**

- **countable / mushy** /ˈkaʊntəbəl/、/ˈmʌʃi/，adj.：可逐次计数的／模糊混成一团的。
- **hit / positional / push / rotational** /hɪt/、/pəˈzɪʃənəl/、/pʊʃ/、/roʊˈteɪʃənəl/，n./adj./n./adj.：冲击／位置变化的／前推／旋转的。
- **continuous vibration / deform** /kənˈtɪnjuəs vaɪˈbreɪʃən/、/dɪˈfɔːrm/，n. phr./v.：连续振动／使变形。

**简体中文译文**

冲击必须能逐次辨认，不能含混成一团：为每次冲击命名，说明它是位移、前推还是旋转，明确“不是连续振动”；只让相机受到冲击，不让人物变形。

## 4. 密集重建为何可行，以及初次判断为何容易出错（原文第 25–27 行）

**词汇与术语**

- **dense reconstruction / first pass** /dens ˌriːkənˈstrʌkʃən/、/fɜːrst pæs/，n. phr.：基于密集证据的重建／首轮处理或判断。
- **reverse-engineering / one-to-many inverse problem** /rɪˌvɜːrs endʒɪˈnɪrɪŋ/、/wʌn tə ˈmeni ˌɪnˈvɜːrs ˈprɑːbləm/，n.／n. phr.：逆向工程／一对多逆问题。
- **near-identical / sparse sampling / prior** /nɪr aɪˈdentɪkəl/、/spɑːrs ˈsæmplɪŋ/、/ˈpraɪər/，adj./n. phr./n.：几乎相同的／稀疏采样／先验假定。
- **helmet-grab redirect** /ˈhelmɪt ɡræb ˌriːdəˈrekt/，n. phr.：抓住头盔并改变朝向的动作。
- **spray / off-camera / candidate plot** /spreɪ/、/ɔːf ˈkæmərə/、/ˈkændɪdət plɑːt/，v./adj. phr./n. phr.：喷洒／画外的／候选剧情。
- **discriminative evidence** /dɪˈskrɪmɪnətɪv ˈevɪdəns/，n. phr.：判别性证据，用于区分相互竞争的解释。
- **user-supplied / actor list / intent chain** /ˈjuːzər səˈplaɪd/、/ˈæktər lɪst/、/ɪnˈtent tʃeɪn/，adj. phr./n. phr./n. phr.：用户提供的／行动者清单／意图链。
- **shrink / hypothesis space / verify / blindly** /ʃrɪŋk/、/haɪˈpɑːθəsɪs speɪs/、/ˈverɪfaɪ/、/ˈblaɪndli/，v./n. phr./v./adv.：缩小／假设空间／验证／盲目地。

**简体中文译文**

逆向工程是一个**一对多的逆问题**：不同脚本可以产生几乎相同的画面。稀疏采样再加上“最常见剧情”的先验，会在不知不觉间填补证据空白。例如，把“抓住头盔后改变方向”的动作误读为两个女孩相互喷洒，漏掉只出现 3–5 帧的画外人的手，或者把相机滚转误判为人物躺下。本技能在建立骨架阶段保留多个候选剧情，使用密集帧、状态机分流和音乐音头作为判别性证据。用户提供的剧情被视为行动者清单与意图链，用来缩小假设空间；随后仍须逐帧验证，既不盲目接受，也不盲目否定。

## 5. 目录结构（原文第 29–54 行）

**词汇与术语**

- **layout / workflow / channel** /ˈleɪaʊt/、/ˈwɜːrkfloʊ/、/ˈtʃænəl/，n.：结构布局／工作流／通道。
- **SOP** /ˌes oʊ ˈpiː/：standard operating procedure /ˈstændərd ˈɑːpəreɪtɪŋ prəˈsiːdʒər/ 的缩写，标准操作流程。
- **agent metadata** /ˈeɪdʒənt ˈmetədeɪtə/，n. phr.：智能体元数据。
- **sampling / grid / spectrogram / scene cut / timecode** /ˈsæmplɪŋ/、/ɡrɪd/、/ˈspektrəɡræm/、/siːn kʌt/、/ˈtaɪmkoʊd/，n.：采样／网格／声谱图／场景切换／时间码。
- **reconciliation matrix / field mapping** /ˌrekənsɪliˈeɪʃən ˈmeɪtrɪks/、/fiːld ˈmæpɪŋ/，n. phr.：对账矩阵／字段映射。
- **timestamp / EN / assembly skeleton** /ˈtaɪmstæmp/、/ˌiː ˈen/、/əˈsembli ˈskelɪtən/，n./缩写/n. phr.：时间戳／English（英语）／编排骨架。
- **4-tuple / recipe / post-SFX** /fɔːr ˈtuːpəl/、/ˈresəpi/、/poʊst ˌes ef ˈeks/，n./n./缩写表达：四元组／配置配方／后期特效音。
- **skin-only swap / prop tier / cognitive** /skɪn ˈoʊnli swɑːp/、/prɑːp tɪr/、/ˈkɑːɡnətɪv/，n. phr./n. phr./adj.：只换外观的替换／道具等级／认知方面的。
- **pitfall / checklist / anti-hallucination** /ˈpɪtfɔːl/、/ˈtʃeklɪst/、/ˌænti həˌluːsɪˈneɪʃən/，n./n./adj. phr.：陷阱／检查清单／抑制模型无依据编造的。
- **all-purpose / hand-off / shot syntax / reference label** /ˌɔːl ˈpɜːrpəs/、/ˈhændɔːf/、/ʃɑːt ˈsɪntæks/、/ˈrefərəns ˈleɪbəl/，adj./n./n. phr./n. phr.：通用的／交接／镜头语法／参考标签。
- **heuristic / cheatsheet / command reference** /hjʊˈrɪstɪk/、/ˈtʃiːt ʃiːt/、/kəˈmænd ˈrefərəns/，n./n./n. phr.：经验判断方法／速查表／命令参考。
- **one-click / param / incl. / optional** /wʌn klɪk/、/ˈpærəm/、/ɪnˈkluːdɪŋ/、/ˈɑːpʃənəl/，adj. phr./缩写/缩写/adj.：一键的／parameter（参数）的简称／including（包括）的缩写／可选的。
- **band energy / credibility / phrase contour** /bænd ˈenərdʒi/、/ˌkredəˈbɪləti/、/freɪz ˈkɑːntʊr/，n. phr./n./n. phr.：频带能量／可信度／乐句轮廓。

**简体中文译文**

以下把原文目录树改排为等价表格，保留全部路径和注释信息：

| 原文件路径 | 说明 |
|---|---|
| `SKILL.md` | 主工作流：5 个证据通道、6 条检查、10 步标准操作流程、状态机分流。 |
| `README.md` | 项目说明。 |
| `LICENSE` | MIT 许可证。 |
| `agents/openai.yaml` | 智能体元数据。 |
| `references/01-forensics-commands.md` | 采样、网格、声谱图、RMS、音头、场景切换、时间码命令，以及对账矩阵。 |
| `references/02-h3-field-mapping.md` | 观察结果到 14 字段的映射、时间戳规则、英文编排骨架。 |
| `references/03-edit-effects.md` | 定格四元组、白闪／漫画／故障特效配方，以及后期特效音。 |
| `references/04-coser-replacement.md` | 仅替换外观的标准操作流程、动作兼容性、道具分级与对照表。 |
| `references/05-pitfalls-checklist.md` | 16 个陷阱、6 条检查，以及认知与交付检查清单。 |
| `references/06-film-type-and-state-machine.md` | A／B／C 片型分流、锁定↔爆发、具名机位、可数冲击、滚转与反幻觉骨架。 |
| `references/07-onset-and-card-points.md` | 音头检测、自由弹性节奏与固定速度的区分、卡点表、伪切镜过滤及时间码网格。 |
| `references/08-multi-image-and-segmentation.md` | 多图通用锁定、零外貌文字规则、超过 15 秒的切分及交接。 |
| `references/shot-syntax.md` | Ref2VA 六部分骨架、切镜语法与相机词汇。 |
| `references/audio-heuristics.md` | 声谱图／RMS／BPM 与 `volumedetect` 音量检测到音乐配方表的对应关系。 |
| `references/ffmpeg-cheatsheet.md` | 以 PowerShell 为主的 ffprobe／ffmpeg 命令速查。 |
| `scripts/forensic_probe.ps1` | Windows 一键取证，视频参数为 `-Video`，包含音头检测。 |
| `scripts/forensic_probe.sh` | macOS／Linux 一键取证，包含音头检测。 |
| `scripts/audio_probe.py` | RMS 包络、频带能量与 BPM 可信度；需要 numpy，librosa 可选。 |
| `scripts/onset_probe.py` | 分级音头／卡点检测及乐句轮廓；需要 numpy、scipy，不需要 librosa。 |

## 6. 运行要求（原文第 56–59 行）

### 6.1 媒体工具（第 58 行）

**词汇与术语**

- **requirements** /rɪˈkwaɪərmənts/，复数 n.：运行要求、依赖条件。
- **PATH** /pæθ/，环境变量名：系统查找可执行程序的目录列表。
- **ffmpeg / ffprobe**：命令标识，原样保留；**probe** /proʊb/（v./n.）意为探测，对应媒体信息探测工具。

**简体中文译文**

`ffmpeg` 和 `ffprobe` 必须能从系统 `PATH` 中找到。

### 6.2 Python 依赖（第 59 行）

**词汇与术语**

- **Python** /ˈpaɪθɑːn/，专名：Python 语言。
- **additionally / optional / throughout** /əˈdɪʃənəli/、/ˈɑːpʃənəl/、/θruːˈaʊt/，adv./adj./adv.：此外／可选的／在整个流程中。
- **onset analysis** /ˈɑːnset əˈnæləsɪs/，n. phr.：音头分析。
- **version / wheel** /ˈvɜːrʒən/、/wiːl/，n.：版本／Python 预构建分发包格式。
- **numpy / scipy / librosa**：依赖包名称，保留准确拼写供安装和查找。

**简体中文译文**

`audio_probe.py` 需要安装 numpy 的 Python 3；`onset_probe.py` 还需要 scipy。整个流程中 librosa 都是可选依赖，不安装它也能进行音头分析，尤其适用于原文所举 Python 3.14 等尚无可用 librosa wheel 包的情形。

> 译注：关于特定 Python 版本是否存在 wheel 的说法属于源版本的依赖状况陈述；本次仅翻译，不把它作为对当前软件支持状态的重新核验结论。

## 7. 快速开始（原文第 61–75 行）

### 7.1 Windows 命令（第 63–67 行）

**词汇与术语**

- **quick start** /kwɪk stɑːrt/，n. phr.：快速开始。
- **PowerShell** /ˈpaʊərʃel/，专名：命令行外壳与脚本环境。
- **profile / execution policy / bypass / file / video / out directory** /ˈproʊfaɪl/、/ˌeksɪˈkjuːʃən ˈpɑːləsi/、/ˈbaɪpæs/、/faɪl/、/ˈvɪdioʊ/、/aʊt dəˈrektəri/，n. phr. 或 n.：启动配置／执行策略／绕过模式／文件／视频／输出目录。
- `-NoProfile`：不加载启动配置；`-ExecutionPolicy Bypass`：此调用使用原文所列的执行策略；`-File`：待执行脚本；`-Video`：输入视频；`-OutDir`：输出目录。参数本身不是待中文化的标识。

**简体中文译文**

在 Windows 中执行以下原样命令：

```powershell
powershell -NoProfile -ExecutionPolicy Bypass -File scripts/forensic_probe.ps1 -Video ".\clip.mp4" -OutDir forensic_out
```

### 7.2 macOS／Linux 命令（第 69–73 行）

**词汇与术语**

- **bash** /bæʃ/，专名／缩写：Bourne Again Shell，命令行外壳；**shell** /ʃel/（n.）指命令解释环境。
- **clip** /klɪp/，n.：视频片段；`clip.mp4` 是示例输入文件名。
- **forensic / out** /fəˈrenzɪk/、/aʊt/，adj./标识词：取证的／输出；`forensic_out` 是输出目录名。

**简体中文译文**

在 macOS 或 Linux 中执行以下原样命令：

```bash
bash scripts/forensic_probe.sh "clip.mp4" forensic_out
```

### 7.3 命令之后的处理与交付（第 75 行）

**词汇与术语**

- **follow / grid / dense-extract / ambiguous window** /ˈfɑːloʊ/、/ɡrɪd/、/dens ɪkˈstrækt/、/æmˈbɪɡjuəs ˈwɪndoʊ/，v./n./v. phr./n. phr.：遵循／网格图／密集提取／歧义时间区间。
- **triage / reconcile / onset / cut / hit** /triːˈɑːʒ/、/ˈrekənsaɪl/、/ˈɑːnset/、/kʌt/、/hɪt/，v./v./n./n./n.：分流／核对／音头／切镜／击打或冲击。
- **split / segment / assemble / reply / file delivery** /splɪt/、/ˈseɡmənt/、/əˈsembəl/、/rɪˈplaɪ/、/faɪl dɪˈlɪvəri/，v./n./v./n./n. phr.：拆分／片段／组装／回复／文件交付。

**简体中文译文**

然后按 `SKILL.md` 操作：阅读 `grid_*.jpg` 网格图，对所有歧义区间密集抽帧，依照 `references/06` 判定片型，把 `onsets.txt` 中的强音头与切镜或击打逐一核对（见 `references/07`），选择 H3 模式；长片依 `references/08` 拆成每段不超过 15 秒的片段，然后编排提示词。智能体在回复中给出可直接粘贴的英文文本块；只有要求文件交付时才保存 `.md` 文件。

## 8. 触发用语（原文第 77–79 行）

**词汇与术语**

- **trigger phrase** /ˈtrɪɡər freɪz/，n. phr.：触发用语，用于表明要调用该工作流。
- **reverse** /rɪˈvɜːrs/，v.：逆向分析；在 `reverse this video for h3` 中指为 H3 反推视频。
- **extract / prompt / clip** /ɪkˈstrækt/、/prɑːmpt/、/klɪp/，v./n./n.：提取／提示词／视频片段。

**简体中文译文**

触发用语包括：“反推视频”“视频转 H3 提示词”“卡点时间／节奏分析”“多镜头分镜运镜”“分段生成”“把图 1 替换进去／只换角色不改剧情”；英文用语 `reverse this video for h3` 译为“为 H3 反推这个视频”，`extract h3 prompt from this clip` 译为“从这个片段提取 H3 提示词”。

## 9. 配套技能（原文第 81–83 行）

**词汇与术语**

- **companion skill / pair with** /kəmˈpænjən skɪl/、/per wɪð/，n. phr./v. phr.：配套技能／搭配使用。
- **prompt-writing / field-reference** /prɑːmpt ˈraɪtɪŋ/、/fiːld ˈrefərəns/，n. phr.：提示词编写／字段参考。
- **e.g.** /ˌiː ˈdʒiː/：拉丁语 exempli gratia 的缩写，意为“例如”。
- **evidence / causal chain / state-machine decision / card point** /ˈevɪdəns/、/ˈkɔːzəl tʃeɪn/、/steɪt məˈʃiːn dɪˈsɪʒən/、/kɑːrd pɔɪnt/，n.：证据／因果链／状态机选择结论／卡点。
- **writer / field definition / output / analysis** /ˈraɪtər/、/fiːld ˌdefɪˈnɪʃən/、/ˈaʊtpʊt/、/əˈnæləsɪs/，n.：编写者或编写技能／字段定义／输出／分析。

**简体中文译文**

本项目可与 H3 提示词编写或字段参考技能（例如 `h3-prompt-master`）配合：本技能负责证据、因果链、状态机选择和卡点；编写技能提供字段定义。输出提示词使用英文，分析可以使用用户的语言。

## 10. 许可证（原文第 85–87 行）

**词汇与术语**

- **license** /ˈlaɪsəns/，n.：许可证。
- **MIT** /ˌem aɪ ˈtiː/：许可证名称，名称源自 Massachusetts Institute of Technology（麻省理工学院）。

**简体中文译文**

采用 MIT 许可证，详见原始 [`LICENSE`](LICENSE)；逐段中文释义见 [`LICENSE.zh-CN.md`](LICENSE.zh-CN.md)。
