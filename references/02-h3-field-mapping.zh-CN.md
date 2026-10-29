# 02 — 观察到 H3 字段的映射与组装骨架｜简体中文释义版

源文件：`references/02-h3-field-mapping.md`。源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。

本文件是独立的简体中文释义阅读版，按源文顺序先释义、后翻译；原始文件不作改动。命令、字段键、路径与引用标签保留原样，中文用于解释其含义；自然语言英文提示词均给出完整中文译文。此阅读版不是替代原始英文提示词或可执行技能的配置文件。音标采用常见英语读音；专有工具名、路径和代码符号不虚构统一读音。n.＝名词，v.＝动词，adj.＝形容词，adv.＝副词，phr.＝短语，abbr.＝缩略语。

## 01 · 标题与适用模式（源文第 1–3 行）

**词汇与术语**

- **T2VA / I2VA / FL2VA / L2VA / Ref2VA**，模式代号，本文分别用于文本生成、首帧图引导、首尾帧引导、仅尾帧引导及多参考输入的视频／音频生成。数字 2 按 to /tuː/（介词，到）理解；T 对应 text /tekst/（n.，文本），I 对应 image /ˈɪmɪdʒ/（n.，图像），FL 对应 first/last /fɜːrst læst/（adj.，首／末），L 对应 last，Ref 对应 reference /ˈrefərəns/（n.，参考）。这些是语境功能释义；源文没有正式展开这些代号。
- **field mapping** /fiːld ˈmæpɪŋ/，名词短语，字段映射；**shot syntax** /ʃɑːt ˈsɪntæks/，名词短语，镜头语法。

**简体中文译文**

# 02 — 观察结果 → H3 字段映射与组装骨架（T2VA／I2VA／FL2VA／L2VA）

Ref2VA 全参考模式使用另一套六段式结构，见 `shot-syntax.md`。本文件适用于无参考图，或仅以首帧／尾帧作参考的 14 字段式结构。

## 02 · 十四个字段及顺序（源文第 5–22 行）

**词汇与术语**

- **subject definitions** /ˈsʌbdʒɪkt ˌdefɪˈnɪʃənz/，名词短语，主体定义，对应 `subject_definitions`；**environment definition** /ɪnˈvaɪrənmənt ˌdefɪˈnɪʃən/，名词短语，环境定义；**lighting definition** /ˈlaɪtɪŋ ˌdefɪˈnɪʃən/，名词短语，灯光定义。
- **visual anchor** /ˈvɪʒuəl ˈæŋkər/，名词短语，视觉锚点；**audio** /ˈɔːdioʊ/，n.，音频；**supplied audio** /səˈplaɪd ˈɔːdioʊ/，名词短语，提供的音频；**fully copy** /ˈfʊli ˈkɑːpi/，动词短语，完整复制，对应 `fully_copy`。
- **integrated multimodal description** /ˈɪntɪɡreɪtɪd ˌmʌltiˈmoʊdəl dɪˈskrɪpʃən/，名词短语，综合多模态描述；**N-beat payoff** /en biːt ˈpeɪɔːf/，名词短语，经过 N 个叙事拍形成的效果落点／笑点回收；beat 在此是叙事或动作节奏单元，未必指音乐拍点。
- **camera direction** /ˈkæmərə dəˈrekʃən/，名词短语，相机与运镜指示；**editing** /ˈedɪtɪŋ/，n.，剪辑；**performance** /pərˈfɔːrməns/，n.，表演；**body mechanics** /ˈbɑːdi məˈkænɪks/，名词短语，身体运动机制。
- **costume hair physics** /ˈkɑːstuːm her ˈfɪzɪks/，组合名词短语，服装与头发的物理表现；**settle** /ˈsetəl/，v.，运动后回稳、停定。
- **negative constraints** /ˈneɡətɪv kənˈstreɪnts/，名词短语，负面约束、禁止事项；字段键为 `negative_constraints`，文中也简称 negative。
- **overall soundscape** /ˌoʊvərˈɔːl ˈsaʊndskeɪp/，名词短语，总体声景；**non-diegetic music** /ˌnɑːn ˌdaɪəˈdʒetɪk ˈmjuːzɪk/，名词短语，非场内音乐／画外配乐；**explicit silence** /ɪkˈsplɪsɪt ˈsaɪləns/，名词短语，明确指定静默。

