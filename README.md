# WAD Demo — Presenter Runbook

Presenter materials for the **Docker Sandboxes ("Coding Factory") WAD demo**: run a coding agent (Claude) inside an isolated microVM, show a working app, demonstrate network policy, and — on a provisioned machine — governance and Cloud Sandboxes.

## Contents

| File | What it is |
|------|------------|
| [RUNBOOK.md](RUNBOOK.md) | Full step-by-step script — what to **Say / Type / Show** at each step |
| [CHEATSHEET.md](CHEATSHEET.md) | Commands only, top to bottom — for glancing at mid-demo |
| [MY-DEMO.pdf](MY-DEMO.pdf) | Printable version of both (runbook + cheat sheet) |

> Steps 5–7 (governance, cloud, pick-up-the-work) need the real provisioned demo machine and are labelled accordingly. Everything else runs locally.

---

## Quick Start — run the demo now

For a machine that's already set up.

1. Load the pinned sbx (every new terminal):
   ```sh
   cd /Users/ajeetraina/work/wad26/wad-demo-presenter
   . runtime/.install-state/env.sh
   ```
2. Confirm it's ready:
   ```sh
   sbx ls
   curl -s -o /dev/null -w "%{http_code}\n" http://127.0.0.1:3001/
   ```
   Expected: `wad-coding-factory` shows `running`, and `200`.
3. Open the app:
   ```sh
   open http://127.0.0.1:3001/
   ```
4. Open the coding agent (present from this terminal):
   ```sh
   ./demo agent
   ```
5. Inside the Claude prompt, run the network demo:
   ```
   ! curl https://github.com/
   ! curl https://example.org/
   ```
   GitHub responds; example.org returns a **403 policy denial** (denied by a local rule).

Full narration and the remaining sections are in [RUNBOOK.md](RUNBOOK.md).

---

## Recovery — sandbox missing or app returns `000`

If the machine is already set up (install phases show `done`), this is a repair:

```sh
cd /Users/ajeetraina/work/wad26/wad-demo-presenter
. runtime/.install-state/env.sh
./demo repair --yes
```

- Fallback if repair fails: `./demo setup --local-only`
- First-time-ever install: `sh __INSTALL_ME.sh 3` from the `wad26` folder (the `3` is the machine's sticker number)

---

## First-time setup vs repair (which command)

| Situation | Command |
|-----------|---------|
| Brand-new machine, from the ZIP package | `sh __INSTALL_ME.sh 3` (run in `wad26/`; no number = legacy) |
| Tools installed, prepare demo first time | `./demo setup` (or `--local-only`, or `--supply-chain`) |
| Already set up, VM disappeared | `./demo repair --yes` |

Check which you are with `./demo status` — phases `done` → repair; phases `pending`/error → first-time setup.
