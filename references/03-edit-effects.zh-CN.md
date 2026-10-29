# 03 — 剪辑、定格与漫画叠加特效｜简体中文释义版

源文件：`references/03-edit-effects.md`。源版本：`7371c753ff4a087ca411e12033a3314231bd28c8`。

本文件是独立的简体中文释义阅读版，按源文顺序先释义、后翻译；原始文件不作改动。命令、字段键、路径与引用标签保留原样，中文用于解释其含义；自然语言英文提示词均给出完整中文译文。此阅读版不是替代原始英文提示词或可执行技能的配置文件。音标采用常见英语读音；专有工具名、路径和代码符号不虚构统一读音。n.＝名词，v.＝动词，adj.＝形容词，adv.＝副词，phr.＝短语，abbr.＝缩略语。

## 01 · 标题与四层分离（源文第 1–9 行）

**词汇与术语**

- **integrated multimodal description** /ˈɪntɪɡreɪtɪd ˌmʌltiˈmoʊdəl dɪˈskrɪpʃən/，名词短语，综合多模态描述；**detailed description** /ˈdiːteɪld dɪˈskrɪpʃən/，名词短语，详细描述；**Ref2VA** 为全参考生成模式代号，reference /ˈrefərəns/，n.，参考。
- **camera direction** /ˈkæmərə dəˈrekʃən/，名词短语，相机与运镜指示；**editing** /ˈedɪtɪŋ/，n.，剪辑；**overall soundscape** /ˌoʊvərˈɔːl ˈsaʊndskeɪp/，名词短语，总体声景；**non-diegetic music** /ˌnɑːn ˌdaɪəˈdʒetɪk ˈmjuːzɪk/，名词短语，画外配乐。

**简体中文译文**

# 03 — 剪辑、定格、漫画叠加特效的识别与写法

## 1. 先分层：现场动作不等于后期特效

把成片拆为四层，分别放入相应字段：

1. **现场动作层**：人物真实做了什么 → `integrated_multimodal_description`（综合多模态描述），或 Ref2VA 的 `detailed_description`（详细描述）。
2. **运镜层** → `camera_direction`（相机指示）。
3. **剪辑特效层**：定格、白闪、漫画图形、变速、转场 → `editing`（剪辑）。
4. **声音层** → `overall_soundscape`（总体声景）与 `non_diegetic_music`（画外配乐）。

## 02 · 常见分层错误（源文第 11–11 行）

**词汇与术语**

本段没有需要另行释义的英文词项。

**简体中文译文**

最常见错误：把后期定格写成"人物停住不动"，把漫画集中线写成现场背景。

## 03 · 定格的识别判据（源文第 13–15 行）

**词汇与术语**

- **freeze-frame** /ˈfriːz freɪm/，n.，定格画面；freeze 为 v.，冻结；frame 为 n.，帧。
- **punch-in** /ˈpʌntʃ ɪn/，n.，短促推进／突然收紧取景；本段指幅度很小的画面推近。s 为 second /ˈsekənd/（n.，秒）的单位符号。

**简体中文译文**

## 2. 定格识别

判据需同时满足：连续多帧的像素近乎不变，持续约 0.3–0.8 秒；常伴随一帧白闪或黑闪、轻微的突然推近、图形叠加或声音“真空”；前后动作仍连续，并非通过硬切换到另一场景。

## 04 · 每次定格的四个记录要素（源文第 17–21 行）

**词汇与术语**

- **RMS** /ˌɑːr em ˈes/，abbr.，root mean square /ruːt miːn skwer/，均方根；这里用来描述音频的短时能量包络。
- **accent** /ˈæksent/，n./修饰语，强调、突出；accent color 指强调色。
- **snap off** /snæp ɔːf/，动词短语，迅速撤去／突然消失；此处指叠加效果在数帧内清除。

**简体中文译文**

每个定格记录**四要素**：

1. **入点**：精确到 0.1 秒，并与均方根能量峰对齐校验。
2. **时长**：通常为 0.5–0.6 秒。
3. **叠加层**：白闪、集中线、网点、拟声字、冲击星、汗滴、边框、强调色。
4. **恢复实拍的方式**：在数帧内迅速撤去叠加，无残留，并恢复正常速度与色彩。

## 05 · 简单白闪定格：时间线示例（源文第 23–29 行）

**词汇与术语**

