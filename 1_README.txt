================================================================
  【本 Skill 来自 NIO嘉亮加仑】
  MG 动画起步包（可分享版）· README
  版本：2026-11-17
  仓库：https://github.com/btcgallon/mg-animation-starter
================================================================

================================================================
  ★ 先看这里：怎么用（30 秒版）
================================================================
这套东西有两种用法，别搞反：

【用法 A · 第一次装环境】—— 先别装 Skill
  把 2_项目准备提示词.txt 整段发给 AI，让它实际安装、实际验证。
  装完必须看到：一条 10 秒测试片 + 「组件 / 版本 / 路径 / 验证结果」表。
  只丢一个 SKILL.md 过去，AI 可能只读外壳、跳过安装和验证。

【用法 B · 日常做片】—— 装好之后再用 Skill
  1. 新会话先发 3_项目唤醒词.txt（或调用 Skill），让它自检 + 复述 + 停下。
  2. 想好主题 / 受众 / 画幅 / 风格，填好 4_任务卡.txt，再发。
  3. 报错、渲染失败、画面不对，先查 5_常见坑速查.txt。

【Skill 什么时候装、怎么用】
  装好环境、成功出过一条 10 秒测试片之后，再把整个文件夹复制到：
    Claude Code   ~/.claude/skills/mg-animation-starter
    WorkBuddy     ~/.workbuddy/skills/mg-animation-starter
    DSH           ~/.dsh/skills/mg-animation-starter
                  （或项目内 .agents/skills/mg-animation-starter）
  重启客户端，然后直接说：
    「用 mg-animation-starter 帮我装环境」
    「用 mg-animation-starter 做一条 XX 主题的片」
    「mg-animation-starter，渲染报错了，帮我查」
  客户端不支持 Skill：把 SKILL.md 和对应 txt 直接贴进对话，效果一样。
  第一次调用 Skill 装环境时，补一句「执行 2 的全文，不要只给方案」。

  一句话：2 / 3 / 4 是给新人的，SKILL.md 是给熟手的快捷方式。

【从 GitHub 获取与更新】
  仓库：https://github.com/btcgallon/mg-animation-starter
  第一次：git clone 这个地址，拿到的就是最新版。
  以后更新：cd 进目录，git pull。
  已装成 Skill 的，也在 skill 目录里 git pull。
  详细步骤见第十节。
================================================================

一、这是什么
----------------------------------------------------------------
这是一套「用代码做 MG 动画」的起步方法包。
它不是 AI 文生视频，也不是剪映 / PR。它的原理是：

    HTML + CSS + JavaScript + GSAP 时间轴
              ↓  无头 Chrome 逐帧截图
            PNG 帧序列
              ↓  FFmpeg 编码
            H.264 MP4

每个字的位置、每根线的粗细、每一帧的时间，都由代码决定。
好处：可复现、可精调、不需要显卡、不需要买素材。
适合：科普、数据、对比、流程、产品原理、文字动效、参数化图解。
不适合：真人出镜、复杂角色动画、电影级实拍。

二、包里有什么（按顺序用）
----------------------------------------------------------------
SKILL.md                  ← Skill 外壳：装好环境之后用，三端入口（见顶部「先看这里」）
1_README.txt              ← 你正在读的这份：说明与使用顺序
2_项目准备提示词.txt      ← 发给 AI Agent，让它从零装好环境
3_项目唤醒词.txt          ← 装好后，每次开工先发这段
4_任务卡.txt              ← 定好主题 / 风格 / 颜色后，发给 Agent 做片
5_常见坑速查.txt          ← 可选：遇到问题先翻这里

三、你需要准备什么
----------------------------------------------------------------
- 一台 Windows 10/11 或 macOS 的电脑（Linux 也可以）
- 建议 8GB 以上内存、20GB 以上空闲磁盘
- 一个能执行命令、读写文件的 AI Agent
  （Claude Code / WorkBuddy / DeepSeek Harness / Codex CLI / Cursor / Gemini CLI 等）
- 能访问 npm / GitHub / 字体源 的网络；必要时自备代理
- 不需要：独立显卡、剪辑软件、付费素材、云渲染账号