**简体中文译文**

## 1. 字段顺序（不可调换；✓ 为必填，○ 为条件必填）

| 序号 | 原样保留的字段键 | 必选条件 | 填入内容与观察来源 |
|---|---|---|---|
| 1 | `subject_definitions` | ✓ | 主体定义：每个可见角色和画外角色的年龄感、发型与面部、整套服装、鞋袜手套、手持剧情道具、静态佩戴道具、职能；以及画幅。 |
| 2 | `environment_definition` | ○ | 环境定义：空间、建筑、地面、背景物件、静态载具、氛围与排除项；I2VA 首帧锁定时省略。 |
| 3 | `lighting_definition` | ○ | 灯光定义：主光方向、软硬程度、色温、环境补光、阴影、湿表面反射与高光、噪点、恒常性；I2VA 首帧锁定时省略。 |
| 4 | `visual_anchor` | I2VA | 视觉锚点：仅用于首帧锚定模式。 |
| 5 | `audio` | 复用音频时 | 音频：把提供的音频标为 `fully_copy`，即完整复制。 |
| 6 | `integrated_multimodal_description` | ✓ | 综合多模态描述：一句话交代结构前提＋N 个叙事拍的效果落点＋`[Shot 1]` 开场状态（不带时间戳）＋时间戳严格递增的事件链；动作句中嵌入同期声。 |
| 7 | `camera_direction` | ✓ | 相机指示：机位、视角、景别、基线晃动；每次运镜的类型、幅度、速度与**动机**；禁用运镜清单。 |
| 8 | `editing` | ✓ | 剪辑：切换策略；每个定格、转场、特效的入点、时长、叠加配方与恢复实拍的方式；N 个叙事拍的节奏。 |
| 9 | `performance` | ✓ | 表演：逐角色情绪弧、反差、表情约束，以及允许夸张出现的位置。 |
| 10 | `body_mechanics` | ✓ | 身体运动机制：蓄力规则、力传导链、喝水／喷出／受击动力学、双脚扎根。 |
| 11 | `costume_hair_physics` | ○ | 服装与头发物理表现：发型、面料、眼镜、裙摆、面罩的滞后摆动、湿身演化与回稳过程。 |
| 12 | `negative_constraints` | ✓ | 负面约束：集中排除人数、道具、风格化、运镜、剪辑、文字、漂移方面的不允许事项。 |
| 13 | `overall_soundscape` | ✓ | 总体声景：环境底噪＋按时间排列的同期声清单＋定格特效音＋录音质感。 |
| 14 | `non_diegetic_music` | ✓ | 画外配乐：完整复制音频（`fully_copy`）、目标音乐设计、明确静默，三者择一。 |

## 03 · 时间戳纪律：前四条（源文第 24–29 行）

**词汇与术语**

- **shot** /ʃɑːt/，n.，镜头；`[Shot 1]` 是第一镜头标签。**timestamp** /ˈtaɪmstæmp/，n.，时间戳。
- **with a small plastic click** /wɪð ə smɔːl ˈplæstɪk klɪk/，介词短语，伴随轻微的塑料咔哒声；click 为 n.，短促咔哒声。
- **audible pouring** /ˈɔːdəbəl ˈpɔːrɪŋ/，名词短语，能听见的倾倒声；audible 为 adj.，可听见的；pouring 为动名词，倾倒。

**简体中文译文**

## 2. 时间戳纪律

1. `[Shot 1]` 永远不带时间戳，只描述开场状态。
2. 此后的时间戳严格递增。14 字段式可用一位小数，如 `[00:09.8]`；Ref2VA 使用两位，如 `00:09.80`。
3. 只在真实状态变化处打时间戳：动作发起、受力、运镜动机起点、声音事件和剪辑点。禁止抒情式时间戳。
4. 事件写法为：`[时间] 触发 → 发起 → 扩张 → 重音 → 回收`；在句中嵌入同期声，如“伴随轻微的塑料咔哒声”“能听见倾倒声”。

## 04 · 时间戳纪律：衔接（源文第 30–30 行）