- **freeze-frame gag** /ˈfriːz freɪm ɡæɡ/，名词短语，定格笑点／定格喜剧桥段；**image locks** /ˈɪmɪdʒ lɑːks/，主谓短语，画面锁定；**roughly half a second** /ˈrʌfli hæf ə ˈsekənd/，名词短语，大约半秒。
- **tiny punch-in zoom** /ˈtaɪni ˈpʌntʃ ɪn zuːm/，名词短语，极小幅度的突然变焦推近；**single white flash** /ˈsɪŋɡəl waɪt flæʃ/，名词短语，一次白闪。
- **comedic shock hold** /kəˈmiːdɪk ʃɑːk hoʊld/，名词短语，具有喜剧惊愕效果的停顿；**motion resumes** /ˈmoʊʃən rɪˈzuːmz/，主谓短语，动作恢复。

**简体中文译文**

## 3. 简单白闪定格（无漫画元素）

写入时间线的中文对应如下：

```text
[00:06.2] 定格笑点 1：画面在[被定格画面]上锁定大约半秒，极小幅度的突然变焦推近与一次白闪标示该定格，形成具有喜剧惊愕效果的停顿。
[00:06.8] 动作恢复：[恢复动作]。
```

## 06 · 简单白闪定格：剪辑汇总（源文第 30–33 行）

**词汇与术语**

- **editing** /ˈedɪtɪŋ/，n.，剪辑；**deliberate** /dɪˈlɪbərət/，adj.，有意安排的；**comedic** /kəˈmiːdɪk/，adj.，喜剧性的。
- **freeze-frame holds** /ˈfriːz freɪm hoʊldz/，名词短语，定格停顿；**accented by** /ˈæksentɪd baɪ/，分词短语（被动形式），由……加以强调；**micro punch-in zoom** /ˈmaɪkroʊ ˈpʌntʃ ɪn zuːm/，名词短语，微幅突然变焦推近。
- **one-frame white flash** /wʌn freɪm waɪt flæʃ/，名词短语，持续一帧的白闪；**cleanly resumes** /ˈkliːnli rɪˈzuːmz/，动词短语，干净利落地恢复；**three-beat shock-gag rhythm** /θriː biːt ʃɑːk ɡæɡ ˈrɪðəm/，名词短语，三拍式惊愕笑点节奏。

**简体中文译文**

`editing`（剪辑）汇总的中文对应如下：

```text
在[…]处有意安排三次喜剧性定格停顿，每次约 0.5 秒；每次都用微幅的突然变焦推近和持续一帧的白闪加以强调，随后干净利落地恢复动作，形成经典的三拍式惊愕笑点节奏。
```

## 07 · 漫画叠加定格：统一制作规则（源文第 35–45 行）

**词汇与术语**

- **manga** /ˈmæŋɡə/，n.，日本漫画；**post-VFX** /poʊst ˌviː ef ˈeks/，名词短语，后期视觉特效；VFX 是 visual effects /ˈvɪʒuəl ɪˈfekts/ 的缩写；**recipe** /ˈresəpi/，n.，配方／处理方案。
- **live action** /laɪv ˈækʃən/，名词短语，真人实拍；**hard-freezes** /hɑːrd ˈfriːzɪz/，v.，第三人称单数，骤然完全定格；**stylized** /ˈstaɪlaɪzd/，adj.，经过风格化处理的；**panel** /ˈpænəl/，n.，漫画格。
- **heavy black ink outlines** /ˈhevi blæk ɪŋk ˈaʊtlaɪnz/，名词短语，粗重的黑色墨线轮廓；**high-contrast** /ˌhaɪ ˈkɑːntræst/，adj.，高对比度的；**B&W**，abbr.，black and white /blæk ənd waɪt/，黑白；**grading** /ˈɡreɪdɪŋ/，n.，调色。
- **screentone / halftone dot shading** /ˈskriːntoʊn ˈhæftoʊn dɑːt ˈʃeɪdɪŋ/，名词短语，网点纸／半色调点状阴影；**thick black panel border** /θɪk blæk ˈpænəl ˈbɔːrdər/，名词短语，粗黑漫画格边框。
- **2D graphic elements** /ˌtuː ˈdiː ˈɡræfɪk ˈelɪmənts/，名词短语，二维图形元素；2D 为 two-dimensional /ˌtuː dɪˈmenʃənəl/ 的缩写；**radial concentration lines** /ˈreɪdiəl ˌkɑːnsənˈtreɪʃən laɪnz/，名词短语，放射集中线。
- **impact starburst** /ˈɪmpækt ˈstɑːrbɜːrst/，名词短语，冲击星爆；**screeching speed lines** /ˈskriːtʃɪŋ spiːd laɪnz/，名词短语，带有尖锐冲刺感的速度线；**bold outlined onomatopoeia** /boʊld ˈaʊtlaɪnd ˌɑːnəˌmætəˈpiːə/，名词短语，粗体描边拟声字；**exaggeration symbol** /ɪɡˌzædʒəˈreɪʃən ˈsɪmbəl/，名词短语，夸张符号。
- **accent color** /ˈæksent ˈkʌlər/，名词短语，强调色；**monochrome** /ˈmɑːnəkroʊm/，adj./n.，单色的／单色表现；**pop-and-shake** /pɑːp ənd ʃeɪk/，名词性组合，弹出后抖动；**snaps away** /snæps əˈweɪ/，动词短语，迅速消失。
- **photorealistic** /ˌfoʊtoʊriːəˈlɪstɪk/，adj.，照片级写实的；**residue** /ˈrezɪduː/，n.，残留；**editing** /ˈedɪtɪŋ/，n.，剪辑。

