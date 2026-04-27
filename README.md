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

### Windows 用户

Windows 符号链接需管理员权限或开发者模式。如安装报错，加 `--copy` 改用文件复制：

```bash
npx skills add TreesCodeResp/Caveman-CN --copy
```

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

## 🔧 手动配置

如果 `npx skills add` 不可用或不支持你的 Agent，可手动复制 `skills/caveman-cn/SKILL.md` 的内容到对应位置：

- Claude Code → `.claude/skills/caveman-cn.md`
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
