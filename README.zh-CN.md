# Design Context UI

[English](./README.md) | **中文**

![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![Type: Skill](https://img.shields.io/badge/Type-Skill-blue)
![Focus: UI Design](https://img.shields.io/badge/Focus-UI%20Design-orange)

一个面向 AI coding agent 的 UI 设计 skill。

它把真实项目上下文、设计参考路由和代码落地约束组织成一条 `reference-led, context-anchored` 的工作流。目标不是盲目延续当前产品已经存在的视觉风格，也不是让参考压过产品本身，而是让参考主导设计方向，让真实项目上下文锚定最终结果必须忠于什么。

这个项目主要受到以下两个方向的启发：

- [Claude Design Sys Prompt](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/Claude-Design-Sys-Prompt.txt)
- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md)

## 这个项目是做什么的

**Design Context UI** 用来帮助 agent 走一条更接近真实设计协作的路径：

- 先认真读取项目上下文
- 再用成熟设计参考主导视觉方向
- 最后把设计语言翻译成可执行实现决策

skill 执行流程是：

1. 理解需求和目标界面
2. 读取项目上下文，理解产品事实、信息结构、可复用组件、技术约束和值得保留的既有信号
3. 通过 `catalog.md` 做路由
4. 只读取最接近的 1 到 3 份设计参考
5. 输出 design readout
6. 把参考语言翻译成贴合上下文的实现决策
7. 如果进入探索模式，先出多个方向，再收敛到一个方向
8. 回到代码里实现
9. 检查代码质量和视觉质量

## 解决的问题

许多 agent 在设计 UI 时会出现这些问题：

- 过度贴合当前 UI，做不出更强结果
- 只会说“高级、极简、科技感”，却落不到具体设计决策
- 参考太多，最后变成风格拼贴
- 因为页面已经存在，就机械保留很多其实并不好的旧设计
- 页面虽然能用，但还是不像一个真正被设计过的产品

这个 skill 主要就是为了解决这些问题。

## 核心特点

- **上下文锚定**
  项目上下文解析，用于理解产品事实、信息结构、约束、实现条件，以及哪些既有信号值得保留。

- **设计案例参考**
  参考设计库解析，用于选择和吸收最适合项目的成熟设计语言。

- **显式设计读解**
  在动代码前，先说明借了什么、不借什么、当前任务优化什么。

- **小范围参考路由**
  通过 `catalog.md` 路由收敛，只读最相关的 1 到 3 份参考。

- **参考转实现**
  不只看风格说明，而是把颜色、排版、密度、层级和组件都转成实现决策。

- **先探索、后实现**
  在探索模式中，必须先给方向，再选方向，最后实现。

- **拒绝产品安全型平庸**
  目标不是默认贴近旧 UI，而是做出更强、更明确、更有判断力的结果。

- **视觉与技术一起验证**
  不只检查能不能跑，也检查有没有又退回通用模板。

## 快速开始

### 安装到 Codex

```bash
git clone https://github.com/DonkeyKing01/design-context-ui-skill.git
cp -r design-context-ui-skill/design-context-ui ~/.codex/skills/design-context-ui
```

### 安装到 Claude Code

```bash
git clone https://github.com/DonkeyKing01/design-context-ui-skill.git
cp -r design-context-ui-skill/design-context-ui ~/.claude/skills/design-context-ui
```

### 手动安装

只要保留下面这个结构即可：

```text
design-context-ui/
  SKILL.md
  references/
    catalog.md
    designs/
      ...
```

核心文件是 [design-context-ui/SKILL.md](./design-context-ui/SKILL.md) 和整个 `references/` 目录。

## 如何使用

### 设计新页面

```text
/design-context-ui

为我们的产品做一个 landing page
```

这时 skill 会：

1. 先读项目，理解产品在做什么
2. 通过 `references/catalog.md` 路由
3. 读取最接近的 1 到 3 份参考
4. 输出紧凑的 design readout
5. 在代码里实现一个更强方向

### 重构已有页面

```text
/design-context-ui

这是我们现在的前端页面，用 claude 风格重做
```

这时 skill 会：

1. 先读项目上下文
2. 选择最接近的参考
3. 提炼可迁移特征和不可直接复制的品牌细节
4. 把参考语言映射到当前技术栈
5. 实现一个更强的方向

### 探索多个设计方向

```text
/design-context-ui

这个新页面先给我 2 到 3 个方向，再实现最合适的一个。
```

这时 skill 会：

1. 进入 `design exploration`
2. 产出 2 到 3 个有明确差异的方向
3. 解释每个方向的 rationale
4. 根据用户反馈或上下文收敛到一个方向
5. 实现设计方向

## skill 的工作方式

它遵循一条固定主线：

`理解需求 -> 读取项目上下文 -> 通过 catalog.md 做路由 -> 读取最合适的设计参考 -> 选择交付模式 -> 外化设计读解 -> 从参考中提炼贴合上下文的实现决策 -> 如果在探索模式下先给方向并选定一个 -> 在现有栈中实现 -> 校验代码与视觉质量 -> 简短交付`

相比“直接给 agent 一份设计参考”，design-context-ui 更强调：

- **先读产品，但不被旧 UI 困住**
- **让参考主导设计判断**
- **先写设计读解，再写代码**
- **先探索，再实现**
- **最终输出必须是可落地代码，而不是灵感板**

## 参考库内容

当前参考库覆盖了多类常见产品风格，包括：

- AI / LLM Platform
- Developer Tools / IDE
- Backend / Database / DevOps
- Productivity / SaaS
- Design / Creative Tools
- Fintech / Crypto
- E-commerce / Retail
- Media / Consumer Tech
- Automotive

目录索引在 [catalog.md](./design-context-ui/references/catalog.md)。

每份详细设计参考通常包含：

- 整体氛围与视觉气质
- 颜色系统与语义角色
- 字体层级与可替代字体
- 按钮、卡片、输入框、导航等组件风格
- 栅格、留白、圆角和密度节奏
- 阴影、层次和表面处理
- 风格边界与可迁移原则

## 项目结构

```text
design-context-ui-skill/
  design-context-ui/
    SKILL.md
    references/
      catalog.md
      designs/
        ai_llm_platforms/
        productivity _ saas/
        developer tools _ ides/
        ...
  ref/
    Claude-Design-Sys-Prompt.txt
    ...
```

- `design-context-ui/SKILL.md`
  skill 的主流程和行为规则
- `design-context-ui/references/catalog.md`
  用来先选最相关参考的路由目录
- `design-context-ui/references/designs/*`
  具体设计参考文件，每份描述一种品牌化视觉语言
- `ref/Claude-Design-Sys-Prompt.txt`
  影响了这份 skill 写法、节奏和设计导演感的源材料

## 项目初心

这个项目的出发点很简单：

我想保留“先读真实项目上下文”这件事的价值，但不再让现有 UI 自动成为默认审美源头。

design-context-ui 不是一个完整设计系统，也不是一个万能审美 prompt。
它更像一个可复用的工作流外壳，强调三件事：

- 先理解产品事实
- 再让参考主导设计
- 最后把设计翻译成代码

## License

MIT
