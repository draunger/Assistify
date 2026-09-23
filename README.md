# Assistify — AI-Powered HR Assistant

An enterprise HR assistant that answers employee questions and **takes real actions** on their behalf — applying for leave, raising support tickets — using Claude tool-calling, with role-based access control enforcing who can see and do what.

**Live demo:** https://assistify-ai-hr-enterprise-chatbot.vercel.app/

> Final-year B.Tech project, built by a team of 4.

---

## What it does

- **Conversational HR support** — employees ask HR questions in natural language and get answers grounded in the company's context.
- **Action-taking via Claude tool-calling** — the assistant doesn't just answer; it translates requests like *"apply for 2 days of leave next week"* into structured API calls that create the leave application or support ticket.
- **Role-based access control (RBAC)** — employee and HR roles see and do different things; the assistant enforces permissions on every action and data lookup.

## Tech stack

| Layer | Technology |
|-------|-----------|
| Frontend | React, Vite, TypeScript, Tailwind CSS |
| Backend | Node.js, Express |
| Database | MongoDB (MongoDB Atlas) |
| AI | Claude API (tool calling) |
| Deployment | Vercel (frontend), Render (backend) |

## Architecture (high level)

```
Employee  ─▶  React/TS client  ─▶  Express API  ─▶  Claude (tool calling)
                                        │                   │
                                        │                   └─ decides which tool to call
                                        ▼                   ▼
                                    MongoDB  ◀──  tool handlers (leave, tickets, lookups)
                                        ▲
                                   RBAC checks on every action
```

The API exposes a set of tools (leave application, ticket creation, employee-data lookup) to Claude. Claude interprets the user's request, chooses the appropriate tool, and the backend executes it — after verifying the caller's role permits the action.

## Team & my role

Built by a 4-person team split across Backend Core, HR Domain, AI/RAG, and Frontend.

**My contribution:** the AI and backend layer — Claude tool-calling integration (mapping natural-language requests to tool schemas and executing the resulting actions) and role-based access control.

> Commit history reflects individual contributions. Filter commits by author to see per-member work.

## Running locally

> Full setup notes are being expanded. High-level steps:

```bash
# Backend
cd server
npm install
# add a .env with your MongoDB URI and Claude API key (see .env.example)
npm run dev

# Frontend
cd web
npm install
npm run dev
```

Required environment variables (see `.env.example` in each folder):

- `MONGODB_URI` — MongoDB Atlas connection string
- `ANTHROPIC_API_KEY` — Claude API key
- `PORT` — backend port (default 3000)

## Status

Deployed and functional: conversational HR assistant with Claude tool-calling (leave, tickets) and role-based access control. Retrieval over uploaded policy documents (vector search) is on the roadmap.
