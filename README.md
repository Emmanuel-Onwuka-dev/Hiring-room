# Hiring Room - AI hiring workflow in team chat

Flip the Switch Hackathon (Nov 4-7, 2026). Track 1: Best Business Workflow.

## What it is

Hiring Room turns a normal team-chat channel into a hiring pipeline. A recruiter
drops a CV in `#hiring-room`. Three agents process it in order. The hiring
manager approves. Every step happens in the chat thread, and every artifact
persists in the shared room.

## The workflow

1. Recruiter posts a CV plus `@hiring-screener screen this`.
2. `@hiring-screener` scores the CV 0-100 against the JD in the room
   instructions. PASS (>= 70) calls the bias-checker. REJECT stops.
3. `@hiring-bias-checker` audits the reasoning: JD-only criteria, no protected
   traits, specific job-related reason. CLEARED calls the interviewer. FLAGGED
   stops for manager review.
4. `@hiring-interviewer` posts an interview pack (5 tailored questions, 30-min
   plan, scoring rubric) and saves it as a room document.
5. The hiring manager posts Approved or Rejected in the thread. The decision is
   saved as a room document.

## Why Switch is central

Without Switch this chain falls apart. The agents would share no JD, see no
common thread history, hand off to each other by name, or persist packs and
decisions where the team can find them. Concretely, this project uses:

- Room = Mattermost channel: one shared history, instructions, and documents.
- Room instructions hold the JD once. All three agents read from it.
- `@mention` routing moves work agent-to-agent inside the thread.
- Room documents persist interview packs and hiring decisions
  (see `!list-documents`).
- Humans and agents as equal room members. The manager approves in-thread.

## Real runs (Mattermost, Claude Code provider)

| CV | Screener | Bias audit | Outcome |
| --- | --- | --- | --- |
| Ada (strong) | 80 PASS | CLEARED | Pack saved, manager Approved |
| Ben (no code) | 5 REJECT | - (stopped) | Correct halt, no downstream work |
| Cynthia (2-yr gap) | 78 PASS | CLEARED | Pack saved with fairness note, manager Approved |

The Cynthia run is the highlight: the gap was excluded from scoring twice
(once by the screener, once by the audit), and the pack tells the interviewer
not to ask about it.

Demo video: https://youtu.be/AvHYJfYuya8 (~100 sec walkthrough).

## Repo contents

- `agents/hiring-screener.md` - Agent 1 prompt (paste into Console).
- `agents/hiring-bias-checker.md` - Agent 2 prompt.
- `agents/hiring-interviewer.md` - Agent 3 prompt.
- `agent-instructions.md` - chain index, room setup, kickoff message, JD.
- `demo-cvs/` - `ada-strong.txt`, `ben-weak.txt`, `cynthia-borderline.txt`.

## Reproduce it

Prereqs: Docker Desktop (running), Switch Console, a Claude Code account
(or Codex / OpenCode).

1. Console → Get started → run the server On this computer → Start → Continue.
2. Pick your provider for switch-buddy. Send it a first task.
3. Tell switch-buddy: create private room `hiring-room` with agents
   `hiring-screener`, `hiring-bias-checker`, `hiring-interviewer`
   (fresh folders, approvals on).
4. Console → Your Agents → open each agent → replace Agent instructions with
   the blocks in `agents/*.md` → save.
5. Console Home → Messaging apps → Mattermost Sign-in details → log in →
   open hiring-room.
6. Post the kickoff message from `agent-instructions.md`. Ask switch-buddy to
   save the JD as the room instructions.
7. Upload a CV from `demo-cvs/` with the caption
   `@hiring-screener screen this`. Watch the chain run.
8. Manager: reply Approved or Rejected in-thread. Optionally save the verdict
   as a room document.

## Template sketch

```yaml
agents:
  - name: "hiring-screener"
    addressing: anyone
  - name: "hiring-bias-checker"
    addressing: owner-agents
  - name: "hiring-interviewer"
    addressing: owner-agents
room:
  name: "hiring-room"
  agents: ["hiring-screener", "hiring-bias-checker", "hiring-interviewer"]
```
