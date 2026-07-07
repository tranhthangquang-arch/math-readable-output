# Readable Math Output Skill

Readable Math Output is a small Codex skill for making formula-heavy answers easier to read in Codex chat.

It is designed for conversations that include equations, derivations, algorithms, control theory, signal processing, statistics, optimization, machine learning objectives, matrices, vectors, or paper-style math explanation.

## Why This Skill Exists

Some Codex chat surfaces render block LaTeX well but display inline `$...$` math literally. That makes variable explanations and short formulas harder to read.

This skill nudges Codex toward a more readable style:

- Use block formulas for important equations.
- Use `aligned`, `cases`, and matrix environments for structured math.
- Avoid inline `$...$` math in prose and bullets.
- Use direct Unicode symbols such as λ, θ, and φ for simple variables.
- Use code-style or plain text only when it is clearer than inline LaTeX.
- Explain symbols in short, readable bullets.

## Example

Instead of writing variable explanations like this:

```markdown
- $lambda$: forgetting factor.
- $theta$: parameter vector.
- $\lambda^{k-i}$: old-data weight.
```

Prefer:

```markdown
- λ: forgetting factor.
- θ: parameter vector.
- λ^(k−i): old-data weight.
```

When the expression deserves proper rendering, place it in a block formula:

```latex
$$
\lambda^{k-i}
$$
```

## Installation

Clone this repository into your Codex skills directory:

```powershell
git clone https://github.com/tranthangquang-arch/math-readable-output.git "$env:USERPROFILE\.codex\skills\math-readable-output"
```

Then restart Codex so the skill metadata is reloaded.

## Usage

You can invoke it explicitly:

```text
Use $math-readable-output to explain the RLS update equations.
```

The skill is also written to trigger by default whenever Codex plans to output formulas, symbolic math, derivations, matrices, recurrence relations, or algorithm update rules.

## Repository Structure

```text
math-readable-output/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── README.md
├── LICENSE
└── .gitignore
```

## Notes

This skill does not change Codex's renderer. It only improves the source formatting Codex uses for formula-heavy answers.

## License

MIT
