# H3 Ref2VA 镜头语法参考｜简体中文逐段释义版

> 对应源文件：[shot-syntax.md](shot-syntax.md)。源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。
> 本文是阅读用译本，按源文顺序先释义再翻译；不替代运行配置、英文提示词模板或原始技能入口。命令、字段键、标签及路径保持原写法，中文解释说明其含义。音标采用常见英式或美式读法；标识符按构成词解释，不杜撰整个标识符的读音。译注只指出源文歧义，不修改原规则。


### 译段 01（源文第 1 行）

**词汇与术语**

shot /ʃɒt/（n.）镜头；syntax /ˈsɪntæks/（n.）语法、组织规则；reference /ˈrefərəns/（n.）参考；Ref2VA（模式标识）以参考素材驱动视频与音频生成的模式，Ref 表示 reference，2 按 to /tuː/ 理解，VA 表示视频／音频；本源文未给出完整官方名称。

**简体中文译文**

H3 Ref2VA 镜头语法参考。


### 译段 02（源文第 3 行）

**词汇与术语**

concise /kənˈsaɪs/（adj.）简明的；skeleton /ˈskelɪtən/（n.）骨架；detailed description /ˈdiːteɪld dɪˈskrɪpʃən/（名词短语）详细描述，对应 `detailed_description`；section /ˈsekʃən/（n.）章节；template /ˈtempleɪt/（n.）模板；forensic workflow /fəˈrensɪk ˈwɜːkfləʊ/（名词短语）取证工作流；dense sampling /dens ˈsɑːmplɪŋ/（名词短语）密集采样；cross-validation /ˌkrɒs vælɪˈdeɪʃən/（n.）交叉验证；causal event chain /ˈkɔːzəl ɪˈvent tʃeɪn/（名词短语）因果事件链；freeze-frame gag /ˈfriːz freɪm ɡæɡ/（名词短语）定格笑点；govern /ˈɡʌvən/（v.）规定；T2VA／I2VA／FL2VA／L2VA 为模式标识，分别对应文本、首帧图、首尾帧图、尾帧图作为生成条件；此处保留源文标识。

**简体中文译文**

本文为 `detailed_description` 章节提供简明骨架。填写任何 Ref2VA 提示词时都可复用，输入为视频加一张或多张参考图、参考视频或参考音频。T2VA／I2VA／FL2VA／L2VA 使用 `02-h3-field-mapping.md` 中的 14 字段模板。负责**产出**这些内容的取证流程，包括密集采样、音频交叉验证、因果事件链和定格笑点，位于 `SKILL.md` 与 `01-forensics-commands.md`；本文件规定如何把这些内容写入 Ref2VA 字段。


## 六段式骨架


### 译段 03（源文第 5–10 行）

**词汇与术语**

six-section /ˌsɪks ˈsekʃən/（adj.）六段的；subject definition /ˈsʌbdʒɪkt ˌdefɪˈnɪʃən/（名词短语）主体定义，字段 `subject_definitions`；identity /aɪˈdentəti/（n.）身份；appearance /əˈpɪərəns/（n.）外观；picture /ˈpɪktʃə/（n.）图片；video /ˈvɪdiəʊ/（n.）视频；source /sɔːs/（n.）源素材；target /ˈtɑːɡɪt/（n./adj.）目标；shot structure /ʃɒt ˈstrʌktʃə/（名词短语）镜头结构；motion path /ˈməʊʃən pɑːθ/（名词短语）运动路径；pacing /ˈpeɪsɪŋ/（n.）节奏推进；temporal /ˈtempərəl/（adj.）时间上的；discard /dɪˈskɑːd/（v.）舍弃。

**简体中文译文**

六段式骨架——第一段：主体定义。

```text
subject_definitions:
<Subject 1> 是 <Picture 1> 中的 <身份>，具有 <外观清单>。
<Video 1> 是用于规定目标视频镜头结构、运动路径与节奏的源视频：<一句话源视频描述>。<Video 1> 仅用于时间结构参考；<说明舍弃什么>。
```


> **译注：** 源文模板同时写了运动路径／节奏及“仅用于时间结构”，具体保留边界须由占位内容明确。本文件的外观清单写法与 `08-multi-image-and-segmentation.md` 的多图零外貌文字规则适用范围不同，译文未合并两者。


