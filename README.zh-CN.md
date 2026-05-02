# Tasteful UI

[English](./README.md) | **中文**

![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)
![Type: Skill](https://img.shields.io/badge/Type-Skill-blue)
![Focus: UI Design](https://img.shields.io/badge/Focus-UI%20Design-orange)

一个让 coding agent 先判断 taste，再选择参考，最后实现 UI 的设计 skill；

在设计中，流程、taste、reference，同样重要。

本人对 ui 设计当前理解有限，skill 实际效果可能并不惊艳，但希望更多从思路和流程上为有共同兴趣的开发者们提供帮助

## 效果

均使用 codex gpt5.5 模型

### 数据面板
原项目 [EV-PM-DSS]()

Prompt:

```text
为当前项目设计一个面向产品经理的数据面板，可切换中英文，轻量级数据筛选交互
```

<table>
  <tr>
    <th width="50%">直接开发 1</th>
    <th width="50%">使用 Tasteful UI 1</th>
  </tr>
  <tr>
    <td><img src="./docs/ev-pm-dss-direct-1.png" alt="EV PM DSS direct result 1"></td>
    <td><img src="./docs/ev-pm-dss-skill-1.png" alt="EV PM DSS Tasteful UI result 1"></td>
  </tr>
  <tr>
    <th width="50%">直接开发 2</th>
    <th width="50%">使用 Tasteful UI 2</th>
  </tr>
  <tr>
    <td><img src="./docs/ev-pm-dss-direct-2.png" alt="EV PM DSS direct result 2"></td>
    <td><img src="./docs/ev-pm-dss-skill-2.png" alt="EV PM DSS Tasteful UI result 2"></td>
  </tr>
</table>

### 查询界面
原项目 [scholarship-query](https://github.com/DonkeyKing01/scholarship-query)

Prompt:

```text
优化当前查询界面，保持简洁美观和用户信任感
```

<table>
  <tr>
    <th width="50%">直接开发</th>
    <th width="50%">使用 Tasteful UI</th>
  </tr>
  <tr>
    <td><img src="./docs/shuping-query-direct-1.png" alt="Shuping query direct result"></td>
    <td><img src="./docs/shuping-query-skill-1.png" alt="Shuping query Tasteful UI result"></td>
  </tr>
</table>

## 参考来源

本项目受以下项目启发：

- [Claude Design Sys Prompt](https://github.com/elder-plinius/CL4R1T4S/blob/main/ANTHROPIC/Claude-Design-Sys-Prompt.txt)：探索 taste；
- [awesome-design-md](https://github.com/VoltAgent/awesome-design-md)：表达和复用风格；
- [Google DESIGN.md](https://github.com/google-labs-code/design.md)：把风格变成 agent 可执行规范；
- [21st.dev Magic](https://21st.dev/magic)：生成多变体并比较；
- [Refactoring UI](https://refactoringui.com/) / [NNGroup](https://www.nngroup.com/articles/principles-visual-design/) / [Laws of UX](https://lawsofux.com/)：评判 UI 水平。

## 当前结构

```text
tasteful-ui/
├── SKILL.md
├── modes/
├── taste/
├── references/
├── formats/
├── workflows/
└── eval/
```

### SKILL.md

router + operating principles。

决定：

- 当前任务进入哪个 mode；
- 哪些文件需要读取；
- 哪些 investment gate 必须停下；
- 最终如何交付。

### modes/

任务模式。

- `taste_first_redesign.md`：默认模式。用于重设计、个人网站、dashboard、landing page、查询页等 taste 未确认的任务；
- `production_ui_implementation.md`：只用于已有明确 design brief / mockup / screenshot / taste direction 的任务；
- `design_critique_only.md`：用于截图排序、打分、诊断，不改代码。

### taste/

审美判断系统。

- `taste_exploration.md`：先判断这个产品应该成为什么；
- `taste_critic.md`：批判一个方向或结果是否真的好；
- `anti_generic_rules.md`：防止 generic SaaS、dark dashboard、假高级、模板化。

### references/

外部风格材料。

`catalog.md` 给已确认的 taste direction 找 supporting references。

reference 是材料，不是方向本身。

### formats/

设计文档格式。

`PROJECT_DESIGN.template.md` 把 taste、项目上下文、外部参考变成 agent 可执行的设计规范。

### workflows/

执行方式。

- `variation_first.md`：方向不确定时，先出多个 taste 方向再比较；
- `implementation.md`：确认 brief 后再实现；
- `verification.md`：技术验证 + 视觉验证。

### eval/

结果评判系统。

`ui_result_critique.md` 判断：

- 是否比原 UI 好；
- reference 是有益还是限制；
- 是否只是更像模板；
- 是否应该回退某些设计。

## 工作流

1. 理解用户输入任务
2. 读取项目上下文
3. 停在 project understanding investment gate
4. 探索 taste
5. 停在 taste direction investment gate
6. 根据 taste direction 路由 `catalog.md`
7. 撰写 `PROJECT_DESIGN.md` / `design.md`
8. 停在 design brief investment gate
9. 依据 brief 完成设计实现
10. 验证
11. 评判设计结果是否真的更好
12. 交付


## 安装

### Codex

```bash
git clone https://github.com/DonkeyKing01/tasteful-ui-skill.git
cp -r tasteful-ui-skill/tasteful-ui ~/.codex/skills/tasteful-ui
```

### Claude Code

```bash
git clone https://github.com/DonkeyKing01/tasteful-ui-skill.git
cp -r tasteful-ui-skill/tasteful-ui ~/.claude/skills/tasteful-ui
```

### 手动安装

保留以下结构，复制进 agent 的 skills 文件夹中：

```text
tasteful-ui/
  SKILL.md
  modes/
  taste/
  references/
  formats/
  workflows/
  eval/
```

## License

MIT
