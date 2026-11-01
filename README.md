# 叶文洁 · ETO 地球统帅挂件

> 住在 DSH Web 界面右下角的「统帅」：Q 版叶文洁 + 黑红气泡 + 三体名言随机出泡，顺手帮你盯着 DeepSeek 余额。

[![License: MIT](https://img.shields.io/badge/license-MIT-a81c24.svg)](LICENSE)
![DSH](https://img.shields.io/badge/DSH-Web%20bundle-7a1218)

![三种气泡](preview/shots/overview.png)

---

## 这是什么

一个标准的 **DSH（DeepSeek Harness）bundle 插件**：装好后每次打开 DSH Web，右下角都会站着一位 Q 版叶文洁。
点她会冒出黑底红边的气泡 —— 先是统帅简报（余额 / 今日已用 / 峰谷倒计时），再点是三体名言，再点是原挂件那套吐槽。

工程上派生自 [小鲸鱼余额挂件](https://github.com/MeteorNOX/DeepSeek-Balance-Whale-Widget)（MIT），
换了角色、配色和默认气泡内容，并做了**命名空间隔离**（`dshw*` → `yewj*`、`/dsh-whale/*` → `/dsh-yw/*`、包名独立），
所以可以和原小鲸鱼挂件同时安装，互不抢配置（但右下角位置会重叠，见「兼容与限制」）。

## 特性

| | |
| --- | --- |
| 🎭 **Q 版叶文洁** | 透明底立绘，深墨蓝 ETO 军装、金线门襟、左胸三体轨道徽记、右臂红底「三」臂章，右手托发光徽章 |
| 🖤 **黑红气泡** | 近黑底 `#121216` + 血红描边 `#B3222B`，外圈淡红辉光；尾巴两个小圆点 |
| 📜 **57 条三体名言** | 取自《三体1名言叶文洁》语录页，随机出泡且不连续重复，落款「——《三体》· 叶文洁」 |
| 💬 **原话语保留** | 原挂件那套吐槽保留 38 条（去鲸鱼化），仍可抽到 petpet 动图 |
| 💰 **余额与记账** | 余额 60 秒刷新 + 点击手动刷新、数字滚动动画、今日已用、峰谷定价与倒计时 |
| 🎛 **气泡编辑器** | 模块化内容（文本/随机语句/图片/余额/今日/峰谷/对话名…），拖拽排序、并列加权、逐行样式与字体 |
| 🔊 **音效与提醒** | 按压/松开音、每轮消耗提示、提问/授权提示、余额预警、今日预算 |
| 🖱 **拖拽与吸附** | 四边吸附、贴左水平镜像翻转、按压 Q 弹、静息呼吸浮动 |
| 📱 **移动端友好** | 触摸拖动、长按 1.5 秒唤出菜单、去掉了浏览器点击高亮 |
| 🔌 **完全本地** | 账本、配置、资源都在本机 `$DSH_HOME`，密钥只存凭据名 |

## 安装

> 需要较新的 DSH（Web 或官方桌面端）。安装后 **必须重启 DSH 宿主**（profile 的 patch 在启动时叠加），
> 浏览器再 `Ctrl+F5` 刷新。

### 方式 A：从本地目录安装（开发 / 自用推荐）

```bash
dsh plugin --profile web add link:"/path/to/dsh-ye-wenjie-widget"
```

### 方式 B：从 GitHub 安装

```bash
dsh plugin --profile web add github:<owner>/dsh-ye-wenjie-widget
```

### 方式 C：等你发布到 npm 之后

```bash
dsh plugin --profile web add dsh-ye-wenjie-widget
```

### 卸载 / 回滚

```bash
dsh plugin --profile web remove dsh-ye-wenjie-widget
```

> 桌面端（Electron）读的是 `desktop` profile，不能用 `--profile web`；在桌面端会话里让 DSH 用它内置的
> `plugin_manager` 安装即可（与上游挂件同一套说明）。

## 用法

| 操作 | 效果 |
| --- | --- |
| 单击角色 | 简报 → 名言 → 原话语 → 收起；下次点击重新从简报开始（「点按角色推进」默认开启） |
| 单击泡泡 | 跳到下一条；最后一条再点收起 |
| 拖动角色 | 自由摆放，松手后四边吸附；贴左边时整体水平镜像 |
| 长按 1.5 秒 / 右键 | 唤出菜单（角色、大小、音效与提示、气泡开关、避让滚动条、吸附与翻转、资源管理、记账） |
| 菜单 → 自定义泡泡 | 编辑每一条气泡的内容、顺序、并列权重与逐行样式 |

## 自定义

### 改名言池

名言池在 `art/make_bubbles.py` 顶部的 `QUOTES` 列表里（每条带权重 `w`），改完重跑：

```bash
python3 art/make_bubbles.py    # 重新生成出厂默认气泡（写入 assets/yewenjie-widget.js 的 BUBBLE_DEFAULT_ITEMS）
```

也可以不改代码：**菜单 → 自定义泡泡** 里直接编辑「随机语句」模块的句子。

### 换角色图

菜单 → 角色 → 导入（png/gif，建议透明底方形图）。
或者替换 `assets/yewenjie.png` 后重跑 `python3 art/make_assets.py`（会一并重出图标与气泡动图）。

### 调默认大小

`assets/yewenjie-widget.js` 里 `--yewj-base` 的 clamp 公式；装好后也可以在菜单里用「大小」滑块调。

## 数据与隐私

运行期数据全部在 `$DSH_HOME`（默认 `~/.dsh`），与上游小鲸鱼插件**完全分开**：

| 文件 / 目录 | 用途 |
| --- | --- |
| `.yewj-size.json` | 缩放、音量、峰谷样式、吸附等外观开关 |
| `.yewj-bubble.json` | 自定义气泡队列、模块库、气泡框 |
| `.yewj-usage.json` | 记账账本与提醒设置 |
| `.yewj-usage-archive.json` / `.yewj-turn.json` / `.yewj-api.json` / `.yewj-codex.json` | 归档、轮次、自定义模型、Codex 统计 |
| `yewenjie-roles/` · `yewenjie-audio/` · `yewenjie-bubble-imgs/` | 自定义角色、音频片段、气泡图库 |

- 密钥写入 DSH 官方凭据服务，配置文件里**只有凭据名**；
- 余额请求只发往 DeepSeek 官方接口，或你在「自定义 API」里填写的接口；
- 账本、截图、角色图都不出本机；插件本身不做任何统计上报。

## 开发

```bash
# 本地预览：真实前端 + 模拟宿主数据，不安装、不重启、不写 ~/.dsh
node preview/server.mjs 3099
# http://127.0.0.1:3099/
#   ?bubble=1/2/3  直接停在简报 / 名言 / 原话语
#   ?clean=1       去掉模拟聊天界面，只留挂件（截图用）
```

```bash
python3 art/make_assets.py     # 角色方形立绘 / 图标 / 气泡动图
python3 art/make_bubbles.py    # 出厂默认气泡 + art/default-bubbles.json
```

```text
dsh-ye-wenjie-widget/
├── package.json            # 插件元数据（dsh.bundle.patch → cordis.patch.yml）
├── cordis.patch.yml        # 挂载声明（id: dsh-ye-wenjie-widget）
├── icon.png                # 256×256 插件图标
├── lib/
│   ├── index.js            # 宿主侧：/dsh-yw/* 路由、余额记账、资源服务、脚本注入
│   └── accounting.mjs      # 记账内核
├── assets/
│   ├── yewenjie-widget.js  # 前端挂件本体（宿主按 mtime 热读取）
│   ├── yewenjie.png        # 角色方形立绘（右下对齐，命中检测沿用原几何）
│   ├── bubble-*.gif / rua.gif
│   └── *.mp3 / *.wav       # 音效
├── art/                    # 素材与默认气泡生成脚本 + default-bubbles.json
├── preview/                # 本地预览服务与截图
└── README.md
```

![菜单](preview/shots/yw-menu.png)

## 兼容与限制

- **与小鲸鱼挂件**：两者都固定在右下角，同时装会重叠；建议二选一。
  卸载鲸鱼：`dsh plugin --profile web remove dsh-whale-widget`（下次启动生效）。
- **音效**：沿用上游素材（小黄鸭 / 音效1 / Minecraft 经验球等），没有做角色语音。
- **名言**：为语录页的节选，过长句做了不改变原意的截取；不是原文全文。
- **立绘**：本仓库 `art/` 程序化生成的同人 Q 版形象，非官方素材。
- **预览服务**：`preview/` 只是开发工具，不属于插件运行路径。

## 致谢与许可

- 工程骨架、记账内核、气泡编辑器、音效与吸附逻辑来自
  [MeteorNOX/DeepSeek-Balance-Whale-Widget](https://github.com/MeteorNOX/DeepSeek-Balance-Whale-Widget)（MIT）。
- 名言文本来自公开语录页 [《三体1名言叶文洁》](http://www.lizhi135.com/articles/lizhi-876848.html)，仅作同人展示。
- 《三体》相关权利归刘慈欣及出版方；本项目与官方无关。
- 本项目以 **MIT** 发布，见 [LICENSE](LICENSE)；派生说明见 [PROVENANCE.md](PROVENANCE.md)。

---

## English

A DSH (DeepSeek Harness) Web widget: a chibi Ye Wenjie (ETO Earth commander) sitting at the bottom-right corner,
with black-and-red speech bubbles that cycle through a curated pool of *The Three-Body Problem* quotes,
plus DeepSeek balance / daily spend / peak-hour pricing.

It is a themed fork of [DeepSeek-Balance-Whale-Widget](https://github.com/MeteorNOX/DeepSeek-Balance-Whale-Widget) (MIT),
with an isolated namespace, new character art, a black-red theme and a quote pool.

```bash
dsh plugin --profile web add link:"/path/to/dsh-ye-wenjie-widget"
# restart the DSH host, then reload the page
```

Dev preview: `node preview/server.mjs 3099` → <http://127.0.0.1:3099/>.
License: MIT. *The Three-Body Problem* belongs to Liu Cixin and its publishers; this is a fan project.