### 译段 04（源文第 12–13 行）

**词汇与术语**

summary /ˈsʌməri/（n.）摘要；task /tɑːsk/（n.）任务；asset /ˈæset/（n.）资产；tag /tæɡ/（n.）标签；one-paragraph /ˌwʌn ˈpærəɡrɑːf/（adj.）单段的；`<Subject 1>`、`<Picture 1>`、`<Video 1>` 是固定引用标签，分别指主体、图片和视频。

**简体中文译文**

第二段：摘要。

```text
summary:
[<任务标签> + <资产标签>] <用一个段落概述任务，并使用 <Subject 1>、<Picture 1>、<Video 1> 等标签>。
```


### 译段 05（源文第 15–18 行）

**词汇与术语**

retention /rɪˈtenʃən/（n.）保留；analysis /əˈnæləsɪs/（n.）分析；appear /əˈpɪə/（v.）出现；fully /ˈfʊli/（adv.）完全地；partially /ˈpɑːʃəli/（adv.）部分地；preserved /prɪˈzɜːvd/（adj./过去分词）保留的；transferred /trænsˈfɜːd/（过去分词）迁移的；reused /ˌriːˈjuːzd/（过去分词）复用的；structural cue /ˈstrʌktʃərəl kjuː/（名词短语）结构线索；reference /ˈrefərəns/（n.）参考。

**简体中文译文**

第三段：保留分析。

```text
retention_analysis:
<Subject 1>（出现在 [Shot X] 等镜头中）：<fully_preserved | partially_preserved | transferred | reused> — <保留什么>。
<Video 1>（约束整个视频）：reference — <保留哪些时间／结构线索>；<舍弃什么>。
[为每个其他参考素材补一行]
```

四个状态值依次表示“完全保留／部分保留／迁移／复用”；`reference` 表示“参考”。


### 译段 06（源文第 20–25 行）

**词汇与术语**

detailed /ˈdiːteɪld/（adj.）详细的；description /dɪˈskrɪpʃən/（n.）描述；style /staɪl/（n.）风格；composition /ˌkɒmpəˈzɪʃən/（n.）构图；element /ˈelɪmənt/（n.）要素；transition /trænˈzɪʃən/（n.）转场；verb /vɜːb/（n.）动词；rest /rest/（n.）其余部分；`[Shot N]`（标记）第 N 个镜头；`00:XX.XXX`（占位时间码）保留原精度。

**简体中文译文**

第四段：详细描述。

```text
detailed_description:
目标视频采用 <一句话风格描述>。

[Shot 1] <包含六项要素的构图与镜头描述，详见下文>。

[Shot 2] 在 00:XX.XXX，<转场动词> <该镜头其余包含六要素的描述>。
```


### 译段 07（源文第 27–28 行）

**词汇与术语**

overall soundscape /ˌəʊvərˈɔːl ˈsaʊndskeɪp/（名词短语）整体声景；ambience /ˈæmbiəns/（n.）环境声；physical /ˈfɪzɪkəl/（adj.）物理动作产生的；SFX /ˌes ef ˈeks/（sound effects）音效；non-verbal /ˌnɒn ˈvɜːbəl/（adj.）非语言的；post /pəʊst/（此处作前缀）后期；freeze-frame /ˈfriːz freɪm/（n.）定格。

**简体中文译文**

第五段：整体声景。

```text
overall_soundscape:
<贯穿整个视频的环境声 + 物理动作音效 + 人物非语言声音；定格的后期音效归入这里>。
```


### 译段 08（源文第 30–32 行）

**词汇与术语**

non-diegetic /ˌnɒn daɪəˈdʒetɪk/（adj.）非叙事内的；music /ˈmjuːzɪk/（n.）音乐；audience-only /ˌɔːdiəns ˈəʊnli/（adj.）只面向观众的；score /skɔː/（n.）配乐；instrumentation /ˌɪnstrʊmenˈteɪʃən/（n.）乐器配置；tempo /ˈtempəʊ/（n.）速度；dynamics /daɪˈnæmɪks/（n.）力度变化；N/A /ˌen ˈeɪ/（常指 not applicable）不适用。

**简体中文译文**

第六段：非叙事内音乐。

