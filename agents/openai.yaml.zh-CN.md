# openai.yaml：智能体元数据逐段词汇释义与简体中文译文

源文件：[`agents/openai.yaml`](openai.yaml)；源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。本文件完整解释原有 4 行配置，供阅读对照，不作为替代配置加载。字段键保留原样；长字符串按完整语义句拆分，顺序不变。音标为 IPA；`n.`＝名词，`v.`＝动词，`adj.`＝形容词，`phr.`＝短语。

## 1. 智能体与显示名称（原文第 1–2 行）

**词汇与术语**

- **agent** /ˈeɪdʒənt/，n.：智能体；这里是顶层配置键 `agent`。
- **display name** /dɪˈspleɪ neɪm/，n. phr.：显示名称；对应 `display_name`。
- **video** /ˈvɪdioʊ/，n.：视频。
- **prompt** /prɑːmpt/，n.：提示词；`Video to H3 Prompt` 表示把视频转为 H3 提示词。

**简体中文译文**

智能体（`agent`）的显示名称（`display_name`）：**视频转 H3 提示词**。

## 2. 简短说明（原文第 3 行，完整字符串）

**词汇与术语**

- **short description** /ʃɔːrt dɪˈskrɪpʃən/，n. phr.：简短说明；对应 `short_description`。
- **forensically** /fəˈrenzɪkli/，adv.：以取证分析的方式。
- **reverse-engineer** /rɪˌvɜːrs endʒɪˈnɪr/，v.：逆向分析，从结果重建产生过程。
- **reference** /ˈrefərəns/，n./adj.：参考、参考用的。
- **ready-to-paste** /ˌredi tə ˈpeɪst/，adj. phr.：可以直接粘贴使用的。
- **dense frame sampling** /dens freɪm ˈsæmplɪŋ/，n. phr.：密集视频帧采样。
- **onset** /ˈɑːnset/，n.：音头，声音或音符起始的时刻。
- **card-point sync** /kɑːrd pɔɪnt sɪŋk/，n. phr.：原文用语，指音画卡点同步；`sync` 为 synchronization /ˌsɪŋkrənəˈzeɪʃən/（n.，同步）的简称。
- **causal event-chain reconstruction** /ˈkɔːzəl ɪˈvent tʃeɪn ˌriːkənˈstrʌkʃən/，n. phr.：因果事件链重建。
- **triage** /triːˈɑːʒ/，n./v.：分类分流；此处按片型选择相机机制。
- **continuous / snap-lock / multi-shot montage** /kənˈtɪnjuəs/、/snæp lɑːk/、/ˈmʌlti ʃɑːt mɑːnˈtɑːʒ/，adj.／n. phr.：连续的／快速重构图后锁定的编辑式快照／多镜头蒙太奇快剪。
- **camera state machine** /ˈkæmərə steɪt məˈʃiːn/，n. phr.：相机状态机，以不同状态及切换规则约束镜头。
- **freeze-frame / glitch** /ˈfriːz freɪm/、/ɡlɪtʃ/，n./n.：定格／故障失真效果。
- **multi-image character locking** /ˈmʌlti ˈɪmɪdʒ ˈkærəktər ˈlɑːkɪŋ/，n. phr.：用多张参考图锁定角色身份与服装。
- **segmentation** /ˌseɡmenˈteɪʃən/，n.：分段。
- **coser**：n.，角色扮演者的非正式称呼；源文未提供统一规范读音，本译本不另造音标。通行的对应词为 **cosplayer** /ˈkɑːzpleɪər/。
- **plot** /plɑːt/，n.：剧情。
- **T2VA / I2VA / FL2VA / L2VA / Ref2VA**：模式标识；按本仓库语境分别指文本、图像首帧、首尾帧、尾帧、参考素材驱动的音视频生成。`2` 按 **to** /tuː/ 理解；**text** /tekst/、**image** /ˈɪmɪdʒ/、**first/last** /fɜːrst/ /læst/、**reference** /ˈrefərəns/、**video/audio** /ˈvɪdioʊ/ /ˈɔːdioʊ/ 均为组成意义词，不把推定展开写成官方全称。

**简体中文译文**

通过密集视频帧采样、音乐音头与卡点同步、因果事件链重建、从片型到相机状态机的分流（连续镜头／编辑式快照锁定／多镜头蒙太奇快剪）、定格和故障特效、多图角色锁定、长片分段，以及不改变剧情的角色扮演者替换，对参考视频进行取证式逆向分析，生成可直接粘贴的 MiniMax H3 提示词（T2VA／I2VA／FL2VA／L2VA／Ref2VA）。

## 3. 默认提示词：目标与分析流程（原文第 4 行，第 1–2 句）

**词汇与术语**

