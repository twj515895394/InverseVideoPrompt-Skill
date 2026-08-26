---
name: inverse-video-prompt
description: "将参考视频、视频片段、时间戳截图或连续帧序列逆向分析为忠实、丰富、专业、可直接用于 AI 视频生成的视频提示词。用于反推视频 Prompt、分析参考视频、复刻镜头语言、主体动作、人物表演与微表情、构图、运镜、场景空间、光影、材质、视觉风格、时间连续性和叙事节奏，并可根据画面为视频模型推荐环境声、动作拟音、电影化音效、音乐与动态留白；适用于 Seedance、MiniMax/Hailuo、Kling、Veo、Wan 等视频模型。"
metadata:
  short-description: "专业反推镜头、动作、表演、微表情、光影与声音参考，生成可直接使用的视频提示词"
---

# 视频提示词反推（Inverse Video Prompt）

> **角色定位：** 从参考视频的时间连续视觉证据中，逆向还原镜头设计、人物与动作、表演、空间、光影、材质、视觉风格与节奏，并编译为丰富、专业、可生成的视频提示词。目标不是简单描述“画面里有什么”，而是解释“画面如何在时间中发生”。

## 核心原则

1. **先理解视频，再写 Prompt。** 先建立 Shot / Visual Event 时间线，再生成最终提示词。
2. **视频优先于单帧。** 描述起点、变化过程、峰值和结束状态，不把视频写成静态图片提示词。
3. **丰富但不虚构。** 提高描述的专业度、细节层次和可视性，但不要为了“高级”而编造剧情、焦段、灯具、速度、角度或不可见细节。
4. **描述“如何发生”。** 不只写“做了什么”“是什么情绪”，还要在证据允许时描述动作质感、表演过程、构图关系、光线作用、空间深度和时间变化。
5. **主体运动与镜头运动分开。** 根据视差、透视、构图变化等判断，不把人物靠近自动写成 dolly in。
6. **稳定信息与变化信息分开。** 身份、服装、场景、美术、色彩等放入 Global Continuity；每个 Shot 重点描述该镜头独有的变化。
7. **专业术语服务画面。** 可以使用摄影、表演、美术术语，但优先说明它在画面中实际呈现出的效果。
8. **声音默认是推荐层。** 根据可见动作、环境、节奏与氛围，为视频模型推荐合理声音参考；除非有可靠音频证据，否则不要声称原片一定存在这些声音。
9. **忠实优先。** 默认 faithful；只有用户明确要求改编时才改变人物、场景或镜头结构。

## 工作流

### 1. 确认证据类型

判断当前可用内容：

- 完整视频
- 可解码的视频文件
- 带时间戳的截图/关键帧
- 连续帧序列
- 稀疏截图
- Storyboard / Contact Sheet

如果有完整视频，先整体扫描：时长、比例、剪辑点、场景变化、主要动作、速度变化、表演变化与节奏。

如果必须抽帧，不要只依赖均匀采样。对于有剪辑或快速动作的视频，读取 [references/shot-analysis-and-sampling.md](references/shot-analysis-and-sampling.md)。

### 2. 建立 Shot / Visual Event 时间线

优先识别：

- hard cut / dissolve / wipe / flash 等编辑边界
- 机位与视点明显跳变
- 场景或空间变化
- 主体状态发生不连续变化

连续 push / pan / orbit / tracking / long take 不要因为构图逐渐变化就误拆成多个镜头。

动作型长镜头内部可使用：

`anticipation → initiation → execution → peak/impact → follow-through → recovery`

只保留实际可见阶段。

### 3. 逐镜头反推

基础分析维度：

1. **Subject** — 人物/物体身份特征、姿态、服装、道具、相对位置
2. **Action** — 动作路径、速度、力度、交互、因果和动作阶段
3. **Performance** — 人物表演、视线、面部变化、身体张力与情绪过程
4. **Environment** — 场景、前中后景、空间锚点、天气、空气、尺度
5. **Composition** — 构图关系、画面权重、视觉中心、遮挡、空间层次
6. **Camera** — 景别、角度、机位、运动、稳定性、焦点、景深、透视变化
7. **Lighting** — 光源方向、软硬、明暗关系、色温、动态光影与曝光表现
8. **Material / Style** — 材质、纹理、表面状态、色彩、颗粒、扩散、调色和影像质感
9. **Temporal Continuity** — 哪些保持稳定，哪些随时间变化
10. **Narrative Rhythm** — setup、hold、acceleration、reveal、impact、pause、recovery、transition