**简体中文译文**

## 4. 漫画叠加定格（需要漫画风格时）

### 4.1 把统一制作规则写入 `editing`（剪辑）

```text
每一次定格都遵循同一套漫画后期视觉特效方案：
（1）真人实拍画面骤然完全定格；
（2）定格画面立即风格化为日本漫画格：粗重的黑色墨线轮廓、高对比度黑白调色、网点纸／半色调点状阴影，以及粗黑漫画格边框；
（3）二维图形元素叠加在定格画面之上，并爆发出现：放射集中线／冲击星爆／尖锐冲刺感速度线，一个粗体描边拟声词，以及一个夸张符号；
（4）每个笑点严格只保留一种强调色，其余部分全部变为漫画式单色；
（5）图形只做一次快速弹出与抖动，随后叠加层在数帧内迅速消失；正常的全彩、照片级写实真人实拍恢复，不留下任何残余。
```

## 08 · 三种递进漫画元素配方（源文第 47–52 行）

**词汇与术语**

- **accent color** /ˈæksent ˈkʌlər/，名词短语，强调色；**splat** /splæt/，n./感叹词，湿物撞击或液体拍溅的“啪叽／噗”的声音；**cough** /kɔːf/，n./v.，咳嗽，作为拟声字可译“咳咳”。

**简体中文译文**

### 4.2 三种递进的漫画元素配方

| 情绪 | 线条 | 拟声字（可换日文／中文） | 夸张符号 | 强调色 |
|---|---|---|---|---|
| 自作自受、震惊 | 放射集中线 | `!?` | 大汗滴、汗线 | 角色标识色 1 |
| 误伤、命中 | 锯齿星爆环＋冲击放射线 | `SPLAT!!`，即“啪叽！！／噗！！” | 叉形爆点、描边水滴 | 被击中者的服装色 |
| 急停、呛住 | 横向速度线堆叠，形成刹车感 | `COUGH!!`，即“咳咳！！” | 头顶裂痕闪电、青筋 | 道具色 |

## 09 · 拟声字替换与字幕边界（源文第 54–54 行）

**词汇与术语**

- **negative** /ˈneɡətɪv/，adj./字段简称，负面约束。
- **graphic SFX typography** /ˈɡræfɪk ˌes ef ˈeks taɪˈpɑːɡrəfi/，名词短语，图形化音效字；**sentence subtitles** /ˈsentəns ˈsʌbtaɪtəlz/，名词短语，完整句式字幕；**never** /ˈnevər/，adv.，绝不。
- **SFX** /ˌes ef ˈeks/，abbr.，sound effects /saʊnd ɪˈfekts/，音效；本项目声音语境下指声音效果，勿与视觉特效混同。

**简体中文译文**

拟声字可改为日文 `ズビシャ!! / ゴホッ!!`，或中文 `噗！！/ 咳咳！！`；但必须在负面约束中声明：“使用图形化的音效文字，绝不使用完整句式字幕。”日文拟声字沿用原文，非英语词项。

## 10 · 防止风格漂移的约束（源文第 56–63 行）

**词汇与术语**

- **negative constraints** /ˈneɡətɪv kənˈstreɪnts/，名词短语，负面约束、禁止事项；字段键为 `negative_constraints`，文中也简称 negative。
- **anime** /ˈænɪmeɪ/，n.，日本动画；**live action** /laɪv ˈækʃən/，名词短语，真人实拍；**photorealistic** /ˌfoʊtoʊriːəˈlɪstɪk/，adj.，照片级写实的。
- **manga residue** /ˈmæŋɡə ˈrezɪduː/，名词短语，漫画效果残留；**overlay snaps off** /ˈoʊvərleɪ snæps ɔːf/，主谓短语，叠加层突然撤去；**specified beats** /ˈspesɪfaɪd biːts/，名词短语，指定节奏点。
- **onomatopoeia** /ˌɑːnəˌmætəˈpiːə/，n.，拟声词；**typography** /taɪˈpɑːɡrəfi/，n.，文字图形与排版；**oversized cartoon water** /ˌoʊvərˈsaɪzd kɑːrˈtuːn ˈwɔːtər/，名词短语，尺寸夸大的卡通水体；**live footage** /laɪv ˈfʊtɪdʒ/，名词短语，实拍影像；**stylization** /ˌstaɪləˈzeɪʃən/，n.，风格化。