- **default prompt** /dɪˈfɔːlt prɑːmpt/，n. phr.：默认提示词；对应 `default_prompt`。
- **analyze / attached / produce** /ˈænəlaɪz/、/əˈtætʃt/、/prəˈduːs/，v./adj./v.：分析／所附的／生成。
- **forensics / sparse grid** /fəˈrenzɪks/、/spɑːrs ɡrɪd/，n.／n. phr.：取证分析／稀疏采样网格。
- **fps** /ˌef piː ˈes/：缩略语，frames per second /freɪmz pər ˈsekənd/，每秒帧数；此处指抽帧频率。
- **transition frame** /trænˈzɪʃən freɪm/，n. phr.：转折或过渡区间的帧。
- **spectrogram** /ˈspektrəɡræm/，n.：声谱图，显示频率能量随时间的变化。
- **RMS** /ˌɑːr em ˈes/：缩略语，root mean square /ruːt miːn skwer/，均方根。
- **BPM** /ˌbiː piː ˈem/：缩略语，beats per minute /biːts pər ˈmɪnɪt/，每分钟拍数。
- **credibility / detection / reconcile** /ˌkredəˈbɪləti/、/dɪˈtekʃən/、/ˈrekənsaɪl/，n./n./v.：可信度／检测／核对并协调一致。
- **cut / freeze / impact / accent** /kʌt/、/friːz/、/ˈɪmpækt/、/ˈæksent/，n.：切镜／定格／冲击／重音。
- **shot-by-shot** /ʃɑːt baɪ ʃɑːt/，adv./adj. phr.：逐镜头地／逐镜头的。
- **named camera setup / angle** /neɪmd ˈkæmərə ˈsetʌp/、/ˈæŋɡəl/，n. phr./n.：具名机位／角度。
- **live action / edit-effects / sound layer** /laɪv ˈækʃən/、/ˈedɪt ɪˈfekts/、/saʊnd ˈleɪər/，n. phr.：现场实拍动作／剪辑特效／声音层。
- **assemble / required field** /əˈsembəl/、/rɪˈkwaɪərd fiːld/，v.／n. phr.：组装／必需字段。

**简体中文译文**

分析所附视频，并生成完整的 MiniMax H3 提示词。开展取证分析：制作稀疏采样网格，对转折区间按每秒 4–8 帧密集抽帧，生成声谱图，核验均方根能量与每分钟拍数的可信度，并检测音头和卡点；将每次切镜、定格与冲击逐一对齐核验强音乐音头；把片型分为连续长镜头、编辑式快照锁定或多镜头蒙太奇快剪，并采用相应的相机状态机；用明确命名的机位和角度建立逐镜头的因果事件链；分离现场动作层、相机层、剪辑特效层和声音层；随后选择 H3 模式，组装每个必需字段。

## 4. 默认提示词：参考图与长片分段（原文第 4 行，第 3 句）

**词汇与术语**

- **supplied** /səˈplaɪd/，adj.：已提供的。
- **identity / costume** /aɪˈdentəti/、/ˈkɑːstuːm/，n.：身份特征／服装。
- **appearance prose** /əˈpɪrəns proʊz/，n. phr.：用自然语言书写的外貌描述。
- **environment / prop** /ɪnˈvaɪrənmənt/、/prɑːp/，n.：环境／道具。
- **split / segment** /splɪt/、/ˈseɡmənt/，v./n.：拆分／片段。
- **per-segment clock** /pər ˈseɡmənt klɑːk/，n. phr.：各片段独立的段内计时。
- **non-restarting music** /nɑːn riːˈstɑːrtɪŋ ˈmjuːzɪk/，n. phr.：不在片段开头重新起奏的连续音乐。
- **hand-off state** /ˈhændɔːf steɪt/，n. phr.：交接状态，用来衔接前一段结尾与后一段开头。

**简体中文译文**

如果提供参考图，就以各自对应的图片锁定每个角色的身份和服装，省去外貌的文字描述，同时用文字定义环境与道具；将超过约 15 秒的片段拆成若干段，每段使用独立的段内时钟，音乐连续衔接而不重新开始，并设置交接状态。

## 5. 默认提示词：角色替换（原文第 4 行，第 4 句）

**词汇与术语**

- **coser**：n.，角色扮演者的非正式称呼；源文未提供统一规范读音，本译本不另造音标。通行的对应词为 **cosplayer** /ˈkɑːzpleɪər/。**character** /ˈkærəktər/，n.：角色。
- **swap** /swɑːp/，n./v.：替换。
- **appearance** /əˈpɪrəns/，n.：外貌、外观。
- **append** /əˈpend/，v.：附加在末尾。
- **replacement table** /rɪˈpleɪsmənt ˈteɪbəl/，n. phr.：替换对照表。

**简体中文译文**

如果用户要求替换角色扮演者或角色，则只改变外观，并在末尾附上替换对照表。

## 6. 默认提示词：交付方式（原文第 4 行，第 5 句）

**词汇与术语**

- **print / reply** /prɪnt/、/rɪˈplaɪ/，v./n.：输出显示／回复；这里的 `print` 不指纸张打印。
- **final / ready-to-paste / block** /ˈfaɪnəl/、/ˌredi tə ˈpeɪst/、/blɑːk/，adj./adj. phr./n.：最终的／可直接粘贴的／文本块。
- **save / file delivery / explicitly** /seɪv/、/faɪl dɪˈlɪvəri/、/ɪkˈsplɪsɪtli/，v./n. phr./adv.：保存／以文件形式交付／明确地。
- **.md**：Markdown /ˈmɑːrkdaʊn/ 文档扩展名，原样保留。

**简体中文译文**

在回复中直接给出最终可粘贴的英文提示词文本块；只有明确要求文件交付时，才保存 `.md` 文件。

> 译注：以上是源配置对视频分析任务的要求。“英文提示词”和“仅在要求时保存”均按原文译出，不改变本次中文翻译文件的性质或交付方式。