```text
non_diegetic_music:
<仅面向观众的配乐：乐器配置 + 速度 + 力度变化> | N/A
```


## 每个镜头的六要素


### 译段 09（源文第 34–39 行）

**词汇与术语**

per-shot /ˌpɜː ˈʃɒt/（adj.）逐镜头的；element /ˈelɪmənt/（n.）要素；block /blɒk/（n.）文本块；cover /ˈkʌvə/（v.）涵盖；missing /ˈmɪsɪŋ/（adj.）缺失的；hallucinate /həˈluːsɪneɪt/（v.）产生幻觉、生成无依据内容；template /ˈtempleɪt/（n.）模板。

**简体中文译文**

每个 `[Shot N]` 文本块都必须包含全部六项要素。源文指出，缺少其中任何一项都是 H3 产生无依据内容的常见原因。原表按“序号／要素／模板”组织。


### 译段 10（源文第 40 行）

**词汇与术语**

composition /ˌkɒmpəˈzɪʃən/（n.）构图；wide shot /waɪd ʃɒt/（名词短语）广景镜头；medium close-up /ˌmiːdiəm ˈkləʊs ʌp/（名词短语）中近景；tight close-up /taɪt ˈkləʊs ʌp/（名词短语）紧特写；over-the-shoulder shot /ˌəʊvə ðə ˈʃəʊldə ʃɒt/（名词短语）过肩镜头。

**简体中文译文**

1. **构图。** 模板词组依次为：一个广景镜头／一个中近景镜头／一个紧特写镜头／一个过肩镜头。


### 译段 11（源文第 41 行）

**词汇与术语**

subject /ˈsʌbdʒɪkt/（n.）主体；appearance /əˈpɪərəns/（n.）外观；position /pəˈzɪʃən/（n.）位置；identity /aɪˈdentəti/（n.）身份；key feature /kiː ˈfiːtʃə/（名词短语）关键特征；phrase /freɪz/（n.）短语。

**简体中文译文**

2. **主体外观与位置。** 模板：`<Subject 1>`，即具有 `<关键特征>` 的 `<身份>`，`<位置短语>`。


### 译段 12（源文第 42 行）

**词汇与术语**

environment /ɪnˈvaɪrənmənt/（n.）环境；lighting /ˈlaɪtɪŋ/（n.）照明；setting /ˈsetɪŋ/（n.）场景；light source /laɪt sɔːs/（名词短语）光源；quality /ˈkwɒləti/（n.）光质；direction /dəˈrekʃən/（n.）方向。

**简体中文译文**

3. **环境与光线。** 模板：`<场景>`，伴随 `<光源 + 光质 + 光线方向>`。


### 译段 13（源文第 43 行）

**词汇与术语**

action /ˈækʃən/（n.）动作；state change /steɪt tʃeɪndʒ/（名词短语）状态变化；present-tense /ˌprezənt ˈtens/（adj.）现在时的；visible /ˈvɪzəbəl/（adj.）可见的；trigger /ˈtrɪɡə/（n.）触发因素；result /rɪˈzʌlt/（n.）结果；diegetic /ˌdaɪəˈdʒetɪk/（adj.）叙事内的；embedded /ɪmˈbedɪd/（adj./过去分词）嵌入的。

**简体中文译文**

4. **动作与状态变化。** 模板：`<Subject 1> <用现在时描述动作>……<可见状态变化>`。采用“触发→动作→结果”的链条，把叙事内动作声嵌入动作句。


### 译段 14（源文第 44 行）

**词汇与术语**

camera movement /ˈkæmərə ˈmuːvmənt/（名词短语）相机运动；push in /pʊʃ ɪn/（动词短语）向前推进；amplitude /ˈæmplɪtjuːd/（n.）幅度；slow speed /sləʊ spiːd/（名词短语）慢速；hold steady /həʊld ˈstedi/（动词短语）保持稳定；pull out /pʊl aʊt/（动词短语）向后拉远。

**简体中文译文**

5. **相机运动。** 模板：相机以小幅度、慢速度向前推进／保持稳定／向后拉远。


### 译段 15（源文第 45 行）

**词汇与术语**

