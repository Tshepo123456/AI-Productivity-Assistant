README.md
<div align="center">
# Nova — AI Workplace Assistant
**An AI-powered assistant that automates everyday workplace tasks — email drafting, meeting summarization, task planning, research, and conversational support.**
[![Live Demo](https://img.shields.io/badge/Live%20Demo-kindred--intelligence-4f46e5?style=for-the-badge)](https://kindred-intelligence.lovable.app)
[![Built with Lovable](https://img.shields.io/badge/Built%20with-Lovable-000?style=for-the-badge)](https://lovable.dev)
[![License: MIT](https://img.shields.io/badge/License-MIT-22c55e?style=for-the-badge)](#license)
</div>
---
## ✨ Overview
**Nova** is a stylish, professional AI workplace copilot built to streamline knowledge-worker tasks. It combines strong prompt engineering with a clean, multi-thread chat experience backed by a real database — so every conversation is persisted, retrievable, and secure.
> Designed with a **Midnight Indigo** aesthetic — deep navy surfaces with electric indigo accents for a focused, modern feel.
---
## 🚀 Key Features
| Mode | What it does |
|------|--------------|
| 💬 **General Assistant** | Concise, structured answers to any workplace question |
| ✉️ **Email Generator** | Polished workplace emails with subject, body, and sign-off — tone-controlled |
| 📝 **Meeting Summarizer** | TL;DR, decisions, action items (with owners/dates), open questions, next steps |
| ✅ **Task Planner** | Objectives → milestones → prioritized tasks (P0/P1/P2) with weekly schedule |
| 🔎 **Research Assistant** | Structured briefings with key findings, sources to verify, and recommendations |
**Plus:**
- 🧵 **Multiple conversation threads** — organize work by project or topic
- 💾 **Persistent history** — every message stored securely in Lovable Cloud
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
```
src/
├── routes/
│   ├── __root.tsx                  # Root layout
│   ├── index.tsx                   # Landing page
│   ├── login.tsx                   # Auth (email + Google)
│   ├── _authenticated.tsx          # Protected layout
│   ├── _authenticated/
│   │   ├── app.tsx                 # New conversation
│   │   └── c.$threadId.tsx         # Thread view
│   └── api/chat.ts                 # Streaming chat endpoint
├── lib/
│   ├── ai-gateway.ts               # Prompt library + provider
│   └── threads.functions.ts        # Server functions (CRUD)
├── components/
│   ├── ai-elements/                # Conversation, message, prompt-input
│   └── ui/                         # shadcn primitives
└── integrations/supabase/          # Auth + DB clients
```
---
## 🔧 Getting Started
### Prerequisites
- [Bun](https://bun.sh) (or Node 20+)
- A Lovable Cloud project (auto-provisioned in Lovable)
### Local development
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
---
## 📄 License
Released under the [MIT License](LICENSE).
---
<div align="center">
Built with ❤️ using **[Lovable](https://lovable.dev)** · Powered by **Lovable Cloud** + **Lovable AI**
</div>