**词汇与术语**

本段没有需要另行释义的英文词项。

**简体中文译文**

5. 相邻事件用残余动量衔接，禁止中性姿势复位。

## 05 · 组装骨架：主体定义（源文第 32–35 行）

**词汇与术语**

- **subject** /ˈsʌbdʒɪkt/，n.，主体；**definition** /ˌdefɪˈnɪʃən/，n.，定义；**off-camera actor** /ˌɔːf ˈkæmərə ˈæktər/，名词短语，画外行动者。
- **never** /ˈnevər/，adv.，绝不；**fully shown** /ˈfʊli ʃoʊn/，动词短语，完整呈现；**vertical** /ˈvɜːrtɪkəl/，adj.，竖向的；**horizontal** /ˌhɔːrɪˈzɑːntəl/，adj.，横向的。

**简体中文译文**

## 3. 英文组装骨架的中文释义

原文把下列骨架标作“直接套”。以下中文块仅供理解；字段名、主体标签及比例占位符保持可对照。

```text
subject_definitions: <Subject 1> ……；<Subject 2> ……；<Subject N / off-camera actor> 始终不完整出镜：[可见部位／控制物件／每次入画的职能]。竖屏／横屏 X:Y。
```

## 06 · 组装骨架：环境定义（源文第 37–37 行）

**词汇与术语**

- **environment definition** /ɪnˈvaɪrənmənt ˌdefɪˈnɪʃən/，名词短语，环境定义；**space** /speɪs/，n.，空间；**architecture** /ˈɑːrkɪtektʃər/，n.，建筑。
- **ground** /ɡraʊnd/，n.，地面；**background objects** /ˈbækɡraʊnd ˈɑːbdʒekts/，名词短语，背景物件；**parked static props** /pɑːrkt ˈstætɪk prɑːps/，名词短语，停放不动的道具；**atmosphere** /ˈætməsfɪr/，n.，氛围；**explicit exclusions** /ɪkˈsplɪsɪt ɪkˈskluːʒənz/，名词短语，明确的排除项。

**简体中文译文**

```text
environment_definition: [空间、建筑、地面、背景物件、停放不动的道具、氛围、明确排除的事项]。
```

## 07 · 组装骨架：灯光定义（源文第 39–39 行）

**词汇与术语**

- **lighting definition** /ˈlaɪtɪŋ ˌdefɪˈnɪʃən/，名词短语，灯光定义；**key** /kiː/，adj./n.，主光；**direction** /dəˈrekʃən/，n.，方向；**quality** /ˈkwɑːləti/，n.，光质；**color temp** /ˈkʌlər temp/，名词短语，color temperature 的简写，色温。
- **ambient** /ˈæmbiənt/，adj.，环境的；**fill** /fɪl/，n.，补光；**shadow** /ˈʃædoʊ/，n.，阴影；**wet** /wet/，adj.，湿润的；**specular** /ˈspekjələr/，adj.，镜面反射的；**behavior** /bɪˈheɪvjər/，n.，表现；**grain** /ɡreɪn/，n.，颗粒；**constancy** /ˈkɑːnstənsi/，n.，恒定性。

**简体中文译文**

```text
lighting_definition: [主光方向＋光质＋色温，环境光／补光，阴影，湿表面／镜面反射表现，颗粒感，光照恒定性]。
```

## 08 · 组装骨架：综合多模态描述（源文第 41–41 行）

**词汇与术语**