current /ˈkʌrənt/（adj.）当前的；sound /saʊnd/（n.）声音；short /ʃɔːt/（adj.）简短的；onomatopoeic /ˌɒnəˌmætəˈpiːɪk/（adj.）拟声的；descriptive /dɪˈskrɪptɪv/（adj.）描述性的；cue /kjuː/（n.）提示、线索。

**简体中文译文**

6. **当前声音。** 模板：`<简短的拟声提示或声音描述>`。


## 切镜语法：仅适用于多镜头


### 译段 16（源文第 47–54 行）

**词汇与术语**

cut /kʌt/（n.）切镜；syntax /ˈsɪntæks/（n.）语法；multi-shot /ˌmʌlti ˈʃɒt/（adj.）多镜头的；timestamp /ˈtaɪmstæmp/（n.）时间戳；strictly increasing /ˈstrɪktli ɪnˈkriːsɪŋ/（形容词短语）严格递增的；At /æt/（prep.）在……时刻。

**简体中文译文**

切镜语法（仅适用于多镜头）：

```text
[Shot 1]                           ← 不带时间戳
[Shot 2] 在 00:03.200，……          ← 第一次切镜；后续时间严格递增
[Shot 3] 在 00:06.400，……
[Shot N] 在 00:11.700，……
```

英文模板中的 `At` 在中文阅读版中译为“在”；镜头标签和时间码原样保留。


### 译段 17（源文第 56–58 行）

**词汇与术语**

rule /ruːl/（n.）规则；decimal /ˈdesɪməl/（n.）小数位；period /ˈpɪəriəd/（n.）句点，此处指小数点；separator /ˈsepəreɪtə/（n.）分隔符。

**简体中文译文**

规则：始终使用两位小数，以句点作为分隔符。


> **译注：** 原文此句明确写“two decimals”，但上面的 `00:03.200` 等示例使用三位小数；本译本保留文字与示例两者，不擅自选定精度。


### 译段 18（源文第 59 行）

**词汇与术语**

forbidden /fəˈbɪdən/（adj.）禁止的；timestamp /ˈtaɪmstæmp/（n.）时间戳；only /ˈəʊnli/（adj.）唯一的。

**简体中文译文**

禁止在 `[Shot 1]` 上写 `0.00`；`[Shot 1]` 是唯一不带时间戳的镜头。


### 译段 19（源文第 60 行）

**词汇与术语**

strictly greater than /ˈstrɪktli ˈɡreɪtə ðæn/（比较短语）严格大于；previous /ˈpriːviəs/（adj.）前一个的；less than or equal to /les ðæn ɔː ˈiːkwəl tuː/（比较短语）小于或等于；duration /djʊˈreɪʃən/（n.）持续时间，对应字段／变量 `duration`。

**简体中文译文**

每个切镜时间必须**严格大于前一个切镜时间**，并且**小于或等于 `duration`**。


### 译段 20（源文第 61 行）

**词汇与术语**

final /ˈfaɪnəl/（adj.）最后的；implicitly /ɪmˈplɪsɪtli/（adv.）隐含地、默认地；duration /djʊˈreɪʃən/（n.）时长；repeat /rɪˈpiːt/（v.）重复。

**简体中文译文**

最后一个镜头默认在 `duration` 处结束，无须再重复写结束时间。


### 译段 21（源文第 62 行）

**词汇与术语**

freeze-frame gag /ˈfriːz freɪm ɡæɡ/（名词短语）定格笑点；event /ɪˈvent/（n.）事件；in-point /ˈɪn pɔɪnt/（n.）入点；duration /djʊˈreɪʃən/（n.）持续时长；snap-back /ˈsnæp bæk/（n.）瞬间恢复；`FREEZE-FRAME GAG n`（事件标签）第 n 个定格笑点。

**简体中文译文**

定格笑点**不是切镜**：应把它留在同一个镜头中，标记为 `FREEZE-FRAME GAG n` 事件，并写清入点、持续时长与恢复方式。参见 `03-edit-effects.md`。


## 转场动词库


### 译段 22（源文第 64–69 行）

**词汇与术语**

transition /trænˈzɪʃən/（n.）转场；verb /vɜːb/（n.）动词；library /ˈlaɪbrəri/（n.）词库；pick /pɪk/（v.）选择；mix /mɪks/（v.）混用。

**简体中文译文**

转场动词库：每个切点选择一种，不要混用。原表按“动词表达／使用条件”排列。


