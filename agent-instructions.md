# Hiring Room - Index

Chain: human drops CV → `@hiring-screener` → `@hiring-bias-checker` → `@hiring-interviewer` → human approves.

Each agent has its own file. Paste the Instructions block from each file into Switch Console when you create that agent.

## Agents

- [hiring-screener](agents/hiring-screener.md) - scores CV vs JD, PASS routes forward
- [hiring-bias-checker](agents/hiring-bias-checker.md) - audits for bias, CLEARED routes forward
- [hiring-interviewer](agents/hiring-interviewer.md) - posts interview pack + Task

## Room setup

- Room name: `hiring-room`
- Bridge: your chat (Mattermost for demo, or Slack / Discord / Teams)
- Members: recruiter + hiring manager (humans) + 3 agents above
- Room Rules: paste the JD below once

## Kickoff message (post once when room is created)

```text
@hiring-screener, @hiring-bias-checker, @hiring-interviewer: this is your hiring room.

Flow: recruiter drops a CV + "@hiring-screener screen this".
Screener scores and routes PASS to bias-checker. Bias-checker audits and routes CLEARED to interviewer. Interviewer posts the pack. Hiring manager says "Approved" or "Rejected" - that is the final Decision.

Room Rules hold the Job Description. Tasks hold interview packs. Decisions hold hires/rejects.
```

## Example Job Description (paste into Room Rules)

```text
Role: Backend Intern (Lagos / Remote)
Must-haves: Python, REST APIs, git, basic SQL
Nice-to-haves: Docker, tests
Reject if: no code evidence (no GitHub, no project, no coursework repo)
```

## Demo CVs to create

1. `ada-strong.txt` - Python + API project + GitHub link → should PASS + CLEAR
2. `ben-weak.txt` - no code, sales background → should REJECT at screener
3. `cynthia-borderline.txt` - good skills but 2-year gap → should PASS then get FLAGGED or discussed

## Template sketch (for README later)

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
