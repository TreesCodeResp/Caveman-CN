# caveman-cn

中文极简回复模式。砍废话保技术实质。

## 来源

本项目基于 [caveman](https://github.com/JuliusBrussee/caveman) 进行中文本地化适配。

## 🚀 快速安装

```bash
npx skills add TreesCodeResp/Caveman-CN
```

指定 Agent 安装：

| Agent | 命令 |
|-------|------|
| Claude Code | `npx skills add TreesCodeResp/Caveman-CN -a claude-code` |
| Cursor | `npx skills add TreesCodeResp/Caveman-CN -a cursor` |
| GitHub Copilot | `npx skills add TreesCodeResp/Caveman-CN -a github-copilot` |
| CodeBuddy | `npx skills add TreesCodeResp/Caveman-CN -a codebuddy` |

### Codex

<details>
<summary><strong>Codex — 完整说明</strong></summary>

**macOS / Linux：**
1. Clone 本仓 → 在仓目录内打开 Codex → `/plugins` → 搜索 "Caveman-CN" → Install
2. repo-local 自动激活已由 `.codex/hooks.json` + `.codex/config.toml` 配置

**Windows：**
1. 先启用符号链接：`git config --global core.symlinks true`（需管理员或开发者模式）
2. Clone 本仓 → 打开 VS Code → Codex Settings → Plugins → 在本地 marketplace 中找到 "Caveman-CN" → Install → Reload Window
3. Codex hooks 在 Windows 下当前禁用，用 `$caveman-cn` 手动启动 

本仓通过 `.codex/hooks.json` + `.codex/config.toml` 实现自动激活，macOS/Linux 下在本仓内启动 Codex 时自动生效。除了 `SessionStart` 首次注入外，`UserPromptSubmit` hook 在每次用户输入时追加简短强化提示，防止长对话中极简模式漂移。安装的插件提供 `$caveman-cn` 命令；若想在其他仓库也启用自动激活，复制相同的 hook 并启用：

```toml
[features]
codex_hooks = true
```

</details>

### Windows 用户

Windows 符号链接需管理员权限或开发者模式。如安装报错，加 `--copy` 改用文件复制：

```bash
npx skills add TreesCodeResp/Caveman-CN --copy
```

> Codex 说明：上游 `caveman` README 已提示 Windows 下 repo-local Codex hooks 可能需要手动触发。`caveman-CN` 仍提供 `.codex/hooks.json`，但需以本机实际行为为准验证。

### 非交互安装（CI/CD）

加 `--yes` 跳过所有确认提示：

```bash
npx skills add TreesCodeResp/Caveman-CN --yes
```

## 📖 使用说明

安装后，skill 会自动激活。你也可以用命令切换强度：

| 命令 | 说明 |
|------|------|
| `/caveman-cn 轻量` | 去客套、去语气词，保留完整句子 |
| `/caveman-cn 标准` | 默认模式，砍连接词，片段句 OK |
| `/caveman-cn 极限` | 最大压缩，缩写+箭头因果 |
| `停止极简` / `正常模式` | 退出极简模式 |

### 强度示例

**问题**："React 组件为什么重复渲染？"

- **轻量**："每次渲染创建新对象引用，导致重渲染。用 `useMemo` 包裹。"
- **标准**："新引用 = 重渲染。`useMemo` 包裹。"
- **极限**："内联 obj → 新引用 → 重渲染。`useMemo`。"

### Codex 使用

- Codex 使用 `$caveman-cn` 语法，不是 `/caveman-cn`
- 本仓通过 `.codex/hooks.json` 自动激活（`SessionStart` 注入 + `UserPromptSubmit` 每轮强化）；安装的插件提供 `$caveman-cn` 命令
- 若想在其他仓库也启用自动激活，复制相同的 `SessionStart` hook 并启用 `codex_hooks`
- 退出：`停止极简` / `正常模式`

## 🔧 手动配置

如果 `npx skills add` 不可用或不支持你的 Agent，可手动复制 `skills/caveman-cn/SKILL.md` 的内容到对应位置：

- Claude Code → `.claude/skills/caveman-cn.md`
- Codex (plugin) → Clone Repo → 在仓目录内打开 Codex → `/plugins` → 搜索 "Caveman-CN" → Install
- Cursor → `.cursor/rules/caveman-cn.mdc`
- GitHub Copilot → `.github/copilot-instructions.md`
- CodeBuddy（项目级）→ `.codebuddy/skills/caveman-cn/SKILL.md`
- CodeBuddy（用户级）→ `~/.codebuddy/skills/caveman-cn/SKILL.md`

## ⚙️ 配置原则

**保留（不可省）**：
- 精确性：数字/命令(含 flag)/术语/公式/代码块/变量名
- 完整性：并列条目只压描述不合并
- 安全性：安全选项不降级（如 `--force-with-lease` 不简化为 `--force`）

**自动暂停场景**：
- 安全警告
- 不可逆操作
- 多步顺序易误读
- 用户追问"什么意思"

## 📝 项目结构

```
Caveman-CN/
├── .agents/
│   └── plugins/
│       └── marketplace.json       # Codex 本地插件发现索引
├── .codex/
│   ├── config.toml                # 启用 codex_hooks
│   └── hooks.json                 # SessionStart 首次注入 + UserPromptSubmit 每轮强化
├── plugins/
│   └── caveman-cn/
│       ├── .codex-plugin/
│       │   └── plugin.json        # 插件 manifest（名称、skill 路径、元数据）
│       ├── assets/
│       │   ├── caveman-cn.svg
│       │   └── caveman-cn-small.svg
│       └── skills/
│           └── caveman-cn/
│               ├── agents/
│               │   └── openai.yaml # Agent 元数据（显示名、默认 prompt）
│               └── SKILL.md       # 插件内 skill 镜像（从根级 skill 同步）
├── skills/
│   └── caveman-cn/
│       └── SKILL.md      # Skill 定义（npx skills 读取）
├── .gitignore
├── LICENSE
└── README.md
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 许可证

[MIT License](LICENSE)
