---
name: mg-animation-starter
description: 用代码做 MG 动画的起步方法包（HTML/CSS/JS + GSAP + 无头 Chrome + FFmpeg）。用于在干净电脑上安装环境、唤醒项目、按闸门做一条类似但不相同的 MG 动画。触发词：MG动画、代码制视频、HyperFrames、做视频、动画起步、motion graphics、explainer video。
version: 1.0.0
---

# 【本 Skill 来自 NIO嘉亮加仑】MG 动画起步 Skill

> 一句话：这不是 AI 文生视频，也不是剪映 / PR。
> 它是「网页即视频」——HTML/CSS/JS + GSAP 时间轴，
> 无头 Chrome 逐帧截图，FFmpeg 编码成 H.264 MP4。

---

## 一、这个 Skill 解决什么

让一个只有 Agent 和模型的干净电脑，能够：

1. 从零装好 MG 动画工具链（Node / FFmpeg / HyperFrames / 无头 Chrome / 本地字体）。
2. 用一条 10 秒测试片验证整条链路。
3. 在每次新会话自动对齐需求、自检环境、按闸门推进。
4. 做出一条结构完整、节奏可读、画面干净的 MG 动画。

它适合：科普、数据、对比、流程、产品原理、文字动效、参数化图解。
它不适合：真人出镜、复杂角色动画、电影级实拍。

---

## 二、文件路由（先读对的那一份）

| 用户现在的意图 | 先读哪个文件 |
|---|---|
| 第一次用 / 换了一台干净电脑 / 环境没装好 | `2_项目准备提示词.txt` |
| 环境装好了，准备开始一条新片 | `3_项目唤醒词.txt` |
| 已经定好主题 / 风格 / 颜色，要正式做片 | `4_任务卡.txt` |
| 报错、渲染失败、画面不对、想避坑 | `5_常见坑速查.txt` |
| 想知道这个包是什么、怎么分享 | `1_README.txt` |

所有文件都在本 `SKILL.md` 所在目录。
如果用户把文件复制到了工作目录，优先读工作目录里的同名文件；
找不到再读本 Skill 目录里的原件。

---

## 三、三种运行时怎么用

这个 Skill 的正文和三个 txt 都是纯文本 + 通用命令，不依赖某个客户端的专有工具。
Claude Code、WorkBuddy、DeepSeek Harness 都可以直接读。

### 3.1 Claude Code

安装（用户级）：
```bash
mkdir -p ~/.claude/skills
cp -r "MG动画起步Skill-NIO嘉亮加仑" ~/.claude/skills/mg-animation-starter
```

Windows PowerShell：
```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse "D:\path\MG动画起步Skill-NIO嘉亮加仑" "$env:USERPROFILE\.claude\skills\mg-animation-starter"
```

也可以放项目级：`<项目>/.claude/skills/mg-animation-starter/`。
装完重启会话，输入 `/mg-animation-starter` 或直接说「用 MG 动画起步 Skill 做一条片」。

### 3.2 WorkBuddy

WorkBuddy 读取 `~/.workbuddy/skills/<name>/SKILL.md`。

Windows PowerShell：
```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.workbuddy\skills" | Out-Null
Copy-Item -Recurse "D:\path\MG动画起步Skill-NIO嘉亮加仑" "$env:USERPROFILE\.workbuddy\skills\mg-animation-starter"
```

macOS / Linux：
```bash
mkdir -p ~/.workbuddy/skills
cp -r "MG动画起步Skill-NIO嘉亮加仑" ~/.workbuddy/skills/mg-animation-starter
```

如果 WorkBuddy 有「导入 Skill / 本地技能」入口，也可以直接选这个文件夹。
装完重开 WorkBuddy，让它读一次 `SKILL.md`。

### 3.3 DeepSeek Harness（DSH）

DSH 支持 `.dsh/skills` 和 `.agents/skills` 两种技能根目录。
不同版本扫描的位置可能不一样；不确定时两处各放一份最稳。

用户级：
```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.dsh\skills" | Out-Null
Copy-Item -Recurse "D:\path\MG动画起步Skill-NIO嘉亮加仑" "$env:USERPROFILE\.dsh\skills\mg-animation-starter"
```

项目级：
```powershell
New-Item -ItemType Directory -Force "<项目>\.agents\skills" | Out-Null
Copy-Item -Recurse "D:\path\MG动画起步Skill-NIO嘉亮加仑" "<项目>\.agents\skills\mg-animation-starter"
```

