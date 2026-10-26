# ScamShield AI — *Pause. Check. Stay Safe.*

**Sobhasaria Hackfest 2026 · Challenge H05: Scam Message & Transaction Risk Triage · Technology partner: JH-NEXIS**
Team: ______ Members: ______

An explainable, rule-based web app that analyses pasted messages and synthetic transactions, shows every risk signal with its points, and suggests safe next steps. **A risk flag is not proof of fraud.** Defensive educational prototype; synthetic data only.

## Features
Overview · Message Scanner · Transaction Risk Checker · Sample Lab (9 seeded examples, real PASS/FAIL) · Evaluation page · Useful/Not useful feedback · About/Methodology. Works offline; no API keys.

## Stack
React + TypeScript + Vite + Tailwind + lucide-react (frontend) · Python + FastAPI + Pydantic (backend) · pytest, Vitest.

## Structure
```
backend/app/{main,schemas,scoring,sample_data,feedback}.py   backend/tests/
frontend/src/{components,pages,services,types}
README.md  TEST_CASES.md  DEMO_SCRIPT.md
```

## Setup & run (needs Python 3.10+, Node 18+; internet only for installing)
Terminal 1 — backend:
```
cd backend
python -m venv .venv
.venv\Scripts\activate          # Windows   (Mac/Linux: source .venv/bin/activate)
pip install -r requirements-dev.txt
uvicorn app.main:app --reload --port 8000
```
Terminal 2 — frontend:
```
cd frontend
npm install
npm run dev
```
Open http://localhost:5173 (dev server proxies `/api` to port 8000).

**Single-server demo build:** `cd frontend && npm run build`, then run uvicorn from `backend`; open http://localhost:8000 (FastAPI serves `frontend/dist`).

## Tests
```
cd backend && pytest -v        # scoring + API tests
cd frontend && npm test        # component tests
```
Expected: all backend tests pass; Evaluation page shows 9/9. See TEST_CASES.md.

## Scoring (deterministic)
Message: urgency +25, credential *request* +35, suspicious link +25, advance-fee +50 (each once, cap 100).
Transaction: highest tier only — ≥1.5x +10, ≥3x +30, ≥10x +50 — plus new device +25.
Bands: LOW 0–24, MEDIUM 25–49, HIGH 50+. Ratio uses the unrounded value (exact decimal arithmetic).

## Synthetic data
M1–M6 and X1–X3 from the problem pack, wording unchanged.

## Privacy & safety
No external calls; links are never opened; message text isn't stored, logged or returned; feedback and history hold no message text. Feedback lives in server memory and is lost on restart. Don't enter real OTPs, passwords, card or bank details.

## Known limitations
English-only regex rules, easy to evade by rewording; legitimate messages with verify-style links may be flagged; rules were tuned against the nine examples so 9/9 is not evidence of real accuracy; no bank integration.

## Tools & AI usage
Built with AI coding assistance (Claude). Libraries: FastAPI, Pydantic, Uvicorn, React, Vite, Tailwind CSS, lucide-react, pytest, httpx, Vitest, Testing Library. The team must be able to explain every rule.

## Verification status (be honest in your submission)
Verified on the build machine: scoring module, 26/26 scoring tests, all nine examples. **Not run there** (no internet to install packages): FastAPI server, API tests, TypeScript build, Vitest, browser UI. Run the commands above and fix anything that appears before demo day.