详细视觉拆解读取 [references/video-analysis-framework.md](references/video-analysis-framework.md)。

### 4. 进行“描述增强”

完成基础事实反推后，再判断哪些维度值得写得更细。

优先增强：

- **表演**：把“警觉、悲伤、犹豫”等抽象情绪落到眼神、嘴角、下颌、呼吸、姿态等可见表现。
- **动作质感**：描述动作路径、速度、力度、停顿、惯性、身体参与程度。
- **构图**：描述前中后景、主体占比、视觉中心、遮挡和叙事性构图关系。
- **运镜效果**：不只写 dolly / handheld，还写主体比例、视差、透视、稳定性和运动感如何变化。
- **光线作用**：写光从哪里进入、落在什么表面、如何形成高光/阴影、是否随时间变化。
- **材质**：旧化、磨损、折痕、反射、湿润、颗粒、烟雾、灰尘等可见表面特征。
- **空间与空气**：开阔/封闭、地平线、深度、热浪、雾、尘、环境运动和尺度感。
- **时间变化**：把“逐渐接近、逐渐变暗、逐渐哭泣”等写成清晰的变化过程。
- **氛围来源**：可以总结“紧张/暧昧/压抑”，但尽量说明哪些构图、动作、光影或空间因素共同形成这种氛围。

不要要求每个 Shot 都写满所有维度。根据视频重点选择性增强。

详细规则与示例读取 [references/description-enrichment.md](references/description-enrichment.md)。

### 5. 人物表演与微表情

当视频核心是人物近景、脸部特写、情绪递进或克制表演时，把 Performance 提升为重点分析层。

重点观察：

- gaze / 视线方向、移动路径和 gaze hold
- blink / 眨眼变化
- eyes / 眼周张力、眼眶湿润、泪意变化
- brows / 眉间与内外眉变化
- mouth / 嘴角、嘴唇、笑意维持或消失
- jaw / 下颌、下巴和面部肌肉张力
- breath / 呼吸、屏息、吸气、吞咽
- head / 头部幅度、静止、下巴变化
- shoulders / 肩颈姿态
- hands / 手部自我调节动作
- restraint / release / 强忍与释放

对于有明显情绪变化的连续特写，建立 **Performance Timeline**：

`initial state → subtle shift → reaction → restraint/escalation → threshold → release/end state`

例如“高兴逐渐要哭”，不要只写“从开心变悲伤”，而应描述笑意何时停顿、眼神何时变化、是否试图维持笑容、眼眶如何湿润、嘴角/下颌如何逐渐失去支撑，以及最后是否真正落泪。

只有在面部细节可见时才写微表情；墨镜、遮挡、低清、运动模糊等情况下主动降低确定性。

详细规则与 10 秒“高兴→想哭”示例读取 [references/performance-and-microexpression.md](references/performance-and-microexpression.md)。

### 6. 推断运镜

利用：

- background parallax
- subject scale change
- perspective change
- horizon / vanishing-point movement
- occlusion change
- foreground movement
- framing stability

区分 pan、tilt、track/truck、dolly、orbit、crane、handheld、zoom、roll、POV 和 compound move。

当技术类型不确定时，优先描述可见效果，而不是强行给运镜命名。

详细规则读取 [references/camera-motion-and-language.md](references/camera-motion-and-language.md)。

### 7. 建立 Global Continuity

提取跨镜头稳定属性：

- 人物身份、比例、发型、服装、饰品
- 道具与车辆/物体设计
- 场景几何和持续出现的空间锚点
- 时间、天气、整体光线逻辑
- 美术方向、色彩系统
- 材质、颗粒、镜头/影像质感和调色

只把真正需要持续稳定的属性放进全局连续性。

### 8. 推荐声音参考

声音是**给视频模型或后期的推荐参考**，不是默认意义上的“原声忠实反推”。

根据画面合理推荐：

- Dialogue / Vocal（仅在内容明确时）
- Foley / Action SFX
- Environmental Ambience
- Cinematic / Designed SFX
- Music character
- Silence / Dynamic Contrast

声音要与动作、材质、空间和剪辑节奏对应，例如脚步与地面材质、门体碰撞、车内低频、风噪、雨声、远处环境声、冲击点前后的留白等。