### 译段 23（源文第 70 行）

**词汇与术语**

the camera cuts to /ðə ˈkæmərə kʌts tuː/（动词表达）镜头切至；plain /pleɪn/（adj.）普通的；hard cut /hɑːd kʌt/（名词短语）硬切；default /dɪˈfɔːlt/（n./adj.）默认值／默认的。

**简体中文译文**

`the camera cuts to`：镜头切至……。用于普通硬切，是默认表达。


### 译段 24（源文第 71 行）

**词汇与术语**

the shot transitions to /ðə ʃɒt trænˈzɪʃənz tuː/（动词表达）镜头过渡到；soft cut /sɒft kʌt/（名词短语）柔和切换；fade /feɪd/（n.）淡入淡出；dissolve /dɪˈzɒlv/（n.）叠化。

**简体中文译文**

`the shot transitions to`：镜头过渡到……。用于柔和切换、淡入淡出或叠化。


### 译段 25（源文第 72 行）

**词汇与术语**

the view shifts to /ðə vjuː ʃɪfts tuː/（动词表达）画面视角转移到；focal length /ˈfəʊkəl leŋθ/（名词短语）焦距；angle /ˈæŋɡəl/（n.）角度。

**简体中文译文**

`the view shifts to`：画面视角转移到……。用于同一相机内焦距或角度发生变化。


### 译段 26（源文第 73 行）

**词汇与术语**

a hard cut reveals /ə hɑːd kʌt rɪˈviːlz/（动词表达）一次硬切呈现出；deliberately /dɪˈlɪbərətli/（adv.）刻意地；scene state /siːn steɪt/（名词短语）场景状态。

**简体中文译文**

`a hard cut reveals`：一次硬切呈现出……。用于硬切后刻意展现明显不同的场景状态。


### 译段 27（源文第 74 行）

**词汇与术语**

the angle switches to /ði ˈæŋɡəl ˈswɪtʃɪz tuː/（动词表达）机位角度切换为；quick /kwɪk/（adj.）快速的；flip /flɪp/（n.）翻转、突变；subject continuity /ˈsʌbdʒɪkt ˌkɒntɪˈnjuːəti/（名词短语）主体连续性。

**简体中文译文**

`the angle switches to`：机位角度切换为……。用于快速切换角度，同时保持主体连续性。


## 单镜头视频：没有切镜


### 译段 28（源文第 76–83 行）

**词汇与术语**

single-shot /ˌsɪŋɡəl ˈʃɒt/（adj.）单镜头的；initial /ɪˈnɪʃəl/（adj.）初始的；composition /ˌkɒmpəˈzɪʃən/（n.）构图；first action /fɜːst ˈækʃən/（名词短语）第一个动作；next action /nekst ˈækʃən/（名词短语）下一个动作；At /æt/（prep.）在……时刻。

**简体中文译文**

单镜头视频（无切镜）：

```text
[Shot 1] <初始构图>。

<Subject 1> <第一个动作>。在 00:01.200，<Subject 1> <下一个动作>。
在 00:02.500，<Subject 1> <下一个动作>。……
```


### 译段 29（源文第 85 行）

**词汇与术语**

tie /taɪ/（v.）绑定、衔接；emote /ɪˈməʊt/（常用作 v.，源文此处名词化）情绪表达；beat /biːt/（n.）叙事节拍；clause /klɔːz/（n.）分句；prank /præŋk/（n.）恶作剧；UGC /ˌjuː dʒiː ˈsiː/（user-generated content /ˌjuːzə ˈdʒenəreɪtɪd ˈkɒntent/）用户生成内容；reversal /rɪˈvɜːsəl/（n.）反转；freeze gag /friːz ɡæɡ/（名词短语）定格笑点；multi-cut /ˌmʌlti ˈkʌt/（adj.）多次切镜的。

**简体中文译文**

把每个情绪表达或叙事节拍，用 `At 00:XX.XXX`（“在某一时刻”）分句绑定在同一个 `[Shot 1]` 文本块里。多数恶作剧／用户生成内容的反转，是带有定格笑点的单镜头，而不是多次切镜。


## 相机运动词汇


### 译段 30（源文第 87–89 行）

**词汇与术语**

