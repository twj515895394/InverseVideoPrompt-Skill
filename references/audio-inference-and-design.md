# 视频声音反推与声音设计

本参考文件用于在反推视频提示词时处理声音层。目标不是凭空编造“原视频一定存在的声音”，而是根据可用证据区分：**实际听到的声音、从画面推测的声音、为了生成或后期复刻而推荐的声音设计**。

## 1. 三层声音结论

所有声音结论优先使用以下三层标签：

- **已确认（Observed）**：原视频音轨中可以直接听见，或用户明确提供。
- **高概率推测（Inferred）**：虽然没有可靠音轨，但由清晰可见的动作、环境或事件强烈支持。
- **创作推荐（Recommended）**：原视频是否存在无法确认，但为了增强节奏、空间感、冲击感或叙事效果，建议在生成或后期加入。

不要把 Recommended 写成对原视频事实的描述。

## 2. 声音分析维度

按以下六类检查声音：

### A. Dialogue / Vocal

检查：

- 对白、旁白、喊叫、耳语、笑声、喘息、哭声、群体呼喊
- 说话者位置与距离
- 口型是否可见、是否需要 lip sync
- 声音情绪、语速、停顿、气息强弱
- 是否应保持无对白

若只能看到人物张嘴，不应自动生成具体台词。可以写“可能有一句短促喊声/对白”，但不要杜撰句子内容。

### B. Foley / Action SFX

根据可见动作推测同步拟音：

- 脚步、衣料摩擦、呼吸
- 手掌接触、抓取、推门、放置物品
- 武器挥动、碰撞、金属摩擦
- 机械按键、旋钮、卡扣、零件装配
- 跌落、撞击、碎裂、滚动
- 水花、沙土、树叶、火焰等材质反馈

声音必须与动作材质、重量、速度和距离匹配。

### C. Environmental Ambience

根据环境建立持续空间底噪：

- 室内 room tone、空调、电流、机器低鸣
- 城市交通、人群、远处警笛
- 森林虫鸣、鸟鸣、风吹树叶
- 海边浪声、风声
- 雨、雷、电气环境
- 大型空间混响、地下空间低频回声

Ambience 的作用是建立空间，不应抢占主体动作声音。

### D. Cinematic / Designed SFX

识别或推荐非自然主义的电影化声音设计：

- whoosh / swish
- riser
- sub-bass hit
- impact boom
- reverse swell
- low-frequency rumble
- transition sweep
- glitch / digital pulse
- energy charge
- tonal drone

这类声音通常用于强化运镜、转场、揭示、冲击点和节奏，而不是现实世界自然声。

### E. Music

反推或推荐：

- 有无配乐
- 音乐类型与质感，而不是具体受版权保护的曲目
- 节拍密度、速度感、强弱变化
- 主导乐器或音色族群
- 情绪功能
- 与剪辑/动作是否同步
- 是否在关键事件前留白、抽空、骤停或进入高潮

优先写“低沉电子脉冲 + 缓慢上升的氛围合成器”这类生成导向描述，不要默认指定现成歌曲。

### F. Silence / Dynamic Contrast

沉默也是声音设计的一部分。检查：

- 动作前是否短暂停顿
- 冲击前是否抽掉环境声或音乐
- 揭示后是否留白
- 是否通过 sudden silence 强化后续 impact

不要为了“丰富”而给每一秒塞满声音。

## 3. 从视觉推测声音的规则

### 强证据

以下事件通常可以给出高置信度声音推测：

- 可见脚落地 → 对应材质脚步
- 门明显关闭 → 门体/锁舌声
- 两物体明确碰撞 → impact/contact
- 雨水明显击打环境 → rain ambience
- 枪口可见开火 → 枪声/机械动作（具体类型不确定时不要过度精确）
- 爆炸视觉事件 → blast + low-end impact + debris tail
- 玻璃明确碎裂 → glass break

### 中等证据

可以推荐但需要保守：

