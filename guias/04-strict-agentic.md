# 04 — Ativar Strict Agentic no OpenClaw 4.24

ATENCAO: Sempre faca backup antes de comecar. O prompt abaixo ja inclui isso.

## Prompt Completo (cole no agente)

Before we get started, the first thing you always want to do is make a backup. Do that now.

You are verifying the exact OpenClaw setup.
Goal: Update OpenClaw to 4.24, then verify that the system matches these three config lines:
- agents.defaults.embeddedPi.executionContract = "strict-agentic"
- plugins.entries.codex.enabled = true
- agents.defaults.model = "codex/gpt-5.5"

Tasks:
1. Back up the current OpenClaw config before changing anything.
2. Check the installed OpenClaw version.
3. Update OpenClaw to 4.24 if needed.
4. Inspect the live config and verify whether these three lines are present.
5. If any line is missing or different, show exact current and intended value.
6. Apply the minimum changes needed to match the intended setup.
7. Re-check the config after changes.
8. Confirm whether the final setup matches all three lines.
9. Do not enable extra settings beyond what is required.

Constraints:
- Do not hallucinate success.
- Show exact values before and after.
- Keep the changes minimal.
- If something cannot be verified, say so clearly.

---

*Proximo: 05-skill-audit.md*