camera movement /ˈkæmərə ˈmuːvmənt/（名词短语）相机运动；vocabulary /vəˈkæbjələri/（n.）词汇；push in /pʊʃ ɪn/（动词短语）推进；small amplitude /smɔːl ˈæmplɪtjuːd/（名词短语）小幅度；slow speed /sləʊ spiːd/（名词短语）慢速；gentle /ˈdʒentəl/（adj.）轻柔的；forward dolly /ˈfɔːwəd ˈdɒli/（名词短语）相机向前移动。

**简体中文译文**

`the camera pushes in with small amplitude at slow speed`：相机以小幅度、慢速度向前推进——轻柔的向前移动镜头。


### 译段 31（源文第 90 行）

**词汇与术语**

push in /pʊʃ ɪn/（动词短语）推进；medium amplitude /ˈmiːdiəm ˈæmplɪtjuːd/（名词短语）中等幅度；moderate speed /ˈmɒdərət spiːd/（名词短语）适中速度；noticeable /ˈnəʊtɪsəbəl/（adj.）明显可察觉的；dolly /ˈdɒli/（n.）相机移动拍摄。

**简体中文译文**

`the camera pushes in with medium amplitude at moderate speed`：相机以中等幅度、适中速度向前推进——可明显察觉的推进镜头。


### 译段 32（源文第 91 行）

**词汇与术语**

pull out /pʊl aʊt/（动词短语）拉远；small /smɔːl/（adj.）小的；amplitude /ˈæmplɪtjuːd/（n.）幅度；slow /sləʊ/（adj.）慢的；back dolly /bæk ˈdɒli/（名词短语）相机后移。

**简体中文译文**

`the camera pulls out with small amplitude at slow speed`：相机以小幅度、慢速度向后拉远——轻柔的后移镜头。


### 译段 33（源文第 92 行）

**词汇与术语**

truck right /trʌk raɪt/（动词短语）相机向右横移；small amplitude /smɔːl ˈæmplɪtjuːd/（名词短语）小幅度；slow speed /sləʊ spiːd/（名词短语）慢速；lateral slide /ˈlætərəl slaɪd/（名词短语）侧向滑移。

**简体中文译文**

`the camera trucks right with small amplitude at slow speed`：相机以小幅度、慢速度向右横移——侧向滑移镜头。


### 译段 34（源文第 93 行）

**词汇与术语**

hold steady /həʊld ˈstedi/（动词短语）保持稳定；locked-off /ˌlɒkt ˈɒf/（adj.）固定机位、完全锁定的。

**简体中文译文**

`the camera holds steady`：相机保持稳定——固定机位。


### 译段 35（源文第 94 行）

**词汇与术语**

pan right /pæn raɪt/（动词短语）向右水平摇镜；amplitude /ˈæmplɪtjuːd/（n.）幅度；horizontal /ˌhɒrɪˈzɒntəl/（adj.）水平的；rotation /rəʊˈteɪʃən/（n.）转动。

**简体中文译文**

`the camera pans right with small amplitude at slow speed`：相机以小幅度、慢速度向右水平摇镜——水平转动。


### 译段 36（源文第 95 行）

**词汇与术语**

tilt down/up /tɪlt daʊn ʌp/（动词短语）向下／向上俯仰摇镜；small amplitude /smɔːl ˈæmplɪtjuːd/（名词短语）小幅度；medium speed /ˈmiːdiəm spiːd/（名词短语）中等速度；vertical rotation /ˈvɜːtɪkəl rəʊˈteɪʃən/（名词短语）垂直方向转动。

**简体中文译文**

`the camera tilts down/up with small amplitude at medium speed`：相机以小幅度、中等速度向下／向上俯仰摇镜——垂直方向转动。


### 译段 37（源文第 96 行）

**词汇与术语**

handheld /ˈhændheld/（adj.）手持的；first-person /ˌfɜːst ˈpɜːsən/（adj.）第一人称的；subtle /ˈsʌtəl/（adj.）细微的；organic /ɔːˈɡænɪk/（adj.）自然的、带有身体感的；shake /ʃeɪk/（n.）晃动；throughout /θruːˈaʊt/（adv.）全程；gimbal /ˈɡɪmbəl/（n.）稳定云台；smooth /smuːð/（adj.）平滑的。

**简体中文译文**

