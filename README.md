# research-ppt

用于科研组会的中英文混排学术 PPT 工作流技能。根据论文原文、汇报背景和风格参考图，在 ChatGPT 的 Pictures 项目内分步提交制作请求，目标产物为 16:9、主要文字可编辑的完整 PPTX。

## 用途

- 文献汇报：围绕具体论文的科学问题、研究设计、方法和关键结果组织内容。
- 调研汇报：围绕领域发展、方法分类、代表工作、共性问题和研究机会组织内容，重点展开两至三篇核心论文。
- 局部精调：在已有 PPTX 上，按用户明确指定的页码和要求修改。

工作流分为三个步骤：

1. 提交四套不同主题色的幻灯片缩略总览生成请求，供用户选择。
2. 用户选定方案后，在原会话提交完整 PPTX 制作请求。主要文字使用原生文本框，论文图和复杂视觉保留高清局部图片。
3. 用户提出具体修改后，在原会话提交指定页面的局部精调请求。

每步确认请求已成为会话中的新用户消息后即停止，等待用户下一次指令。提交成功不代表成品已经生成或通过检查；检查、下载须由用户后续明确要求。

科研内容依据论文原文，参考图只提供视觉风格。技能要求区分实证结果、综合判断和待验证假设，不使用生成图替代真实科研证据。

## 依赖

| 依赖 | 要求 |
| --- | --- |
| Codex 技能运行环境 | 能发现并读取 `SKILL.md` 和本地附件。 |
| 浏览器操作工具 | 能操作 ChatGPT 网页、上传附件、检查界面状态并保留会话。配套技能优先使用 `mcp__cua_repl.js`；主技能发送后使用 `tab.markHandoff()`。 |
| `chatgpt-pictures` 技能 | 必须单独安装，负责 Pictures 项目定位、附件上传、Pro 设置检查和网页提交。当前仓库未包含该技能，也未提供其下载地址；需要使用已有安装或向维护者获取。 |
| ChatGPT 网页会话 | 已登录，能够访问自己的 Pictures 项目，并在发送前实际选中并确认 `Pro` 设置。付费订阅本身不等于已选中该设置。 |
| 汇报材料 | 核心论文原文，以及汇报目的、听众背景、时长或页数限制、研究阶段等背景资料。背景信息按实际需要提供，不从风格参考图推断研究内容。 |
| Git | 用于下方克隆安装方式。 |

本仓库由技能指令和参考图片组成，没有本地 PPT 生成程序或包依赖清单；安装本仓库无需运行 `pip install` 或 `pnpm install`。PPT 制作请求通过 ChatGPT 网页提交。

## 安装

以下命令适用于 macOS / Linux shell，安装到用户级技能目录。当前 OpenAI 官方文档列出的目录为 `~/.agents/skills`，详见 [Build skills](https://learn.chatgpt.com/docs/build-skills)。

### 1. 安装本技能

目标目录 `~/.agents/skills/research-ppt` 应尚不存在：

```bash
mkdir -p "$HOME/.agents/skills"
git clone https://github.com/weiyu1218/research-ppt.git "$HOME/.agents/skills/research-ppt"
```

克隆会同时保留 `SKILL.md` 与 `assets/reference.png`，不要只复制技能正文而遗漏参考图。

### 2. 安装并适配配套技能

将获得的 `chatgpt-pictures` 完整技能目录放入同一个用户级技能目录，使其入口为 `~/.agents/skills/chatgpt-pictures/SKILL.md`。如果已经安装在其他可发现的目录，可使用现有安装。

打开已安装的 `research-ppt/SKILL.md`，将其中两处指向 `/Users/fwy/.codex/skills/chatgpt-pictures/SKILL.md` 的依赖链接改为本机 `chatgpt-pictures/SKILL.md` 的实际绝对路径。Markdown 链接目标应填写展开后的完整路径，不直接填写 `$HOME`。

检查配套 `chatgpt-pictures/SKILL.md` 中的 Pictures 项目地址。配套技能目前含有维护者环境的特定项目链接，其他账号应使用自己实际可访问的 Pictures 项目地址，不能直接假定原链接适用。

### 3. 确认技能可用

确认 Codex 的技能列表中同时存在 `research-ppt` 和 `chatgpt-pictures`。按官方文档，安装后若技能没有出现，可重启 Codex。

在浏览器中登录 ChatGPT，确认自己的 Pictures 项目可访问，并且提交界面提供可选的 `Pro` 设置。无法确认这些条件时，技能会停止提交并说明阻碍。

## 使用

在 Codex 中调用 `$research-ppt`，附上论文并说明汇报类型、目的和听众背景，例如：

```text
$research-ppt
请根据上传的论文制作调研汇报，面向熟悉机器学习但生物学背景较少的课题组成员。
先执行第一步，使用技能自带的参考图。
```

随后查看 Pictures 会话中的预览，选择方案并明确要求执行第二步。需要检查、下载或修改时，再发出相应指令；局部修改须提供页码和具体要求。

详细提示词和执行边界见 [SKILL.md](SKILL.md)，默认风格参考见 [assets/reference.png](assets/reference.png)。