**简体中文译文**

### 4.3 防止漂移（写入 `negative_constraints`）

```text
不得把整条视频变成动画；定格之外的真人实拍必须保持照片级写实；
每次叠加层撤去后，不得残留漫画效果；
不得在指定节奏点之外出现定格或漫画特效；
拟声字必须是图形化音效文字，绝不能是完整句式字幕；
实拍影像中不得出现尺寸夸大的卡通水体；卡通风格化只能存在于定格叠加层内部。
```

## 11 · 其他剪辑形态：一镜到底（源文第 65–67 行）

**词汇与术语**

- **one unbroken take** /wʌn ʌnˈbroʊkən teɪk/，名词短语，一个不中断的连续镜头；**hard cuts** /hɑːrd kʌts/，名词短语，硬切；**dissolves** /dɪˈzɑːlvz/，n. pl.，叠化转场；**speed ramps** /spiːd ræmps/，n. pl.，渐变速度处理。

**简体中文译文**

## 5. 其他剪辑形态

**一镜到底**：英文约束的完整意思是：“一个不中断的连续镜头，不硬切、不叠化、不做渐变速度处理。”景别变化仅通过手持移动实现。

## 12 · 其他剪辑形态：硬切（源文第 68–68 行）

**词汇与术语**

- **match-on-action** /mætʃ ɑːn ˈækʃən/，名词短语，动作匹配剪辑，即跨切点保持动作连续。
- **cut** /kʌt/，n./v.，切镜；**shot syntax** /ʃɑːt ˈsɪntæks/，名词短语，镜头语法。

**简体中文译文**

**硬切**：只在有意义的视觉变化处切镜，并使用动作匹配剪辑，保持方向、速度与动量连续；禁止机械地按秒数切镜。多镜头的切镜语法见 `shot-syntax.md`。

## 13 · 其他剪辑形态：变速（源文第 69–69 行）

**词汇与术语**

- **slomo** /ˈsloʊ moʊ/，n.，slow motion /sloʊ ˈmoʊʃən/ 的缩写，慢动作。

**简体中文译文**

**变速**：只有明确观察到慢动作时才写慢动作；必须写清减速区间与恢复点。定格不等于慢动作。

## 14 · 其他剪辑形态：转场（源文第 70–70 行）

**词汇与术语**

本段没有需要另行释义的英文词项。

**简体中文译文**

- **转场**：优先用运镜/能量变化表达段落边界。

## 15 · 定格特效音的完整写法（源文第 72–78 行）

**词汇与术语**

- **overall soundscape** /ˌoʊvərˈɔːl ˈsaʊndskeɪp/，名词短语，总体声景；**each freeze frame** /iːtʃ friːz freɪm/，名词短语，每一个定格。
- **record-scratch** /ˈrekərd skrætʃ/，n.，唱片刮擦声；**rewind squeal** /ˌriːˈwaɪnd skwiːl/，名词短语，倒带尖啸声；**leading into** /ˈliːdɪŋ ˈɪntuː/，分词短语，引入、衔接至。
- **punchy impact hit** /ˈpʌntʃi ˈɪmpækt hɪt/，名词短语，有力的冲击音；**crisp percussive** /krɪsp pərˈkʌsɪv/，adj.，清脆且有打击感的；**DON**，拟声写法，可译“咚”，不作为普通英语词虚构音标；**comic pop tail** /ˈkɑːmɪk pɑːp teɪl/，名词短语，带喜剧感的爆破尾音。
- **roughly half-second near-silence vacuum** /ˈrʌfli hæf ˈsekənd nɪr ˈsaɪləns ˈvækjuəm/，名词短语，大约半秒的近乎无声真空；**ambient sound snapping back** /ˈæmbiənt saʊnd ˈsnæpɪŋ bæk/，名词与分词组成的结构，环境声瞬间恢复；**the instant it clears** /ði ˈɪnstənt ɪt klɪrz/，时间状语结构，定格清除的那个瞬间。

**简体中文译文**

## 6. 定格特效音（写入 `overall_soundscape`，不是音乐字段）

```text
每一次定格开始时：先出现短促的唱片刮擦声／倒带尖啸声，再接上有力的冲击音——清脆、有打击感的一声“咚”，带着喜剧式爆破尾音；随后在定格停留期间，出现大约半秒、接近无声的声音真空。定格一结束，环境声立即恢复。
```