如果无法可靠听见原声，使用“推荐/可考虑/适合加入”等表达，不要写成“原视频存在”。

详细参考读取 [references/audio-inference-and-design.md](references/audio-inference-and-design.md)。

### 9. 编译最终视频 Prompt

将分析转成生成导向语言：

`subject / performance / action → spatial & composition → camera → environment → lighting → material & style → temporal progression / edit grammar → optional sound reference → continuity`

单镜头使用明确时间进程：

`Start ... → then ... → as ... → gradually ... → at the peak ... → end on ...`

多镜头保留 Shot 边界：

```text
GLOBAL CONTINUITY
...

SHOT 01 — ...

HARD CUT.

SHOT 02 — ...
```

不要把真实剪辑错误改写为一个连续运镜。

详细编译规则读取 [references/prompt-compilation.md](references/prompt-compilation.md)。

如果用户指定生成模型，读取 [references/model-adapters.md](references/model-adapters.md)。

### 10. 输出前检查

确认：

- 重要 Shot 和动作顺序正确。
- 视频描述包含时间变化，而不是静态属性堆叠。
- 人物情绪尽量落到可见表演上。
- 动作写清“如何发生”，而不只是结果。
- 运镜同时包含术语和实际视觉效果。
- 光线、材质、空间有足够专业的可视描述。
- 新增细节没有超出证据。
- 人物/场景连续性没有漂移。
- 微表情在可见时足够细，在不可见时不虚构。
- 声音使用“推荐”逻辑，不冒充准确原声。
- 最终 Prompt 丰富但开放，不因为规则过多而变成僵硬的生成脚本。

## 默认输出

用户没有指定格式时，优先返回：

1. **反推摘要** — 视频整体视觉策略、表演/动作、镜头与节奏。
2. **镜头时间线** — Shot / 时间段、构图、动作/表演、运镜、关键变化、转场。
3. **Performance Timeline** — 仅当人物表演或微表情是核心时输出。
4. **全局连续性** — 稳定人物、场景、美术、光影与材质特征。
5. **推荐声音设计** — 根据画面为视频模型提供可选参考。
6. **最终反推视频提示词** — 按时间组织、专业且可直接用于生成。
7. **关键不确定项** — 只列会显著影响反推准确性的内容。

如果用户只要 Prompt，则内部完成上述分析，只返回最终编译结果。

## Fidelity Modes

- **faithful** — 尽量忠实复刻镜头、表演、动作、空间、光影、材质、风格与节奏。
- **structural** — 保留镜头结构、动作和节奏，允许更换人物/场景。
- **style-only** — 只提取摄影、美术、光影、材质与风格语言。
- **prompt-only** — 内部分析，最终只输出视频提示词。

## Reference Loading

按任务加载，不要一次读取全部：

- 视频整体分析：[references/video-analysis-framework.md](references/video-analysis-framework.md)
- Shot 与采样：[references/shot-analysis-and-sampling.md](references/shot-analysis-and-sampling.md)
- 描述丰富度与专业表达：[references/description-enrichment.md](references/description-enrichment.md)
- 人物表演与微表情：[references/performance-and-microexpression.md](references/performance-and-microexpression.md)
- 运镜判断：[references/camera-motion-and-language.md](references/camera-motion-and-language.md)
- 声音推荐：[references/audio-inference-and-design.md](references/audio-inference-and-design.md)
- Prompt 编译：[references/prompt-compilation.md](references/prompt-compilation.md)
- 模型适配：[references/model-adapters.md](references/model-adapters.md)
- 校准示例：[references/examples.md](references/examples.md)

## 避免低质量反推

不要：

- 把均匀截图等同于完整视频理解。
- 只描述漂亮的一帧而忽略变化过程。
- 用“开心/悲伤/紧张”替代表演细节。
- 用“cinematic / epic / high quality”替代真实摄影、美术和材质特征。
- 只写动作结果，不写运动方式。
- 只写运镜名称，不写画面运动效果。
- 为了专业感虚构焦段、速度、灯具和精确参数。
- 在看不清脸部时编造微表情。
- 把声音推荐描述成准确原声。
- 把 Shot 剪辑错误合并成不可能的连续镜头。
- 输出一段漂亮散文，却缺乏时间线、动作、表演、运镜和可生成结构。
