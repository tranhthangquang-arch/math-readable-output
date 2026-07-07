---
name: math-readable-output
description: Default formatting policy for any answer that contains mathematical formulas, symbolic variables, equations, derivations, proofs, algorithm equations, control theory, signal processing, statistics, optimization, machine learning objectives, matrices, vectors, recurrence relations, LaTeX, or paper-style math explanation. Always use this skill whenever Codex will output formulas or symbolic math, even if the user does not explicitly request readable formula formatting. Use for readable formula output, math explanation, derivation, algorithm formulas, RLS, Kalman, adaptive filters, control systems, signal processing, probability, statistics, linear algebra, optimization, and scientific paper explanations.
---

# Math Readable Output

## Overview

Make math-heavy Codex answers readable even when the chat UI does not render LaTeX perfectly. Prefer spacious block formulas, aligned derivations, and short variable explanations over dense inline notation.

## Default Invocation

- Use this skill by default whenever an answer will contain formulas, equations, symbolic variables, derivations, proofs, matrices, vectors, optimization objectives, recurrence relations, or algorithm update rules.
- Use this skill even when the user asks a general technical question and formulas are only part of the answer.
- Do not wait for explicit phrases such as "use readable math" or "format the formula"; formula-bearing answers should opt into this formatting style automatically.

## Output Rules

- Put important equations in block math using `$$ ... $$`; avoid burying long formulas in prose.
- Use `aligned`, `cases`, `bmatrix`, or `pmatrix` for multi-line derivations, piecewise definitions, and matrices.
- Break long equations at semantic points: objective equals, summation term, constraints, update equation, or approximation.
- Keep explanatory prose outside the formula block; introduce the equation in one sentence, then explain it after the block.
- Use one short bullet list to define variables after a formula when symbols are not obvious.
- Do not use inline dollar math such as `$theta$`, `$y(i)$`, or `$lambda$` in bullets or prose; Codex chat may display the delimiters literally.
- In variable bullets and short prose, prefer plain Unicode math symbols directly when they are simple: Greek lambda (U+03BB), theta (U+03B8), phi/varphi (U+03C6/U+03D5), superscript T when useful, and ordinary function forms like J(k), y(i), theta(k), P(k).
- Use code-style symbols only for ASCII fallback, literal code variables, or expressions that look worse as Unicode text.
- For complex powers, fractions, matrices, or long transposed products, use a separate block formula instead of inline LaTeX.
- Reserve rendered LaTeX only for block formulas when the expression deserves visual display.
- For formulas that may not render, add a compact "plain-text reading" only when it improves clarity.
- Avoid excessive LaTeX cleverness, custom macros, and cramped inline fractions.

## Preferred Patterns

Use this for standalone equations:

```latex
$$
J(k)
= \sum_{i=1}^{k} \lambda^{k-i}
  \left[y(i)-\varphi^{T}(i)\theta\right]^2,
\qquad 0 < \lambda \le 1
$$
```

Use this for derivations or update rules:

```latex
$$
\begin{aligned}
K(k)
&= \frac{P(k-1)\varphi(k)}
        {\lambda + \varphi^{T}(k)P(k-1)\varphi(k)} \\
\theta(k)
&= \theta(k-1)
   + K(k)\left[y(k)-\varphi^{T}(k)\theta(k-1)\right] \\
P(k)
&= \frac{1}{\lambda}
   \left[I-K(k)\varphi^{T}(k)\right]P(k-1)
\end{aligned}
$$
```

Use this for constraints:

```latex
$$
\begin{aligned}
\min_{\theta}\quad
& \sum_{i=1}^{k} \lambda^{k-i}
  \left[y(i)-\varphi^{T}(i)\theta\right]^2 \\
\text{s.t.}\quad
& 0 < \lambda \le 1
\end{aligned}
$$
```

## Explanation Style

- Start with the main idea in plain language.
- Present the formula as a visual block.
- Explain symbols in 3-6 bullets using direct symbols or plain text, not inline `$...$` math delimiters.
- Explain the intuition after the symbols, especially for forgetting factors, weights, gains, covariance, loss functions, and constraints.
- When comparing formulas, place them in separate blocks with short labels rather than one dense paragraph.
- If the user asks for image-like or more readable math formatting, optimize spacing and line breaks over compactness.

## Avoid

- Do not use a single long inline formula when a block formula is clearer.
- Do not put inline `$...$` math inside Chinese or English prose unless the renderer is known to support it.
- Do not write LaTeX fragments such as `\lambda^{k-i}` inside bullets; use a direct symbol/plain-text approximation in bullets, and put the rendered version in a separate block formula if needed.
- Do not mix Chinese punctuation inside LaTeX unless it is plain text inside `\text{...}`.
- Do not over-explain every elementary symbol if the user already knows the domain.
- Do not claim the Codex UI will render formulas like KaTeX or MathJax; this skill only improves source formatting and readability.