- 快速挥臂/挥剑 → whoosh 或空气切割声
- 快速推拉/甩镜 → subtle camera whoosh
- 光能积聚 → tonal rise / energy charge
- 大型物体经过 → low-frequency pass-by
- 紧张特写 → low drone / heartbeat-like pulse 作为创作推荐

### 弱证据

不要从下列情况直接断言具体声音：

- 人物张嘴但听不到音轨 → 不生成具体台词
- 远处车辆 → 不确定是否能实际听清引擎
- 静态霓虹灯 → 不自动添加明显电流噪声
- 画面慢动作 → 不自动认定原视频使用低频拉伸音效

## 4. 声音与时间线绑定

声音设计必须跟随 Shot 与 Action Phase，而不是单独列一个无时间关系的音效清单。

推荐结构：

```text
0.0-1.8s  Ambiente: quiet industrial room tone, distant ventilation hum
1.8-2.4s  Foley: two fast footsteps approaching
2.4s      Sync SFX: metal door slam
2.4-3.0s  Designed SFX: short sub-bass impact, followed by room reverb tail
3.0-4.5s  Music: tense pulse rises slightly, then cuts before the reveal
```

对于连续动作：

```text
anticipation → subtle cloth movement + breath intake
execution → fast whoosh synchronized to arm motion
impact → dry contact hit + short low-frequency accent
recovery → debris/cloth tail + ambience returns
```

## 5. 声音与运镜联动

不要把每次运镜都机械地加 whoosh。仅在视觉速度、剪辑风格或参考音频支持时使用。

可考虑：

- whip pan → short directional whoosh
- fast push-in → restrained tonal rise or air movement
- crash zoom → sharp accent / transient hit
- reveal/orbit completion → tonal resolve or subtle impact
- hard cut → 可无声音过渡，也可用 cut hit；取决于整体风格
- montage cut → beat-synced click/impact/foley 可以增强节奏

声音应服务镜头，不要让镜头运动被声音设计绑死。

## 6. 空间与声学属性

声音推荐至少考虑：

- 距离：near / mid / far
- 方位：left / center / right / off-screen
- 空间：dry / small room / large hall / exterior open space
- 混响长度与强弱
- 高频衰减和遮挡感
- 远近层次

例如：

```text
Close footsteps remain dry and centered; distant crowd ambience is diffuse and low in the mix; the impact carries a short metallic reverb matching the warehouse interior.
```

## 7. 原声复刻与创作增强分开输出

默认同时给两部分：

### A. 推测原声（Likely Source Audio）

只放：

- 已确认声音
- 有明显视觉证据的高概率声音
- 必要的不确定性说明

### B. 推荐声音设计（Recommended Sound Design）

为了更适合 AI 生成或后期制作，可以主动推荐：

- ambience 层
- 同步 Foley
- cinematic accents
- 音乐情绪与节奏
- silence / dynamic contrast

这样用户可以清楚知道哪些是“复刻”，哪些是“增强”。

## 8. 最终声音输出模板

```text
### 声音反推
- 已确认：...
- 高概率推测：...
- 不确定：...

### 推荐声音设计
- 环境底噪：...
- 动作拟音：...
- 电影化音效：...
- 音乐：...
- 动态/留白：...

### 时间线
- 0.0-2.0s: ...
- 2.0-3.5s: ...
- 3.5-5.0s: ...
```

如果目标视频模型支持原生音频生成，可将必要声音描述编译进最终视频 Prompt；如果模型主要生成无声视频，则把声音块作为独立的 **Audio / Sound Design Prompt** 输出，供后续音频生成或剪辑使用。

## 9. 质量检查

返回前检查：

- 是否清楚区分“听到 / 推测 / 推荐”？
- 是否给动作事件绑定了对应声音时点？
- 是否考虑空间、距离、材质和重量？
- 是否存在无意义的 whoosh/impact 堆叠？
- 音乐是否在描述功能和节奏，而不是只写“cinematic music”？
- 是否使用 silence 和 dynamic contrast？
- 是否避免杜撰不可见的对白内容？
- 声音是否与画面节奏、剪辑点和 Action Phase 对齐？
