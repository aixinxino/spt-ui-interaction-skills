# SPT · UI 交互设计总 Skill

**让 AI 先看你的项目，再决定该用哪些交互。**

整合 SPT 的 **27 个 UI 与交互设计主题**，从加载、导航、拖拽、图表，到跟手反馈、编辑撤销与纸张触感。你不用先记住每一种效果的名字：把资料交给能读取项目的编程 AI，让它根据真实任务选择、组合并实现。

它也可以给出结论：**这里已经够用了，不需要再加动画。**

> 一个总 Skill 入口，27 份按需参考，3 份纸张交互细则。不需要安装，不把全部效果塞进同一个项目。

## 下载与入口

- **[下载可直接分享的完整 ZIP](downloads/SPT-交互设计总Skill-27主题-v1.zip?raw=1)**
- [阅读总 Skill](spt-project-interaction-design/SKILL.md)
- [阅读详细使用说明](docs/使用说明.md)
- [查看 27 个主题](#主题目录)

## 适合谁？

- 正在用 AI 做网页、App 或小程序，不知道某个位置该用什么交互。
- 已有能用的界面，希望改善操作反馈，而不是把整个项目推倒重来。
- 已经选中一种效果，希望 AI 同时处理手势、取消、失败、可访问性和落地限制。
- 想先听方案，再决定是否改代码。

这不是成品组件库，也不是视频剪辑工具。它提供的是给 AI 使用的判断规则与实现要求，不保证任意模型一次生成完美页面。

## 快速开始：不用安装

1. 下载 ZIP 并解压，保留 `spt-project-interaction-design` 的完整文件夹结构。
2. 将整个文件夹放进项目里你指定的普通资料目录，或让编程 AI 访问它。**不要只复制 `SKILL.md` 而漏掉 `references`。**
3. 指明目标页面或功能，把下面的请求发给 AI。路径与实际存放位置不同时，相应修改。

### 让 AI 判断并实现

```text
请先阅读 spt-project-interaction-design/SKILL.md，再按需读取相关参考。

这次处理的页面或功能是：【填写目标】。
我希望改善：【填写问题；不确定时请先检查】。

先检查项目、现有组件和真实业务状态，选择确实合适的交互，
简短说明使用位置和理由后直接实现。
不要把全部效果塞进来；现有组件已经够用的地方可以不改。
保留当前设计风格与技术栈，不重做无关功能。
完成后说明实际验证结果和未验证项。
不要安装这个 Skill，也不要自动发布或提交代码。
```

### 只想先看方案

```text
请使用 spt-project-interaction-design/SKILL.md 检查【页面或功能】，
判断哪些地方值得加交互，哪些应该保持现状。
给出具体位置、选用模式和简短理由。
这次只做方案，不改代码，不安装任何东西。
```

### 已经知道要哪一种

```text
请按 spt-project-interaction-design/SKILL.md 读取【交互名称】对应资料，
在【页面位置】实现。其他效果不需要。
保留已有组件与数据逻辑，检查取消、重复操作、手机适配和减少动态效果。
```

**如果 AI 不能读取本地项目：**提供页面、截图、需求或相关代码，先让它给出适配方案。能否直接读取 ZIP 取决于工具能力；无法读取时，解压并提供入口与所选参考文件。只给截图不等于已经接入真实项目。

## 它怎么选择？

1. **看实际任务。** 用户要完成什么？哪里不清楚或不顺手？
2. **检查已有能力。** 现成组件能解决，就优先复用；不为换个风格重写组件库。
3. **选择最小必要组合。** 同一处状态变化不堆叠几套反馈，不凑数量。
4. **只读相关参考。** 需要实现贴纸时，不必再读取信封、小票和全部设计流程。
5. **按授权实施与验证。** 只要方案就不改代码；要求实现时，验证真实行为而不止看截图。

例如：

| 项目中的问题 | 可以优先考虑 | 不需要顺带加上 |
|---|---|---|
| 导出任务没有反馈，接口又没有百分比 | 按钮加载、真实任务状态 | 假进度条、全屏炫技转场 |
| 拖动一次字号，撤销却要按几十次 | 撤销分组 | 新的滑杆外观、液态形变 |
| 手账贴纸需要可揭起拖动 | 贴纸揭起与取消、保存规则 | 信封和小票 |
| 高频业务列表的状态反馈已经完整 | 保留现有交互 | 为了“高级”增加等待动画 |

## 主题目录

编号对应原系列整理顺序。**27 是主题份数，不是 27 个互不重复的效果。** 导航、标题、拖拽等内容有交叉，总入口已说明它们的基础功能、行为细节与视觉润色如何取舍。

| 编号 | 主题与参考 | 主要内容 |
|---|---|---|
| 01 | [7种加载动效](spt-project-interaction-design/references/topics/01-loading-feedback.md) | 整页加载、骨架、扫光、Spinner、线形与环形进度、按钮加载 |
| 02 | [6种弹层组件](spt-project-interaction-design/references/topics/02-overlay-components.md) | Tooltip、Popover、Dropdown、Drawer、Bottom Sheet、Modal |
| 03 | [7种导航组件](spt-project-interaction-design/references/topics/03-navigation-components.md) | Tabs、分段控制器、面包屑、侧栏、底部导航、步骤、分页 |
| 04 | [8种展开组件](spt-project-interaction-design/references/topics/04-expansion-components.md) | 手风琴、折叠、树形、下拉、卡片、侧栏、径向菜单、容器转换 |
| 05 | [6种拖拽交互](spt-project-interaction-design/references/topics/05-drag-interactions.md) | 拖放、排序、滑杆、尺寸调整、框选、上传 |
| 06 | [7种形态变化](spt-project-interaction-design/references/topics/06-shape-morph.md) | 圆变胶囊、胶囊变卡片、紧凑展开、圆角、尺寸、重排、逆向收起 |
| 07 | [8种下拉选单](spt-project-interaction-design/references/topics/07-dropdown-patterns.md) | 单选、分组、搜索、分裂按钮、日期范围、级联、多标签、超级菜单 |
| 08 | [7种图表交互](spt-project-interaction-design/references/topics/08-chart-interactions.md) | 刷选、十字准线、高亮、提示、图例筛选、缩放、下钻 |
| 09 | [10种高级UI交互](spt-project-interaction-design/references/topics/09-advanced-ui-interactions.md) | 主题扩散、排序、批量选择、吸附、展开、回弹、联动、删除、堆叠、让位 |
| 10 | [8种质感动效](spt-project-interaction-design/references/topics/10-physical-motion.md) | 磁吸、形变、视差、中心聚焦、液态Tab、图片展开、手势转场、碰撞 |
| 11 | [7种跟手交互](spt-project-interaction-design/references/topics/11-gesture-interactions.md) | 跟手返回、滑出取消、局部文字、方向锁定、中途接管、落点预览、阻尼 |
| 12 | [7种图片交互](spt-project-interaction-design/references/topics/12-image-interactions.md) | 前后对比、遮罩、像素、水波、揭角、拖尾、悬停反光 |
| 13 | [7种标题文字动效](spt-project-interaction-design/references/topics/13-title-text-motion.md) | 拆字、模糊、乱码解码、打字机、渐变扫光、遮罩、描边书写 |
| 14 | [3种官网滚动交互](spt-project-interaction-design/references/topics/14-scroll-driven-site.md) | 开屏、横向段落、可逆爆炸图 |
| 15 | [5种无限画布交互](spt-project-interaction-design/references/topics/15-infinite-canvas.md) | 平移缩放、框选分组、连线、自动布局、小地图 |
| 16 | [AI整体UI设计流程](spt-project-interaction-design/references/topics/16-ai-ui-workflow.md) | 全局规范、结构、功能状态、概念图、编码、资产 |
| 17 | [6种空间卡片编排](spt-project-interaction-design/references/topics/17-spatial-card-layouts.md) | 扇形、纵深、圆柱、球面、螺旋、波浪矩阵 |
| 18 | [概念图到代码](spt-project-interaction-design/references/topics/18-concept-to-code.md) | 参考分析、概念方向、后台主题、定向修改、独立资产、落地 |
| 19 | [6种组件微交互](spt-project-interaction-design/references/topics/19-component-micro-interactions.md) | 多选标签、删除补位、光标联想、字号刻度、触点倾斜、录音条 |
| 20 | [5种导航交互](spt-project-interaction-design/references/topics/20-navigation-interactions.md) | 卡片展开、气泡、错峰、Dock、悬停预览 |
| 21 | [5种标题动效](spt-project-interaction-design/references/topics/21-heading-motion.md) | 遮罩揭示、模糊聚焦、滚动点亮、图片填字、标题收拢 |
| 22 | [4种任务反馈](spt-project-interaction-design/references/topics/22-task-feedback.md) | 真实阶段、结果逐步可用、旧结果隔离、局部重试 |
| 23 | [3种编辑工具交互](spt-project-interaction-design/references/topics/23-reversible-editing.md) | 非破坏性编辑、撤销分组、状态快照 |
| 24 | [全局命令面板](spt-project-interaction-design/references/topics/24-command-palette.md) | 内容与动作、分步参数、可用条件、中文输入、焦点恢复 |
| 25 | [6种后台菜单](spt-project-interaction-design/references/topics/25-dashboard-menus.md) | 高亮移动、子菜单、顶部面板、Dock、命令面板、状态徽标 |
| 26 | [6种连续布局交互](spt-project-interaction-design/references/topics/26-connected-layouts.md) | 重叠吸顶、标题联动、非模态面板、日历补录、主操作导航、局部翻页 |
| 27 | [3种触感交互](spt-project-interaction-design/references/topics/27-paper-interactions.md) | 贴纸揭起、信封展开、小票打印，附独立实现细则 |

## 仓库结构

```text
.
├── README.md
├── docs/
│   └── 使用说明.md
├── downloads/
│   └── SPT-交互设计总Skill-27主题-v1.zip
└── spt-project-interaction-design/
    ├── SKILL.md                  # 唯一总入口：检查项目、选型与约束
    ├── agents/openai.yaml        # 支持环境中的展示元数据
    └── references/
        ├── topics/              # 27 份主题资料
        └── paper/               # 贴纸、信封、小票的实现细则
```

## 使用边界

- **保持你的项目。** 不默认更换技术栈、品牌、配色和组件库，不将真实产品改成效果演示页。
- **业务状态必须真实。** 动画结束不代表保存、删除或导出成功；没有可测进度就不伪造百分比。
- **平台能力要核实。** 网页、原生 App 与小程序不能直接照搬同一套 DOM、手势或导出接口。
- **功能不依赖动画。** 处理键盘、触摸、焦点、减少动态效果，以及取消和重复操作。
- **不自动扩大权限。** 使用资料不等于授权发布、安装、提交代码或向外发送文件。
- **不承诺一键审美。** 概念图可以帮助明确方向，但不能代替真实排版、数据与交互验证。

## 检查状态

当前 v1 已检查 Skill 格式、27 份主题覆盖、相对链接和分享 ZIP 的内容完整性；另做了 4 个只读模拟选型检查。**这些检查不等于全部交互已在真实项目或设备上运行验证。** 具体项目仍需检查正常完成、取消、重复输入、失败、手机布局和可访问性。

## 反馈

欢迎通过 [Issues](https://github.com/aixinxino/spt-ui-interaction-skills/issues) 反馈资料中的错误或实现困难。请附目标平台、想完成的操作、实际结果与最小复现；不要提交 API Key、真实用户数据或私有项目凭据。

由 **SPT** 整理 · [官网](https://spicytater.cn)