注意 DSH 的两个已知限制：
1. **写权限**：DSH 默认只能写会话工作区。做片前把工作区设到 `<WORKDIR>`，
   或让用户授权写目标目录；否则它只能读、不能建项目。
2. **中文编码**：PowerShell 5.1 输出中文前先设
   `[Console]::OutputEncoding = [System.Text.Encoding]::UTF8`；
   写文件用 UTF-8 无 BOM。

### 3.4 没有 skill 工具的运行时

如果当前 Agent 没有「加载 Skill」的能力，也不影响使用：
让用户把 `SKILL.md` 和对应 txt 的内容直接贴进对话，
Agent 按同样的步骤执行即可。

---

## 四、开工顺序（三条命令）

### 第 1 步 · 装环境（只做一次）

读 `2_项目准备提示词.txt`，按它的步骤执行。
它会在 `<WORKDIR>` 下装好：

- Node.js 22+
- HyperFrames CLI
- FFmpeg / FFprobe 全量版
- 无头 Chrome
- 本地 GSAP + 中文字体
- 一个 10 秒测试项目

验收标准：
```bash
npx hyperframes doctor --json
npx hyperframes check --json
npx hyperframes render --quality draft --output out/smoke.mp4
ffprobe -v error -show_entries format=duration:stream=codec_name,width,height \
  -of default=noprint_wrappers=1 out/smoke.mp4
```

只有核心四项（Node / FFmpeg / FFprobe / Chrome）全 ok，
并且 ffprobe 能看到 h264 / 正确分辨率 / 约 10 秒，才算装好。

### 第 2 步 · 唤醒（每次新会话）

读 `3_项目唤醒词.txt`，让它：
1. 读环境说明和任务卡；
2. 跑 `npx hyperframes doctor --json`；
3. 用 3 行复述主题、画幅、路线、第一道闸门；
4. 停下等用户发任务卡。

### 第 3 步 · 做片

读 `4_任务卡.txt`，让用户填好 `<尖括号>`，按四道闸门推进：

1. 需求对齐
2. 配色确认
3. 逐屏静帧
4. 10 秒试渲

每道闸门都要停，不许一口气做完。

---

## 五、硬边界（这个 Skill 不做什么）

- **不提供风格**：没有原作者的配色、字体、版式、幕结构、动效习惯。
  风格由用户自己定；任务卡只给流程和工程约束。
- **不提供素材**：没有图片、音频、矢量图、参考片、字体文件。
  需要用户自己找可商用素材，或自己画。
- **不提供私有提示词**：不包含原作者的完整任务卡、学习笔记、复盘全文。
- **不保证好看**：它保证「能起步、能出片、能验证」；
  风格强不强、动效细不细，取决于用户的审美和迭代。
- **不替用户决定**：平台、画幅、时长、配色、旁白、BGM，
  都要用户先给方向；Agent 只给默认值和建议。

---

## 六、常见命令速查

```bash
# 环境
npx hyperframes doctor --json
npx hyperframes browser ensure
npx hyperframes skills update

# 新项目
npx hyperframes init my-video --resolution landscape --non-interactive

# 检查与看帧
npx hyperframes check --json
npx hyperframes snapshot --at 1,3,5,8

# 渲染
npx hyperframes render --quality draft --output out/draft.mp4
npx hyperframes render --quality looks --output out/final.mp4

# 验收
ffprobe -v error -show_entries format=duration:stream=codec_name,width,height \
  -of default=noprint_wrappers=1 out/final.mp4
```

参数以当前版本 `npx hyperframes <command> --help` 为准。

---

## 七、第一次响应协议

当用户第一次调用这个 Skill 时，先做这三件事，不要直接写页面：

1. 判断用户处在哪一步：
   - 环境没装 → 读 `2_项目准备提示词.txt`
   - 环境装好、还没定需求 → 读 `3_项目唤醒词.txt`
   - 需求已定 → 读 `4_任务卡.txt`
2. 用 3 行复述你理解的任务和环境状态。
3. 如果环境已存在，跑一次 `npx hyperframes doctor --json`；
   如果核心项 fail，先修环境，不要开始做片。

---

## 八、署名

本 Skill 由 **NIO嘉亮加仑** 整理分享。
转发、二次分享、改写成别的运行时版本，请保留这句话：

> 本 Skill 来自 NIO嘉亮加仑。

HyperFrames 是第三方工具，安装与使用请遵循其官网许可与额度说明。
本 Skill 不附带任何第三方素材，也不授权任何品牌 Logo 的使用。

---

**本 Skill 来自 NIO嘉亮加仑。**
它是一套起步方法，不是一套成片模板。
