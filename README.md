# Zachary Woods

I build AI tools, desktop software, and automation for real operational workflows.

My work focuses on the parts that make an agent useful beyond a demo: process control, scoped access, human review, and evidence that the system behaved as intended.

## Selected work

- **ONNX:** [Merged Resize performance contribution](https://github.com/onnx/onnx/pull/7920). Replaced recursive interpolation with vectorized, separable interpolation in the reference evaluator.
- **Shelly:** A completed Rust and TypeScript desktop shell for Claude Code and Codex. Agent turns become interactive pages; replies return to the owning terminal session. The project is EOL: its interaction model has since converged with mainstream agent clients, and solo maintenance is no longer planned. The [sanitized historical source archive](https://github.com/mrgyatso/shelly-archive) and [browser demo](https://share.aletheia.dev/companion/) remain available as engineering and product/interface references.
- **Keyhole:** An experimental Go/NATS system for scoped endpoint diagnostics, on-device redaction, audit trails, and approval-gated file changes. The [public historical demo snapshot](https://github.com/mrgyatso/keyhole-demo) includes a [recorded local fixture walkthrough](https://github.com/mrgyatso/keyhole-demo/blob/main/docs/DEMO-TRANSCRIPT.md) covering access decisions, reviewed changes, rollback, revocation and audit verification. Newer feature work is separate from that snapshot.

## Engineering walkthroughs

- [ONNX Resize: making interpolation separable](case-studies/onnx-resize.md) — algorithm, compatibility details and evidence.
- [Shelly: reviewing agent work through interactive pages](case-studies/shelly.md) — process ownership, page rendering, reply delivery and the EOL decision.

## Historical projects

[Engineering archive](https://github.com/mrgyatso/engineering-archive) collects Bongo Claude, Dev Mill, MockChain, CodeCanvas, QueryLens and SmartCI. Each snapshot states what works, what remains incomplete, how it was checked and why it is no longer maintained.

[Portfolio and resume](https://zachary-woods-world.mrgyatso.chatgpt.site/work) · [Interactive portfolio](https://zachary-woods-world.mrgyatso.chatgpt.site/) · [LinkedIn](https://www.linkedin.com/in/zachwoodscs)