- **integrated multimodal description** /ˈɪntɪɡreɪtɪd ˌmʌltiˈmoʊdəl dɪˈskrɪpʃən/，名词短语，综合多模态描述；**structural premise** /ˈstrʌktʃərəl ˈpremɪs/，名词短语，结构前提；**N-beat payoff** /en biːt ˈpeɪɔːf/，名词短语，N 个叙事拍后的效果落点；**material rule** /məˈtɪriəl ruːl/，名词短语，物质／材质行为规则。
- **opening state** /ˈoʊpənɪŋ steɪt/，名词短语，开场状态；**framing** /ˈfreɪmɪŋ/，n.，取景构图；**foreground/background anchors** /ˈfɔːrɡraʊnd ˈbækɡraʊnd ˈæŋkərz/，名词短语，前景／背景锚点。
- **trigger** /ˈtrɪɡər/，n./v.，触发；**action** /ˈækʃən/，n.，行动；**expansion** /ɪkˈspænʃən/，n.，扩张；**accent** /ˈæksent/，n.，重音／强调点；**recovery** /rɪˈkʌvəri/，n.，回收／恢复。
- **embedded diegetic sound** /ɪmˈbedɪd ˌdaɪəˈdʒetɪk saʊnd/，名词短语，嵌入动作句的场内同期声；**final timestamp** /ˈfaɪnəl ˈtaɪmstæmp/，名词短语，最后时间戳；**ending state** /ˈendɪŋ steɪt/，名词短语，结束状态。

**简体中文译文**

```text
integrated_multimodal_description: [用一句话交代：结构前提＋N 个叙事拍的效果落点＋物质／材质行为规则]。[Shot 1] [开场状态，不带时间戳；取景构图＋每个主体的状态＋前景／背景锚点]。[00:00.5] 触发→行动→扩张→重音→回收，句中嵌入同期声。……[最后时间戳] 结束状态。
```

## 09 · 组装骨架：相机指示（源文第 43–43 行）

**词汇与术语**

- **POV** /ˌpiː oʊ ˈviː/，abbr.，point of view /pɔɪnt əv vjuː/，视点；**holder** /ˈhoʊldər/，n.，持机者；**framing** /ˈfreɪmɪŋ/，n.，构图；**angle** /ˈæŋɡəl/，n.，角度。
- **baseline shake** /ˈbeɪslaɪn ʃeɪk/，名词短语，基线晃动；**range** /reɪndʒ/，n.，区间；**movement type** /ˈmuːvmənt taɪp/，名词短语，运动类型；**amplitude** /ˈæmplɪtuːd/，n.，幅度；**speed** /spiːd/，n.，速度。
- **small / medium / large** /smɔːl ˈmiːdiəm lɑːrdʒ/，adj.，小／中／大；**slow / medium / fast** /sloʊ ˈmiːdiəm fæst/，adj.，慢／中／快；**motivated by** /ˈmoʊtɪveɪtɪd baɪ/，分词短语（被动形式），由……提供动机；**body / event** /ˈbɑːdi ɪˈvent/，n.，身体／事件。
- **orbit** /ˈɔːrbɪt/，n./v.，环绕运镜；**zoom** /zuːm/，n./v.，变焦。

**简体中文译文**

```text
camera_direction: [视点／持机者，取景构图，角度，基线晃动]；[时间区间] 采用某种运镜，幅度为[小／中／大]，速度为[慢／中／快]，动机来自[身体动作／事件]；……；明确列出禁止环绕、禁止变焦等事项。
```

## 10 · 组装骨架：剪辑（源文第 45–45 行）

**词汇与术语**

- **editing** /ˈedɪtɪŋ/，n.，剪辑；**cut policy** /kʌt ˈpɑːləsi/，名词短语，切镜策略；**deliberate effect** /dɪˈlɪbərət ɪˈfekt/，名词短语，有意安排的特效。
- **in-point** /ˈɪn pɔɪnt/，n.，入点；**duration** /dʊˈreɪʃən/，n.，时长；**overlay recipe** /ˈoʊvərleɪ ˈresəpi/，名词短语，叠加配方；**snap-back** /ˈsnæp bæk/，n.，迅速恢复；**rhythm** /ˈrɪðəm/，n.，节奏；**allowed** /əˈlaʊd/，adj.，被允许的。

**简体中文译文**

```text
editing: [切镜策略]；每个有意安排的特效都写明：入点、时长、叠加配方、迅速恢复方式；N 个叙事拍的节奏；哪些行为不被允许。
```

## 11 · 组装骨架：表演（源文第 47–47 行）

**词汇与术语**

