# 暗影猎手｜11-20 至 11-21 镜头生成清单（MiniMax H3）

在 `工作流/api` 目录执行。正式出片加 `-Width 1344 -Height 768 -RefSize max`；测试可先用默认 864×480。
H3 每段最短约 5.2 秒（124 帧），最长 15 秒。短镜头都按 5 秒生成，前后多留了静止段，剪辑时裁掉。

| 序号 | 镜头 | 模式 | 时长 | 剪辑后保留 |
| --- | --- | --- | --- | --- |
| 01 | Bean 张翼扇三下、两声警叫 | kf | 5 s | 约 4 s |
| 02a | Ash 转正脸说 "Oh, crap!" | kf | 5 s | 约 2.5 s |
| 02b | 推进 Ash 的金棕色眼睛 | kf | 5 s | 约 3.5 s |
| — | 瞳孔转场（剪映：缩放 + 圆形蒙版） | 剪辑 | — | 约 1 s |
| 03a | Houndson 特写 "Puff! One more!" | flf2v（单首帧） | 5 s | 约 2.5 s |
| 03b | 全景出手扔飞盘 "Go, Puff!"，Puff 起跳 | kf | 5 s | 约 2.5 s（裁掉前段静止） |
| 03c | 俯拍：飞盘入画、Puff 从画外冲进来 | kf | 5 s | 约 3.5 s |
| 04 | Houndson 跑来说 "Good boy."，Puff 抬眼 | kf | 5 s | 约 4 s |
| 05a | 墙顶俯拍：Puff 抬头、飞盘掉落 | kf | 5 s | 约 3 s |
| 05b | 墙顶俯拍：Puff 狂吠、Houndson 抬头、阴影进入 | kf | 7 s | 约 6 s |
| 07 | Houndson 特写 "What… is that thing?" | flf2v（单首帧） | 5 s | 约 4.5 s |
| 06 | （可选）Houndson 视角仰拍墙顶莉莉 | flf2v（单首帧） | 5 s | 约 2–3 s |
| 08 | 背面全景：莉莉扑向 Puff | kf | 5 s | 约 3 s |
| 09a | 过肩俯拍：Houndson 翻滚护住 Puff，利爪挥来 | kf | 5 s | 约 3 s |
| 09b | 过肩俯拍：利爪划过三角肌 | kf | 5 s | 约 2 s |

```powershell
# 01 Bean 警叫
.\run_h3.ps1 -Mode kf -Images shot-bean-perch-start.webp,shot-bean-wings-end.webp,animal-bean-single.png -PromptFile prompts\01-bean-warning.txt -Seconds 5

# 02a Ash "Oh, crap!"
.\run_h3.ps1 -Mode kf -Images shot-ash-alarm-turned.webp,shot-ash-alarm-front.webp,character-ash-single.png -PromptFile prompts\02a-ash-oh-crap.txt -Seconds 5

# 02b 推进金棕色眼睛
.\run_h3.ps1 -Mode kf -Images shot-ash-alarm-front.webp,shot-ash-amber-eye-closeup.webp,character-ash-single.png -PromptFile prompts\02b-ash-eye-pushin.txt -Seconds 5

# 03a 特写 "Puff! One more!"
.\run_h3.ps1 -Mode flf2v -Images shot-houndson-smile-closeup.webp -PromptFile prompts\03a-houndson-one-more.txt -Seconds 5

# 03b 扔飞盘 "Go, Puff!"
.\run_h3.ps1 -Mode kf -Images shot-frisbee-hold-start.webp,shot-frisbee-throw-end.webp,character-houndson-single.png,animal-puff-single.png -PromptFile prompts\03b-frisbee-throw.txt -Seconds 5

# 03c 俯拍追飞盘（从瞳孔转场接入）
.\run_h3.ps1 -Mode kf -Images shot-chase-overhead-start.webp,shot-chase-overhead-end.webp,animal-puff-single.png -PromptFile prompts\03c-frisbee-chase-overhead.txt -Seconds 5

# 04 Houndson 跑来 "Good boy."（尾帧右上角的裤腿残留要先修掉，修好后覆盖 shot-houndson-run-end.webp）
.\run_h3.ps1 -Mode kf -Images shot-houndson-run-start.webp,shot-houndson-run-end.webp,character-houndson-single.png,animal-puff-single.png -PromptFile prompts\04-houndson-good-boy.txt -Seconds 5

# 05a 俯拍：Puff 抬头、飞盘掉落
.\run_h3.ps1 -Mode kf -Images shot-overhead-frisbee-start.webp,shot-overhead-puff-lookup-mid.webp,character-houndson-single.png,animal-puff-single.png -PromptFile prompts\05a-overhead-puff-looks-up.txt -Seconds 5

# 05b 俯拍：狂吠、抬头、阴影
.\run_h3.ps1 -Mode kf -Images shot-overhead-puff-lookup-mid.webp,shot-overhead-bark-end.webp,character-houndson-single.png,animal-puff-single.png -PromptFile prompts\05b-overhead-bark-lookup.txt -Seconds 7

# 07 Houndson 特写台词
.\run_h3.ps1 -Mode flf2v -Images shot-houndson-closeup-lookup.png -PromptFile prompts\07-houndson-what-is-that.txt -Seconds 5

# 06（可选）仰拍墙顶莉莉
.\run_h3.ps1 -Mode flf2v -Images shot-lily-wall-pov.webp -PromptFile prompts\06-lily-wall-pov.txt -Seconds 5

# 08 莉莉扑向 Puff
.\run_h3.ps1 -Mode kf -Images shot-courtyard-creature-dive-start.png,shot-courtyard-creature-dive-end.png,character-houndson-single.png,character-houndson-courtyard-closeup.png,animal-puff-single.png -PromptFile prompts\08-lily-dive-at-puff.txt -Seconds 5

# 09a 翻滚护住 Puff
.\run_h3.ps1 -Mode kf -Images shot-slash-1-roll.png,shot-slash-2-shield.png,character-houndson-single.png,animal-puff-single.png -PromptFile prompts\09a-roll-shield-puff.txt -Seconds 5

# 09b 利爪划过三角肌
.\run_h3.ps1 -Mode kf -Images shot-slash-2-shield.png,shot-slash-3-wound.png,character-houndson-single.png,animal-puff-single.png -PromptFile prompts\09b-claw-slash-deltoid.txt -Seconds 5
```

## 剪辑提示

- 05b 的阴影如果又变形：把尾帧换成没有阴影的版本，提示词删掉 SHADOW 段，阴影在剪映里用 PNG 叠加（正片叠底 + 位移关键帧）。
- 08 的飞扑在剪映里做曲线变速，加速 2–3 倍；残影如果像黑烟，改用方向模糊。
- 07 特写的橙色光和夜景不统一，剪辑时整体压暗、暗部加冷蓝、加暗角。
