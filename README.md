# Zachary Woods

I build AI tools, desktop software, and automation for real operational workflows.

My work focuses on the parts that make an agent useful beyond a demo: process control, scoped access, human review, and evidence that the system behaved as intended.

## Selected work

- **ONNX:** [Merged Resize performance contribution](https://github.com/onnx/onnx/pull/7920). Replaced recursive interpolation with vectorized, separable interpolation in the reference evaluator.
- **Shelly:** A completed Rust and TypeScript desktop shell for Claude Code and Codex. Agent turns become interactive pages; replies return to the owning terminal session. The project is EOL: its interaction model has since converged with mainstream agent clients, and solo maintenance is no longer planned. The [sanitized historical source archive](https://github.com/mrgyatso/shelly-archive) and [browser demo](https://share.aletheia.dev/companion/) remain available as engineering and product/interface references.
- **Keyhole:** A Go prototype for scoped endpoint diagnostics, on-device redaction, audit trails, and approval-gated file changes. Validated in an experimental Windows environment; source repository currently private.

## Engineering walkthroughs

- [ONNX Resize: making interpolation separable](case-studies/onnx-resize.md) — algorithm, compatibility details and evidence.
- [Shelly: reviewing agent work through interactive pages](case-studies/shelly.md) — process ownership, page rendering, reply delivery and the EOL decision.

[Portfolio](https://aletheia.dev) · [LinkedIn](https://www.linkedin.com/in/zachwoodscs)