- **performance** /pərˈfɔːrməns/，n.，表演；**per-character arc** /pər ˈkærəktər ɑːrk/，名词短语，逐角色的发展弧线；**contrast design** /ˈkɑːntræst dɪˈzaɪn/，名词短语，反差设计。
- **exaggeration** /ɪɡˌzædʒəˈreɪʃən/，n.，夸张；**allowed / forbidden** /əˈlaʊd fərˈbɪdən/，adj.，允许的／禁止的；**posed faces** /poʊzd ˈfeɪsɪz/，名词短语，摆拍式表情；**constant smiling** /ˈkɑːnstənt ˈsmaɪlɪŋ/，名词短语，持续微笑；**lip-sync** /ˈlɪp sɪŋk/，n./v.，对口型；**as applicable** /æz əˈplɪkəbəl/，状语短语，视适用情况。

**简体中文译文**

```text
performance: [逐角色的发展弧线]；反差设计；哪些位置允许／禁止夸张；根据具体情况规定不得出现摆拍式表情、持续微笑或对口型。
```

## 12 · 组装骨架：身体运动机制（源文第 49–49 行）

**词汇与术语**

- **body mechanics** /ˈbɑːdi məˈkænɪks/，名词短语，身体运动机制；**wind-up** /ˈwaɪnd ʌp/，n.，动作前的蓄力；**release** /rɪˈliːs/，n.，发力／释放；**force transmission chain** /fɔːrs trænzˈmɪʃən tʃeɪn/，名词短语，力传导链。
- **drinking kinetics** /ˈdrɪŋkɪŋ kɪˈnetɪks/，名词短语，饮水动作的动力学；**raise arm** /reɪz ɑːrm/，动词短语，抬臂；**tilt back** /tɪlt bæk/，动词短语，后仰；**swallow** /ˈswɑːloʊ/，v.，吞咽；**lower** /ˈloʊər/，v.，放低。
- **grounded feet** /ˈɡraʊndɪd fiːt/，名词短语，稳踏地面的双脚；**floating** /ˈfloʊtɪŋ/，n./adj.，漂浮／漂浮的。

**简体中文译文**

```text
body_mechanics: [每次发力前先蓄力]；力传导链；饮水动作动力学为抬臂→后仰→吞咽→放低；双脚稳踏地面，不得漂浮。
```

## 13 · 组装骨架：服装与头发物理表现（源文第 51–51 行）

**词汇与术语**

- **costume / hair / physics** /ˈkɑːstuːm her ˈfɪzɪks/，n.，服装／头发／物理规律；**lag** /læɡ/，n.，滞后；**wet evolution** /wet ˌevəˈluːʃən/，名词短语，湿润状态的逐步变化。
- **fabric weight** /ˈfæbrɪk weɪt/，名词短语，面料重量；**darken and cling** /ˈdɑːrkən ənd klɪŋ/，并列动词短语，颜色变深并贴附；**glasses slide/fog** /ˈɡlæsɪz slaɪd fɑːɡ/，主谓短语，眼镜滑动／起雾；**visor resistance** /ˈvaɪzər rɪˈzɪstəns/，名词短语，面罩的阻力。
- **animate independently** /ˈænɪmeɪt ˌɪndɪˈpendəntli/，动词短语，独立自行运动。

**简体中文译文**

```text
costume_hair_physics: [每个角色的头发滞后运动与湿润状态演化]；[面料重量，遇水变深并贴附身体]；[眼镜滑动／起雾；面罩阻力]；任何物件都不得脱离物理原因自行运动。
```

## 14 · 组装骨架：负面约束（源文第 53–53 行）

**词汇与术语**

- **negative constraints** /ˈneɡətɪv kənˈstreɪnts/，名词短语，负面约束、禁止事项；字段键为 `negative_constraints`，文中也简称 negative。
- **focused list** /ˈfoʊkəst lɪst/，名词短语，聚焦的清单；**extra people** /ˈekstrə ˈpiːpəl/，名词短语，额外人物；**added props beyond X** /ˈædɪd prɑːps bɪˈjɑːnd eks/，名词短语，X 之外增加的道具；**costume swap** /ˈkɑːstuːm swɑːp/，名词短语，服装替换。
- **style drift** /staɪl drɪft/，名词短语，风格漂移；**forbidden camera** /fərˈbɪdən ˈkæmərə/，名词短语，禁止的相机行为；**ordinary cuts** /ˈɔːrdəneri kʌts/，名词短语，普通切镜；**subtitles / watermark** /ˈsʌbtaɪtəlz ˈwɔːtərmɑːrk/，n.，字幕／水印。
- **blood** /blʌd/，n.，血；**effect residue** /ɪˈfekt ˈrezɪduː/，名词短语，特效残留；**freeze outside beats** /friːz ˌaʊtˈsaɪd biːts/，动词短语，在指定节奏点以外定格；**identity change** /aɪˈdentəti tʃeɪndʒ/，名词短语，身份变化。

