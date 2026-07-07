# Readable Math Output Skill   codex公式格式修改

Readable Math Output is a small Codex skill for making formula-heavy answers easier to read in Codex chat.

It is designed for conversations that include equations, derivations, algorithms, control theory, signal processing, statistics, optimization, machine learning objectives, matrices, vectors, or paper-style math explanation.

## 中文说明

这是一个用于改善 Codex 数学公式输出体验的本地 skill。它不会修改 Codex 的公式渲染引擎，而是通过约束回答格式，让包含公式、变量、推导和递推关系的回答更容易阅读。

适合这些场景：

- 解释数学公式、算法公式、目标函数、损失函数。
- 推导控制理论、信号处理、自适应滤波、RLS、Kalman 等公式。
- 阅读论文中的符号表达、矩阵表达、优化问题。
- 避免 Codex 在正文里输出难读的行内 `$...$` LaTeX。

这个 skill 的核心规则是：

- 重要公式使用块级 LaTeX，也就是 `$$ ... $$`。
- 多行推导使用 `aligned`，分段函数使用 `cases`，矩阵使用 `bmatrix` 或 `pmatrix`。
- 正文和项目符号中不使用行内 `$...$`，避免 Codex 聊天框把美元符号原样显示出来。
- 简单变量优先直接显示为 Unicode 符号，例如 `λ`、`θ`、`φ`。
- 复杂表达式如果需要漂亮显示，就单独放进块级公式。

## 为什么需要它

Some Codex chat surfaces render block LaTeX well but display inline `$...$` math literally. That makes variable explanations and short formulas harder to read.

This skill nudges Codex toward a more readable style:

- Use block formulas for important equations.
- Use `aligned`, `cases`, and matrix environments for structured math.
- Avoid inline `$...$` math in prose and bullets.
- Use direct Unicode symbols such as `λ`, `θ`, and `φ` for simple variables.
- Use code-style or plain text only when it is clearer than inline LaTeX.
- Explain symbols in short, readable bullets.

## 示例

不要这样写变量解释：

```markdown
- $lambda$: forgetting factor.
- $theta$: parameter vector.
- $\lambda^{k-i}$: old-data weight.
```

推荐这样写：

```markdown
- λ: forgetting factor.
- θ: parameter vector.
- λ^(k−i): old-data weight.
```

如果表达式需要漂亮显示，就单独放进块级公式：

```latex
$$
\lambda^{k-i}
$$
```

## Installation

Clone this repository into your Codex skills directory:

```powershell
git clone https://github.com/tranhthangquang-arch/math-readable-output.git "$env:USERPROFILE\.codex\skills\math-readable-output"
```

Then restart Codex so the skill metadata is reloaded.

## 安装方式

把仓库克隆到 Codex 的 skills 目录：

```powershell
git clone https://github.com/tranhthangquang-arch/math-readable-output.git "$env:USERPROFILE\.codex\skills\math-readable-output"
```

然后重启 Codex，让新的 skill metadata 生效。

## Usage

You can invoke it explicitly:

```text
Use $math-readable-output to explain the RLS update equations.
```

The skill is also written to trigger by default whenever Codex plans to output formulas, symbolic math, derivations, matrices, recurrence relations, or algorithm update rules.

## 使用示例

可以显式调用：

```text
Use $math-readable-output 解释一下带遗忘因子的 RLS 目标函数和递推公式
```

也可以在普通问题中自动触发。只要回答里涉及公式、符号变量、矩阵、优化目标、递推公式或推导过程，Codex 就会尽量使用这个更易读的数学输出风格。

## Repository Structure

```text
math-readable-output/
|-- SKILL.md
|-- agents/
|   `-- openai.yaml
|-- README.md
|-- LICENSE
`-- .gitignore
```

## Notes

This skill does not change Codex's renderer. It only improves the source formatting Codex uses for formula-heavy answers.

## 注意事项

这个 skill 不能让 Codex 聊天框真正变成 MathJax 或 KaTeX 渲染器。它做的是“输出格式约束”：让公式尽量使用块级排版，让变量解释尽量使用直接符号或普通文本，从而提高可读性。

## License

MIT
