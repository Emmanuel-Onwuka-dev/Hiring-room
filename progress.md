# Hiring Room - Progress Log

Last updated: Nov 5, 2026. Hackathon closes Nov 7, 11:59 PM IST.

## Goal
Track 1 - Best Business Workflow ($2,000). Build a practical workflow where humans + AI agents get real work done in team chat via Switch.

## What Switch is (recap)
- Not a chat app, not an agent. It's the pipe: `Agents <-> Switch Room <-> Team chat (Slack/Teams/Discord/Mattermost)`.
- People talk in their normal chat channel. That channel becomes a Room (shared history, rules, tasks, decisions).
- Agents join like teammates with name/avatar, called via @mention.
- Setup tool: Switch Console (desktop app) + Docker on laptop. Mattermost included free for demo (no Slack admin needed).
- Switch ships no agents/models. We bring Claude Code / Codex / OpenCode + chat, Switch connects them.

## Our idea: Hiring Room (CV reviewer chain)
Human drops CV in #hiring-room → 3 agents process in order → human approves.

1. `@hiring-screener` (anyone) - scores CV 0-100 vs JD in Room Rules. PASS (>=70) calls bias-checker, REJECT stops.
2. `@hiring-bias-checker` (owner-agents only) - audits screener reasoning for bias. CLEARED calls interviewer, FLAGGED stops for manager review.
3. `@hiring-interviewer` (owner-agents only) - posts interview pack (5 questions + 30-min plan + rubric) as Room Task. Waits for human.
4. Hiring manager (human) - says Approved/Rejected in thread → logged as Decision.

Why 3 agents: screener finds talent, bias-checker makes it fair, interviewer makes it actionable. Without shared Room they'd lose JD/history/decisions.

## Files created
- `agent-instructions.md` - index: chain, room setup, kickoff message, example JD, demo CV plan, template sketch
- `agents/hiring-screener.md` - Agent 1 prompt (paste into Console)
- `agents/hiring-bias-checker.md` - Agent 2 prompt
- `agents/hiring-interviewer.md` - Agent 3 prompt
- This file: `progress.md`

## Example JD (for Room Rules)
Role: Backend Intern (Lagos/Remote). Must-haves: Python, REST APIs, git, basic SQL. Nice: Docker, tests. Reject if no code evidence.

## Demo plan (for video, ~90 sec)
1. Recruiter posts JD once → Room Rules.
2. Drop 3 fake CVs: ada-strong.pdf (PASS+CLEAR), ben-weak.pdf (REJECT), cynthia-borderline.pdf (PASS then FLAGGED/discussed).
3. Show chain @mentions in thread, Task created, manager Approves 1.

## Environment
- Machine: Windows, CPU arch AMD64 (checked via $env:PROCESSOR_ARCHITECTURE). Use Docker Desktop Windows x86_64/AMD64 installer, not ARM64.
- Docker blocked on: "Virtual Machine Platform Windows feature not enabled" + per-user install lacks admin rights.

## Docker fix (do once, needs admin + restart)
1. Close Docker installer.
2. Win key → type PowerShell → right-click → Run as administrator → Yes.
3. Run: `wsl --install`
4. Restart computer.
5. Re-run Docker Desktop installer (same AMD64 one), open Docker Desktop, wait for running/green.
- Alt path: right-click Docker installer → Run as administrator → All-users installation (enables feature, then restart).
- If `wsl --install` says virtualization off: enable VT-x/AMD-V in BIOS.

## Current status
- [x] Explained Switch + Track 1 rules
- [x] Chose Hiring Room idea, designed 3-agent chain
- [x] Wrote agent instruction files (split per-agent)
- [x] Confirmed Docker arch: AMD64
- [x] Finish Docker Desktop install (user confirmed installed + running Nov 5)
- [x] Install Switch Console (user confirmed installed + opened Nov 5)
- [x] Run quickstart: server running, switch-buddy on Claude Code answered, Mattermost connected
- [x] Create hiring-room + 3 agents by pasting prompts (buddy built, outputs confirm detailed prompts active)
- [x] Create fake JD + 3 fake CVs for testing (demo-cvs/*.txt: ada-strong, ben-weak, cynthia-borderline)
- [x] Test chain end-to-end in chat (Ada 80 CLEAR+pack, ben 5 REJECT-stop, cynthia 78 CLEAR+pack with fairness note)
- [x] Record demo video + write README showing Switch usage (video https://youtu.be/AvHYJfYuya8)
- [ ] Submit before Nov 7, 11:59 PM IST

## Key links
- Hackathon: https://www.wemakedevs.org/hackathons/switch
- Resources: https://www.wemakedevs.org/hackathons/switch/resources
- Quickstart: https://docs.switchagents.ai/switch-rooms/getting-started
- Switch framework: https://docs.switchagents.ai/switch-rooms/building/index
- Releases (Console): https://github.com/sandbox-quantum/switch/releases/latest
- Discord help: https://discord.gg/E2rWw2Yhsm

## Next action on restart
Resume at: Build complete. Video recorded, README linked. Only step left: submit repo + video before Nov 7 11:59 PM IST.