手持第一人称模板：`subtle organic handheld shake throughout, never gimbal-smooth`——全程带有细微、自然的手持晃动，绝不呈现稳定云台般的平滑效果。


### 译段 38（源文第 98 行）

**词汇与术语**

quantify /ˈkwɒntɪfaɪ/（v.）量化；amplitude /ˈæmplɪtjuːd/（n.）幅度；none /nʌn/（pron.）无；small /smɔːl/（adj.）小；medium /ˈmiːdiəm/（adj.）中等；large /lɑːdʒ/（adj.）大；speed /spiːd/（n.）速度；slow /sləʊ/（adj.）慢；moderate /ˈmɒdərət/（adj.）适中；fast /fɑːst/（adj.）快；motivation /ˌməʊtɪˈveɪʃən/（n.）动机。

**简体中文译文**

始终量化幅度（无／小／中／大）和速度（慢／适中／快），并说明每次相机运动的动机。


## 主体开场句式


### 译段 39（源文第 100–102 行）

**词汇与术语**

subject /ˈsʌbdʒɪkt/（n.）主体；opening pattern /ˈəʊpənɪŋ ˈpætən/（名词短语）开场句式；continuity /ˌkɒntɪˈnjuːəti/（n.）连续性；echo /ˈekəʊ/（v.）复述、呼应；last known position /lɑːst nəʊn pəˈzɪʃən/（名词短语）上一次已知的位置。

**简体中文译文**

主体开场句式：为保证每次切镜的连续性，新镜头开头应复述主体上一次已知的位置。


### 译段 40（源文第 104–107 行）

**词汇与术语**

tight close-up /taɪt ˈkləʊs ʌp/（名词短语）紧特写；remain seated /rɪˈmeɪn ˈsiːtɪd/（动词短语）仍坐着；table /ˈteɪbəl/（n.）桌子；bowl /bəʊl/（n.）碗；spoon /spuːn/（n.）勺子；in frame /ɪn freɪm/（介词短语）在画面内。

**简体中文译文**

```text
[Shot 2] 在 00:03.200，镜头切到 <Subject 1> 的紧特写；
<Subject 1> 仍坐在镜头 1 中那张桌子旁，碗和勺子仍在画面内。
```


## 参考标签使用纪律


### 译段 41（源文第 109–114 行）

**词汇与术语**

reference label /ˈrefərəns ˈleɪbəl/（名词短语）参考标签；discipline /ˈdɪsəplɪn/（n.）使用纪律、规范；tag /tæɡ/（n.）标签；reusable /ˌriːˈjuːzəbəl/（adj.）可复用的；content /ˈkɒntent/（n.）内容。

**简体中文译文**

参考标签使用纪律：为每一项可复用内容选择正确标签。原表按“标签／用途”排列。


### 译段 42（源文第 115 行）

**词汇与术语**

subject /ˈsʌbdʒɪkt/（n.）主体；reusable /ˌriːˈjuːzəbəl/（adj.）可复用的；visible /ˈvɪzəbəl/（adj.）可见的；person /ˈpɜːsən/（n.）人；animal /ˈænɪməl/（n.）动物；object /ˈɒbdʒɪkt/（n.）物体；scene /siːn/（n.）场景；style /staɪl/（n.）风格；action /ˈækʃən/（n.）动作。

**简体中文译文**

`<Subject N>`：可复用的可见内容，包括人、动物、物体、场景、风格和动作。


### 译段 43（源文第 116 行）

**词汇与术语**

picture /ˈpɪktʃə/（n.）图片；image /ˈɪmɪdʒ/（n.）图像；frame anchor /freɪm ˈæŋkə/（名词短语）帧锚点；keyframe /ˈkiːfreɪm/（n.）关键帧；last frame /lɑːst freɪm/（名词短语）尾帧；composition reference /ˌkɒmpəˈzɪʃən ˈrefərəns/（名词短语）构图参考。

**简体中文译文**

`<Picture N>`：作为帧锚点、关键帧、尾帧或构图参考的图像。


### 译段 44（源文第 117 行）

**词汇与术语**

video /ˈvɪdiəʊ/（n.）视频；editing source /ˈedɪtɪŋ sɔːs/（名词短语）剪辑源素材；continuation /kənˌtɪnjuˈeɪʃən/（n.）续接；whole-video structure /ˌhəʊl ˈvɪdiəʊ ˈstrʌktʃə/（名词短语）整片结构。