**简体中文译文**

```text
negative_constraints: [聚焦的清单：不增加人物；不增加 X 之外的道具；不换服装；不出现风格漂移；不使用被禁止的相机行为；不出现普通切镜；不出现字幕／水印；不出现血；不残留特效；不在指定节奏点以外定格；不改变身份]。
```

## 15 · 组装骨架：总体声景（源文第 55–55 行）

**词汇与术语**

- **overall soundscape** /ˌoʊvərˈɔːl ˈsaʊndskeɪp/，名词短语，总体声景；**ambient bed** /ˈæmbiənt bed/，名词短语，环境声音底层；**ordered diegetic cues** /ˈɔːrdərd ˌdaɪəˈdʒetɪk kjuːz/，名词短语，按顺序排列的场内声音提示。
- **per-freeze post-SFX** /pər friːz poʊst ˌes ef ˈeks/，名词短语，每次定格的后期音效；**unpolished field-recording note** /ʌnˈpɑːlɪʃt fiːld rɪˈkɔːrdɪŋ noʊt/，名词短语，保留未经精修的现场录音质感的说明。
- **SFX** /ˌes ef ˈeks/，abbr.，sound effects /saʊnd ɪˈfekts/，音效；本项目声音语境下指声音效果，勿与视觉特效混同。

**简体中文译文**

```text
overall_soundscape: [环境声音底层]；按顺序给出场内声音提示：“在 X.X 秒……”；每次定格对应的后期音效；说明保留未经精修的现场录音质感。
```

## 16 · 组装骨架：画外配乐（源文第 57–58 行）

**词汇与术语**

- **non-diegetic music** /ˌnɑːn ˌdaɪəˈdʒetɪk ˈmjuːzɪk/，名词短语，画外配乐；**fully copy** /ˈfʊli ˈkɑːpi/，动词短语，完整复制；**audio** /ˈɔːdioʊ/，n.，音频。
- **target music spec** /ˈtɑːrɡɪt ˈmjuːzɪk spek/，名词短语，目标音乐规格，spec 是 specification /ˌspesɪfɪˈkeɪʃən/ 的简写；**explicit silence** /ɪkˈsplɪsɪt ˈsaɪləns/，名词短语，明确静默；**throughout** /θruːˈaʊt/，adv.，全程。

**简体中文译文**

```text
non_diegetic_music: [完整复制 <Audio N>，标记为 fully_copy。]／[目标音乐规格]／[没有画外配乐。音乐层全程明确保持静默；……]。
```

## 17 · 三层声音分离速查（源文第 60–66 行）

**词汇与术语**

- **integrated multimodal description** /ˈɪntɪɡreɪtɪd ˌmʌltiˈmoʊdəl dɪˈskrɪpʃən/，名词短语，综合多模态描述；**overall soundscape** /ˌoʊvərˈɔːl ˈsaʊndskeɪp/，名词短语，总体声景；**non-diegetic music** /ˌnɑːn ˌdaɪəˈdʒetɪk ˈmjuːzɪk/，名词短语，画外配乐。
- **BGM** /ˌbiː dʒiː ˈem/，abbr.，background music /ˈbækɡraʊnd ˈmjuːzɪk/，背景音乐。
- **explicit silence** /ɪkˈsplɪsɪt ˈsaɪləns/，名词短语，明确静默；**N/A** /ˌen ˈeɪ/，abbr.，not applicable /nɑːt əˈplɪkəbəl/，不适用。

**简体中文译文**

## 4. 三层声音分离速查