四、三步开始
----------------------------------------------------------------
第 1 步：装环境
  把 2_项目准备提示词.txt 整段复制给你的 Agent。
  它会探测系统，安装 Node.js / FFmpeg / HyperFrames / 无头 Chrome，
  建一个测试项目，并渲染一条 10 秒 MP4 验证整条链路。
  装完让它给你一张「组件 / 版本 / 路径 / 验证结果」表。

第 2 步：唤醒
  每次新会话，先把 3_项目唤醒词.txt 发给 Agent。
  它会先做环境自检、读任务卡，然后用 3 行复述理解，停下等你。

第 3 步：做片
  等你想好主题、受众、画幅、风格方向后，填好 4_任务卡.txt 里的
  <尖括号> 内容，发给 Agent。它会按闸门一步一步做，每步停下等你确认。

如果你已经把整个文件夹装成了 Skill（见第九节），
可以直接调用 `mg-animation-starter`，不用每次贴长文。

注意：SKILL.md 是「装好之后的快捷入口」，不是第一次的安装包。
第一次在干净电脑上，仍按 2 → 3 → 4 的顺序发；
只丢一个 Skill 过去，Agent 可能只读外壳、跳过实际安装和验证。

五、这份包不包含什么
----------------------------------------------------------------
- 不包含原作者的成片风格、配色、字体、版式、音色、文案
- 不包含原作者的私有提示词、项目文件、素材库
- 不包含任何图片、音频、矢量图、参考片
- 不包含「保证好看」：风格由你定，质量取决于你和 Agent 的沟通

六、做完能到什么程度
----------------------------------------------------------------
能独立起步做一条结构完整、节奏可读、画面干净的 MG 动画：
有资料、有文案、有分镜、有配色、有静帧确认、有试渲、有成片。
至于风格强不强、动效细不细，取决于你自己的审美和迭代。

七、版权与署名
----------------------------------------------------------------
- 本方法包由 NIO嘉亮加仑 整理分享。转发或二次分享，请保留
  「本 Skill 来自 NIO嘉亮加仑」这句话。
- HyperFrames 是第三方工具，安装与使用请遵循其官网许可与额度说明。
- 字体、音乐、图片请使用可商用 / 公有领域资源，并自行保留授权记录。
- 本包不附带任何第三方素材，也不授权任何品牌 Logo 的使用。

八、常见问题
----------------------------------------------------------------
Q: 我只有网页版聊天机器人，能用吗？
A: 不能。它读不到本机文件、也不能执行命令。
   必须用能操作本地环境的 Agent。

Q: 一定要有显卡吗？
A: 不需要。渲染靠 CPU + 无头 Chrome + FFmpeg。内存越大越稳。

Q: 一定要配旁白吗？
A: 不一定。无旁白 + 画面文字 + BGM 是最容易起步的路线。

Q: 中文配音怎么做？
A: 三条路：HyperFrames 自带 Kokoro（先试 3 句，中文可能不理想）、
   edge-tts（免费在线）、你自己的本地 TTS。开工前先定样音。

Q: 渲染很慢 / 内存爆？
A: 降低并发 worker，或用 draft 画质；长片分段渲染再拼接。

Q: 我能改成自己的风格吗？
A: 必须能。这套包只给流程，不给风格。你的配色、字体、版式、动效
   都由你在任务卡里定。

Q: 装完以后还需要联网吗？
A: 渲染本身不需要联网。但首次安装、下载字体 / 模型、查资料需要。
   字体和 JS 库要本地化，运行时不要依赖 CDN。

九、安装与使用 Skill（Claude Code / WorkBuddy / DeepSeek Harness）
----------------------------------------------------------------
整个文件夹带 SKILL.md，可以直接复制到对应运行时的技能目录。
目标文件夹名建议用 `mg-animation-starter`（和 SKILL.md 里的 name 一致）。

Claude Code：
  mkdir -p ~/.claude/skills
  cp -r "MG动画起步Skill-NIO嘉亮加仑" ~/.claude/skills/mg-animation-starter
  # 或项目级：<项目>/.claude/skills/mg-animation-starter/

