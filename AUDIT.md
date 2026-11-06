# Repo Audit - switch-hiring-room

Date: Nov 5, 2026. Purpose: pre-submission review against the hackathon
judging criteria.

## Verdict

Ready to submit after minor doc touch-ups. Nothing found blocks judging.

## Judging criteria check

1. Use of Switch - PASS. README explains why the chain fails without Switch.
   Video shows @mention routing, shared thread history, and room documents.
2. Technical execution - PASS with note. 8 reproduce steps, exact agent
   prompts in `agents/`, demo CVs included. Note: one filename drift, see
   issue 1.
3. Creativity and impact - PASS. Hiring chain with a bias audit stage. The
   Cynthia run proves the fairness claim with a real note in the pack.
4. Presentation - PASS. Video link verified live (title "Switch Demo",
   HTTP 200). README covers workflow, runs, files, and setup.

## File inventory (10 files)

| File | Purpose | Status |
| --- | --- | --- |
| README.md | Submission front page | OK, video linked |
| agent-instructions.md | Chain index, kickoff, JD | OK, see issue 1 |
| agents/hiring-screener.md | Agent 1 prompt | OK, matches Console |
| agents/hiring-bias-checker.md | Agent 2 prompt | OK, matches Console |
| agents/hiring-interviewer.md | Agent 3 prompt | OK, matches Console |
| demo-cvs/ada-strong.txt | Strong CV, PASS path | OK |
| demo-cvs/ben-weak.txt | Weak CV, REJECT path | OK |
| demo-cvs/cynthia-borderline.txt | Gap CV, fairness path | OK |
| demo-script.rtf | Video narration script | OK, see issue 4 |
| progress.md | Build log | OK, see issue 2 |

## Checks run

- Secrets scan (key, secret, password, token patterns): clean, no hits.
- Dash style: no em-dashes or en-dashes anywhere (verified by search).
- Attribution: no AI credit lines anywhere (verified by search).
- Video link: resolves to youtube.com/watch?v=AvHYJfYuya8, 200 OK.
- Prompt consistency: repo prompt files match the pasted Console prompts
  except dash characters, which change no behavior.

## Issues

1. Minor: `agent-instructions.md` lists demo CVs as `.pdf` names, but the
   files on disk are `demo-cvs/*.txt`. README already uses the correct names.
2. Minor: `progress.md` file list is stale. It omits README.md, demo-cvs/,
   demo-script.rtf, and this audit. Internal log only.
3. Advisory: no `.gitignore` in the repo. Nothing secret is present, so it is
   safe to push as-is.
4. Advisory: the demo script is RTF, not .docx. Word opens it directly.

## Pre-submit actions

1. Fix the `.pdf` names to `.txt` in `agent-instructions.md` (1 minute).
2. Push to GitHub. Confirm the README renders and the video link is clickable.
3. Submit repo plus video before Nov 7, 11:59 PM IST.
