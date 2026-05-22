
README.md
# Nova — AI Workplace Assistant
**An AI-powered assistant that automates everyday workplace tasks — email drafting, meeting summarization, task planning, research, and conversational support.**
**An AI-powered workplace copilot that automates everyday knowledge work: drafting emails, summarizing meetings, planning tasks, and conducting research.**
[![Live Demo](https://img.shields.io/badge/Live%20Demo-kindred--intelligence-4f46e5?style=for-the-badge)](https://kindred-intelligence.lovable.app)
[![Built with Lovable](https://img.shields.io/badge/Built%20with-Lovable-000?style=for-the-badge)](https://lovable.dev)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge)](#license)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge)](#-license)
</div>
---
## ✨ Overview
**Nova** is a stylish, professional AI workplace copilot built to streamline knowledge-worker tasks. It combines strong prompt engineering with a clean, multi-thread chat experience backed by a real database — so every conversation is persisted, retrievable, and secure.
> Designed with a **Midnight Indigo** aesthetic — deep navy surfaces with electric indigo accents for a focused, modern feel.
---
## 🚀 Key Features
| Mode | What it does |
|------|--------------|
## 📑 Submission Index
1. [AI Solution / Prototype](#1-ai-solution--prototype)
2. [Documentation](#2-documentation-12-pages)
   - [Problem Statement](#problem-statement)
   - [Solution Overview](#solution-overview)
   - [Tools Used](#tools-used)
   - [Sample Prompts](#sample-prompts)
   - [Challenges and Solutions](#challenges-and-solutions)
3. [Presentation](#3-presentation)
   - [Features and Impact](#features-and-impact)
   - [Live Demo](#live-demo)
---
## 1. AI Solution / Prototype
**Nova** is a fully working web-based prototype — a multi-mode AI assistant with persistent, authenticated conversations.
🔗 **Live prototype:** [kindred-intelligence.lovable.app](https://kindred-intelligence.lovable.app)
### What the prototype demonstrates
| Capability | Demonstrated by |
|---|---|
| Conversational interface | Streaming chat UI with multi-thread history |
| Specialized AI workflows | 5 task-specific modes with tailored prompts |
| Persistent state | Postgres-backed thread + message storage |
| Secure multi-user access | Email + Google OAuth, Row Level Security |
| Production deployment | Edge-deployed on Cloudflare Workers |
---
## 2. Documentation (1–2 Pages)
### Problem Statement
Knowledge workers lose **hours every day** to repetitive writing and synthesis tasks — composing emails, summarizing meetings, breaking down projects into tasks, and gathering background research. Generic chatbots help, but they:
- Force users to **re-prompt the same instructions** for every task
- Produce **unstructured output** that needs reformatting
- **Lose conversation history** between sessions
- Offer **no role-based specialization** for workplace contexts
There is a need for a focused, secure assistant that knows *how* to handle each workplace task without the user having to engineer the prompt every time.
### Solution Overview
**Nova** is an AI workplace assistant that wraps a state-of-the-art LLM (Google Gemini 3 Flash, via the Lovable AI Gateway) with **five purpose-built modes**, each driven by a carefully engineered system prompt:
| Mode | Output |
|---|---|
| 💬 **General Assistant** | Concise, structured answers to any workplace question |
| ✉️ **Email Generator** | Polished workplace emails with subject, body, and sign-off — tone-controlled |
| 📝 **Meeting Summarizer** | TL;DR, decisions, action items (with owners/dates), open questions, next steps |
| ✅ **Task Planner** | Objectives → milestones → prioritized tasks (P0/P1/P2) with weekly schedule |
| 🔎 **Research Assistant** | Structured briefings with key findings, sources to verify, and recommendations |
**Plus:**
| ✉️ **Email Generator** | Subject + greeting + body + sign-off, tone-controlled |
| 📝 **Meeting Summarizer** | TL;DR → Decisions → Action Items (table) → Open Questions → Next Steps |
| ✅ **Task Planner** | Objective → Milestones → Prioritized tasks (P0/P1/P2) → Weekly schedule |
| 🔎 **Research Assistant** | Summary → Key findings → Sources to verify → Recommendations |
Every conversation is persisted per-user in a Postgres database protected by Row Level Security, so users can return to prior threads at any time.
### Tools Used
| Layer | Tool |
|---|---|
| Frontend framework | **TanStack Start v1** (React 19, SSR, file-based routing) |
| Build tooling | **Vite 7** + **Bun** |
| UI / styling | **Tailwind CSS v4**, **shadcn/ui**, semantic OKLCH tokens |
| AI model | **Google Gemini 3 Flash Preview** via the **Lovable AI Gateway** |
| Streaming SDK | **Vercel AI SDK** (`ai`, `@ai-sdk/openai-compatible`) |
| Backend / DB / Auth | **Lovable Cloud** (Postgres + Auth + RLS) |
| Deployment | **Cloudflare Workers** (Edge) |
| Build / dev platform | **[Lovable](https://lovable.dev)** |
### Sample Prompts
System prompts live in [`src/lib/ai-gateway.ts`](src/lib/ai-gateway.ts). Examples of **user prompts** that showcase each mode:
**✉️ Email Generator**
> *"Write a friendly but firm email to a vendor whose invoice is 3 weeks overdue. Ask for payment by Friday and propose a 15-min call if there's an issue."*
**📝 Meeting Summarizer**
> *"Here are my notes from today's product sync: [paste notes]. Summarize and pull out action items with owners."*
**✅ Task Planner**
> *"I have to launch a customer feedback survey in 2 weeks. Break it into milestones and a weekly plan."*
**🔎 Research Assistant**
> *"Give me a briefing on the current state of EU AI Act compliance requirements for SaaS startups."*
**💬 General Assistant**
> *"What's the best way to give critical feedback to a peer without damaging the relationship?"*
### Challenges and Solutions
| Challenge | Solution |
|---|---|
| **Inconsistent output formatting** across tasks | Built a **mode-based prompt library** that enforces a structured markdown schema per task (tables, headings, sections). |
| **Streaming UX** without page reloads or jank | Adopted the **Vercel AI SDK** for token-by-token streaming with a sticky-to-bottom chat container. |
| **Multi-user data isolation** | All `threads` and `messages` tables enforce **Row Level Security** so users can only read/write their own data. |
| **Auth-protected server functions failing in SSR prerender** | Moved protected calls from route loaders into components via `useServerFn` + `useQuery`, and gated loader-based fetches behind the `_authenticated` layout. |
| **Cost / abuse exposure on the chat endpoint** | Added **thread-ownership validation** and a **100-message-per-request cap** in `src/routes/api/chat.ts` before any model call. |
| **Hallucinated citations in research mode** | Prompt explicitly instructs the model to **flag uncertainty** and **never fabricate sources** — only list things to verify. |
| **No vendor lock-in for AI** | Used the **Lovable AI Gateway** (OpenAI-compatible API) so the underlying model can be swapped without code changes. |
---
## 3. Presentation
### Features and Impact
**🎯 Core Features**
- 🧵 **Multiple conversation threads** — organize work by project or topic
- 💾 **Persistent history** — every message stored securely in Lovable Cloud
- 💾 **Persistent history** — every message stored securely, retrievable anytime
- 🔐 **Email + Google authentication** with Row Level Security
- ⚡ **Streaming responses** powered by the Lovable AI Gateway (Gemini 3 Flash)
- 🎨 **Midnight Indigo design system** — semantic tokens, dark-mode native
---
## 🧠 Prompt Engineering
Each mode uses a carefully crafted **system prompt** that defines role, output structure, and tone. For example, the Meeting Summarizer enforces a 5-section markdown format (TL;DR → Decisions → Action Items table → Open Questions → Next Steps), while the Email Generator requires a subject line and matched tone. See [`src/lib/ai-gateway.ts`](src/lib/ai-gateway.ts) for the full prompt library.
---
## 🛠️ Tech Stack
- **Framework:** TanStack Start v1 (React 19, SSR, file-based routing)
- **Build:** Vite 7
- **Styling:** Tailwind CSS v4 + shadcn/ui + semantic design tokens (OKLCH)
- **Backend:** Lovable Cloud (Postgres + Auth + RLS)
- **AI:** Lovable AI Gateway — `google/gemini-3-flash-preview`
- **Streaming:** Vercel AI SDK (`ai`, `@ai-sdk/openai-compatible`)
- **Deployment:** Cloudflare Workers (Edge)
---
## 🏗️ Architecture
- ⚡ **Streaming responses** — instant feedback, no waiting for full completion
- 🎨 **Midnight Indigo design system** — focused, professional, dark-mode native
- 🛡️ **Responsible AI guardrails** — no fabricated sources, transparent prompts, authenticated by default
**📈 Impact**
| Metric | Before Nova | With Nova |
|---|---|---|
| Time to draft a professional email | 5–10 min | < 30 sec |
| Time to summarize a 1-hour meeting | 15–20 min | < 1 min |
| Time to scope a new project | 30+ min | < 5 min |
| Prompt engineering required from user | High (every task) | None (mode picker) |
**🏗️ Architecture**
```
src/
│   │   └── c.$threadId.tsx         # Thread view
│   └── api/chat.ts                 # Streaming chat endpoint
├── lib/
│   ├── ai-gateway.ts               # Prompt library + provider
│   ├── ai-gateway.ts               # Prompt library + AI provider
│   └── threads.functions.ts        # Server functions (CRUD)
├── components/
│   ├── ai-elements/                # Conversation, message, prompt-input
└── integrations/supabase/          # Auth + DB clients
```
---
## 🔧 Getting Started
### Prerequisites
- [Bun](https://bun.sh) (or Node 20+)
- A Lovable Cloud project (auto-provisioned in Lovable)
### Local development
### Live Demo
🔗 **[kindred-intelligence.lovable.app](https://kindred-intelligence.lovable.app)**
**Demo flow (suggested for slides / walkthrough):**
1. **Sign in** with Google or email → land on the new-conversation screen
2. **Pick a mode** (e.g. Email Generator) → enter a real workplace prompt
3. **Watch streaming output** render in structured markdown
4. **Switch modes** mid-session to show specialization (e.g. Meeting Summarizer)
5. **Open the sidebar** → revisit a prior thread to demonstrate persistence
6. **Sign out / sign in as a different user** → show data isolation via RLS
---
## 🔧 Getting Started (for reviewers)
```bash
# Install dependencies
bun install
# Start the dev server
bun run dev
```
The app will be available at `http://localhost:5173`.
### Environment variables
Automatically managed by Lovable Cloud:
```
VITE_SUPABASE_URL=
VITE_SUPABASE_PUBLISHABLE_KEY=
VITE_SUPABASE_PROJECT_ID=
LOVABLE_API_KEY=           # server-only, for AI Gateway
```
---
## 🛡️ Responsible & Ethical AI
Nova is built with safety, privacy, and accountability in mind:
- **No fabricated sources** — the Research mode is instructed to flag uncertainty and never invent citations.
- **User-scoped data** — Row Level Security ensures users only ever read or write their own conversations.
- **Authenticated by default** — every chat call requires a verified Supabase JWT.
- **Transparent prompts** — all system prompts are open and auditable in [`src/lib/ai-gateway.ts`](src/lib/ai-gateway.ts).
- **No anonymous sign-ins** — standard email + Google OAuth flows only.
---
## 🌐 Live Demo
🔗 **[kindred-intelligence.lovable.app](https://kindred-intelligence.lovable.app)**
---
## 📦 Deployment
This project is published via **Lovable**. To deploy your own copy:
1. Open the project in [Lovable](https://lovable.dev)
2. Click **Publish** in the top right
3. (Optional) Connect a custom domain under **Project → Settings → Domains**
---
## 🤝 Contributing
Issues and pull requests are welcome. For substantial changes, please open an issue first to discuss what you'd like to change.
The app runs at `http://localhost:5173`. Environment variables (`VITE_SUPABASE_URL`, `VITE_SUPABASE_PUBLISHABLE_KEY`, `LOVABLE_API_KEY`) are auto-managed by Lovable Cloud.
---