| 声音类型 | 例子 | 唯一允许的字段 |
|---|---|---|
| 动作同期声 | 吞咽、面罩咔哒、喷水、呛咳、脚步 | 嵌入 `integrated_multimodal_description`（综合多模态描述）中对应的动作句。 |
| 环境／特效总览 | 夜巷底噪、怠速、风、定格特效音序列 | `overall_soundscape`（总体声景）。 |
| 音乐层 | 背景音乐、配乐、歌曲 | 仅放在 `non_diegetic_music`（画外配乐）；无音乐时明确写“静默”，或标 `N/A`（不适用）。 |

## 18 · 首帧锚定模式调整（源文第 68–70 行）

**词汇与术语**

- **target video** /ˈtɑːrɡɪt ˈvɪdioʊ/，名词短语，目标视频；**fully referenced** /ˈfʊli ˈrefərənst/，分词短语（被动形式），完整作为参考；**picture** /ˈpɪktʃər/，n.，图片；**shot** /ʃɑːt/，n.，镜头。
- **visual anchor** /ˈvɪʒuəl ˈæŋkər/，名词短语，视觉锚点；**environment / lighting / subject** /ɪnˈvaɪrənmənt ˈlaɪtɪŋ ˈsʌbdʒɪkt/，n.，环境／灯光／主体。I2VA 是本文的首帧图引导模式代号。

**简体中文译文**

## 5. I2VA／FL2VA／L2VA 调整

**I2VA 首帧锚定**：在开头添加句子，其完整中文意思是：“对于目标视频，在目标视频开始后的 0.00 秒处，完整参考 `<Picture 1>`（来自 `[Shot 1]`）。”添加 `visual_anchor`（视觉锚点），省略环境与灯光的文字字段；主体以图片为唯一视觉权威，只保留极简的身份锚点，即轮廓、运动结构与整体色调。

## 19 · 首尾帧模式调整（源文第 71–71 行）

**词汇与术语**

- **first-frame state** /fɜːrst freɪm steɪt/，名词短语，首帧状态；**observable intermediate changes** /əbˈzɜːrvəbəl ˌɪntərˈmiːdiət ˈtʃeɪndʒɪz/，名词短语，可观察到的中间变化。FL2VA 为首尾帧引导模式代号。

**简体中文译文**

**FL2VA**：补充从“首帧状态 → 可观察到的中间变化 → 收敛至尾帧”的连续路径，倾向采用单镜头。

## 20 · 仅尾帧模式调整（源文第 72–72 行）

**词汇与术语**

- **L2VA**，模式代号，本文指仅尾帧引导生成；last /læst/，adj.，最后的。

**简体中文译文**

**L2VA**：从给定尾帧反推合理的开场状态，让动作、物体和构图逐步收敛到尾帧。

## 21 · 目标音乐设计字段（源文第 74–76 行）

**词汇与术语**

- **genre** /ˈʒɑːnrə/，n.，流派；**key** /kiː/，n.，调性；**instrumentation architecture** /ˌɪnstrəmenˈteɪʃən ˈɑːrkɪtektʃər/，名词短语，配器架构。
- **BPM** /ˌbiː piː ˈem/，abbr.，beats per minute /biːts pər ˈmɪnɪt/，每分钟拍数。
- **musical structure** /ˈmjuːzɪkəl ˈstrʌktʃər/，名词短语，音乐结构；**dynamics arc** /daɪˈnæmɪks ɑːrk/，名词短语，力度发展弧线；**synchronization** /ˌsɪŋkrənəˈzeɪʃən/，n.，同步；**vocals** /ˈvoʊkəlz/，n. pl.，人声；**production** /prəˈdʌkʃən/，n.，制作处理。
- **non-diegetic music** /ˌnɑːn ˌdaɪəˈdʒetɪk ˈmjuːzɪk/，名词短语，画外配乐，对应字段 `non_diegetic_music`。

**简体中文译文**

## 6. 目标音乐设计字段（确实需要配乐时，原文称“十项写法”）

流派／每分钟拍数／调性／配器架构／音乐结构／力度发展弧线／同步关系／人声／制作处理：把这些内容作为创作目标，一次性写入 `non_diegetic_music`。音乐全程连续，不中断、不拆成相互割裂的段落；不得把音乐写入画面描述。

译注：原文标题写“十项”，实际列出九项；此处如实保留，不自行补造第十项。