**简体中文译文**

`<Video N>`：提供剪辑源素材、续接依据或整片结构的参考视频。


### 译段 45（源文第 118 行）

**词汇与术语**

audio signal /ˈɔːdiəʊ ˈsɪɡnəl/（名词短语）音频信号；copy /ˈkɒpi/（v.）复制；reference /ˈrefərəns/（v.）参考；voice /vɔɪs/（n.）人声；music /ˈmjuːzɪk/（n.）音乐；ambience /ˈæmbiəns/（n.）环境声。

**简体中文译文**

`<Audio N>`：为人声、音乐或环境声而复制或参考的音频信号。


### 译段 46（源文第 120 行）

**词汇与术语**

assign /əˈsaɪn/（v.）分配、指定；same /seɪm/（adj.）相同的；rename /ˌriːˈneɪm/（v.）重命名；alias /ˈeɪliəs/（n./v.）别名／设置别名；implicit reuse /ɪmˈplɪsɪt ˌriːˈjuːs/（名词短语）隐含复用；hard error /hɑːd ˈerə/（名词短语）硬性错误。

**简体中文译文**

标签一经分配，在每个章节中都必须表示**同一事物**。重命名、使用别名或隐含复用都属于硬性错误。


## “通用图 1”变体


### 译段 47（源文第 122–124 行）

**词汇与术语**

universal /ˌjuːnɪˈvɜːsəl/（adj.）通用的、全面适用的；picture /ˈpɪktʃə/（n.）图片；variant /ˈveəriənt/（n.）变体；define /dɪˈfaɪn/（v.）定义；character /ˈkærəktə/（n.）角色；scene /siːn/（n.）场景。

**简体中文译文**

“通用图 1”变体：当同一张参考图同时定义角色与场景时，使用以下写法。


### 译段 48（源文第 126–128 行）

**词汇与术语**

universal visual anchor /ˌjuːnɪˈvɜːsəl ˈvɪʒuəl ˈæŋkə/（名词短语）全面适用的视觉锚点；entire /ɪnˈtaɪə/（adj.）整个的；appearance /əˈpɪərəns/（n.）外观；costume /ˈkɒstjuːm/（n.）服装；hair /heə/（n.）头发；accessory /əkˈsesəri/（n.）配饰；compositional layout /ˌkɒmpəˈzɪʃənəl ˈleɪaʊt/（名词短语）构图布局；camera angle /ˈkæmərə ˈæŋɡəl/（名词短语）机位角度；lighting direction /ˈlaɪtɪŋ dəˈrekʃən/（名词短语）光线方向；color palette /ˈkʌlə ˈpælət/（名词短语）色彩方案；prop placement /prɒp ˈpleɪsmənt/（名词短语）道具位置；background environment /ˈbækɡraʊnd ɪnˈvaɪrənmənt/（名词短语）背景环境；wall tone /wɔːl təʊn/（名词短语）墙面色调；surrounding atmosphere /səˈraʊndɪŋ ˈætməsfɪə/（名词短语）周围氛围。

**简体中文译文**

```text
<Picture 1> 是整个目标视频全面适用的视觉锚点。它不仅规定 <Subject 1> 的外观、服装、头发和配饰，也规定场景的构图布局、机位角度、光线方向、色彩方案、道具位置与背景环境。目标视频需要决定房间、道具、窗光、墙面色调或周围氛围应是什么样时，都必须遵循 <Picture 1>。
```


### 译段 49（源文第 130 行）

**词汇与术语**

retention /rɪˈtenʃən/（n.）保留；govern /ˈɡʌvən/（v.）约束、规定；entire visual look /ɪnˈtaɪə ˈvɪʒuəl lʊk/（名词短语）整体视觉外观；framed /freɪmd/（过去分词）完成构图的；lit /lɪt/（light 的过去分词）布光的；defined /dɪˈfaɪnd/（过去分词）定义的。

**简体中文译文**

在保留分析中标注 `(governs the entire visual look)`，意为“约束整体视觉外观”；镜头开头写 `framed and lit as defined by <Picture 1>`，意为“按照 `<Picture 1>` 的规定构图并布光”。