WorkBuddy：
  mkdir -p ~/.workbuddy/skills
  cp -r "MG动画起步Skill-NIO嘉亮加仑" ~/.workbuddy/skills/mg-animation-starter

DeepSeek Harness（DSH）：
  mkdir -p ~/.dsh/skills
  cp -r "MG动画起步Skill-NIO嘉亮加仑" ~/.dsh/skills/mg-animation-starter
  # 或项目级：<项目>/.agents/skills/mg-animation-starter/
  # 不确定 DSH 扫哪个目录时，两处各放一份最稳。

Windows PowerShell 示例（三端通用，改目标路径即可）：
  Copy-Item -Recurse "D:\path\MG动画起步Skill-NIO嘉亮加仑" "$env:USERPROFILE\.claude\skills\mg-animation-starter"
  Copy-Item -Recurse "D:\path\MG动画起步Skill-NIO嘉亮加仑" "$env:USERPROFILE\.workbuddy\skills\mg-animation-starter"
  Copy-Item -Recurse "D:\path\MG动画起步Skill-NIO嘉亮加仑" "$env:USERPROFILE\.dsh\skills\mg-animation-starter"

装完重启对应客户端，让它重新扫描技能目录。
如果客户端没有「技能」功能，也不影响：把 SKILL.md 和对应 txt 直接贴进对话即可。

DSH / WorkBuddy 的工作区提醒：
- DSH 默认只能写会话工作区；做片前把工作区设到 <WORKDIR>，或让用户授权。
- WorkBuddy 默认工作区在 `_sessions`；做片前切到项目目录。

装好之后怎么调用：
- Claude Code：输入 `/mg-animation-starter`，或直接说
  「用 mg-animation-starter 做一条片」。
- WorkBuddy：在技能列表里选 mg-animation-starter，或直接说它的名字。
- DSH：直接说「用 mg-animation-starter ……」；它会在 `.dsh/skills`
  或项目内 `.agents/skills` 下查找。
- 调用后的第一句，先说清你在哪一步：
  「先装环境」/「环境好了，要开新片」/「渲染报错」。
  Skill 会按文件路由去读 2 / 3 / 4 / 5，不会自己乱猜。

怎么确认 Skill 真的加载了：
- 让它复述 SKILL.md 里的「四道闸门」或「文件路由表」。
- 答不上来，就是没加载成功；退回直接贴 txt，不影响做片。

三条使用边界：
1. 第一次装环境仍以 2 为主，Skill 只是帮你找到 2。
2. Skill 不提供风格、素材、私有提示词；风格仍由你自己定。
3. 每次新会话仍建议先发 3 或先调用 Skill；
   不要让它凭上一轮记忆直接写代码。

十、从 GitHub 获取与更新
----------------------------------------------------------------
仓库地址：
  https://github.com/btcgallon/mg-animation-starter

第一次获取（推荐 clone，不要只用 zip）：
  git clone https://github.com/btcgallon/mg-animation-starter.git

以后更新：
  cd mg-animation-starter
  git pull

如果已经装成 Skill（以 Claude Code 为例）：
  cd ~/.claude/skills
  git clone https://github.com/btcgallon/mg-animation-starter.git
  # 以后更新：
  cd ~/.claude/skills/mg-animation-starter
  git pull

WorkBuddy / DSH 同理，只换目录：
  ~/.workbuddy/skills/
  ~/.dsh/skills/（或项目内 .agents/skills/）

如果你当初是复制文件夹，不是 clone：
  git pull 用不了。先备份你改过的文件，再删除旧目录，
  重新 clone 一次；或者 git init + 添加 remote 后 fetch。

没有 git、也不想用命令行：
  打开仓库页 → Code → Download ZIP，解压覆盖。
  注意：ZIP 不会合并你的本地修改，覆盖前先备份。

看当前版本：
  README 顶部有版本日期；仓库的 commit 记录是最准的更新日志。
  本地也可以跑：git log -1 --oneline

================================================================
  再次说明：本 Skill 来自 NIO嘉亮加仑。
  它是一套起步方法，不是一套成片模板。
================================================================
