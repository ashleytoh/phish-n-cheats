# Phish n Cheats

Phish n Cheats is an e-commerce fraud and marketplace trust & safety simulation. It looks like a normal second-hand marketplace, but five scam listings are planted among genuine decoys. Players browse, chat with suspicious sellers, decide whether to report or proceed, and receive a scored breakdown of what they spotted or missed.

The project is designed as a playable scam-awareness experience and a lightweight trust-team research instrument: it teaches users how common marketplace scams feel in-context, while also showing which scam patterns and red flags users are most likely to miss.

## Product concept

Most anti-scam education is delivered as static advice: “do not pay outside the platform”, “watch out for pressure tactics”, “verify authenticity”. Phish n Cheats turns that advice into an interactive marketplace drill.

Players enter a fictional Carousell-style marketplace called **Carouza**, where real-looking listings are mixed with planted scam scenarios. When a player opens a planted listing, they chat with an AI-powered scammer following a specific fraud playbook. At the end of the conversation, the player either reports the listing or proceeds with the deal. The app then grades the decision and explains the missed or detected red flags.

## Core experience

1. **Browse like a normal marketplace user**  
   Search, filter, and open product listings across categories such as electronics, gaming, luxury, fashion, home, sports, and hobbies.

2. **Find the planted scams**  
   Five hidden scam listings are mixed into a larger set of genuine decoy listings.

3. **Chat with the seller**  
   Planted scams trigger a simulated chat where the scammer uses believable marketplace tactics such as urgency, off-platform nudges, deposits, fake buyer protection, or authenticity deflection.

4. **Report or proceed**  
   The player chooses whether to report the listing or continue with the deal.

5. **Receive feedback**  
   The app generates a verdict, red-flag trace, score breakdown, safety tips, and an overall scam-resistance level.

6. **View trust & safety analytics**  
   The dashboard aggregates play records to show which scam archetypes fool the most users, which red flags are most often missed, and whether players improve over the event.

## Scam archetypes

The five planted scams are:

| Archetype | What it tests |
|---|---|
| Off-platform migration | Whether the player resists moving to WhatsApp, Telegram, or another channel where platform protections are weaker. |
| Urgency / flash sale | Whether the player catches pressure tactics around scarcity, time limits, and “pay now to lock it in”. |
| Deposit before meetup | Whether the player refuses to send money before inspecting the item or meeting safely. |
| Phishing payment link | Whether the player avoids fake “secure checkout” or “buyer protection” links outside the marketplace. |
| Counterfeit item | Whether the player asks for authentication proof instead of trusting a too-good-to-be-true branded item. |

## Key features

- **Realistic marketplace UI** with product cards, listing detail pages, categories, search, seller metadata, buyer-protection cues, likes, prices, and product photos.
- **Planted scam listings plus decoys** so the hunt feels closer to a real marketplace feed instead of an obvious quiz.
- **LLM-powered scammer chats** that adapt to the player’s messages while staying within the selected scam playbook.
- **Fallback scam lines** so the app remains playable even when no OpenAI API key is configured.
- **Suggested replies** that let players probe red flags or take risky actions, while still supporting free-text chat.
- **Conversation judging** that decides whether the player was scammed or avoided the scam based on the transcript and final action.
- **Trace feedback** showing what the player did, what they should have done, missed red flags, tips, and a score breakdown.
- **Event-level report** with scams found, defended cases, failed cases, red flags spotted, total score, and scam-resistance level.
- **Trust & Safety dashboard** that turns individual playthroughs into aggregate fraud intelligence.

## Screenshots

These screenshots show the main playable flow, from marketplace browsing through the scam chat, feedback screens, player report, and Trust & Safety dashboard.

### 1. Marketplace feed

<img src="docs/pitch/assets/product/feed.png" alt="Marketplace feed with planted scam listings" width="100%" />

### 2. Listing detail

<img src="docs/pitch/assets/product/listing.png" alt="Suspicious marketplace listing detail screen" width="100%" />

### 3. Seller chat

<img src="docs/pitch/assets/product/chat.png" alt="In-app chat with a suspicious marketplace seller" width="100%" />

### 4. Scam feedback

<img src="docs/pitch/assets/product/freeze.png" alt="Scam intervention feedback modal" width="100%" />

### 5. Player report

<img src="docs/pitch/assets/product/report.png" alt="Player report showing scam-resistance score and outcomes" width="100%" />

### 6. Trust & Safety dashboard

<img src="docs/pitch/assets/product/dashboard.png" alt="Trust and Safety dashboard summarising scam intelligence" width="100%" />

## Tech stack

### Frontend

- React 18
- TypeScript
- Vite
- React Router
- Zustand with session storage persistence
- Tailwind CSS
- Framer Motion
- Lucide React icons

### Backend

- Express API server
- OpenAI-compatible LLM provider
- Local fallback behavior when AI is unavailable
- Shared API contracts between client and server

### Testing and tooling

- Vitest
- Testing Library
- ESLint
- Prettier
- Concurrent local frontend/backend dev server

## Project structure

```text
.
├── api/                    # Vercel serverless entry point
├── public/listings/         # Product/listing images
├── server/                  # Express API, LLM provider, prompts, handlers
│   ├── app.ts               # API routes
│   ├── handlers.ts          # Chat, judge, and trace handlers
│   ├── prompts.ts           # Scam playbooks and grading prompts
│   └── llm/                 # LLM provider abstraction
├── src/
│   ├── app/                 # App shell, routing, theme, header
│   ├── components/          # Shared UI components
│   ├── data/                # Listings, red flags, suggestions, seed play records
│   ├── features/
│   │   ├── intro/           # Event intro and opt-in flow
│   │   ├── marketplace/     # Feed, search, categories, listing details
│   │   ├── chat/            # Simulated seller chat experience
│   │   ├── grading/         # Per-scam trace feedback
│   │   ├── report/          # Player result report
│   │   └── dashboard/       # Trust & safety analytics dashboard
│   └── lib/                 # Types, API client, scoring, aggregation, store
├── index.html
├── package.json
└── vite.config.ts
```

## Run locally

### Prerequisites

- Node.js 18+
- npm
- Optional: an OpenAI API key for live AI seller replies and richer grading

### Setup

```bash
npm install
cp .env.example .env
```

Edit `.env` if you want live AI behavior:

```bash
OPENAI_API_KEY=sk-your-key-here
OPENAI_MODEL=gpt-4o-mini
AI_PROVIDER=openai
PORT=8787
```

If `OPENAI_API_KEY` is not set, the app still runs with canned fallback seller lines.

### Start the app

```bash
npm run dev
```

This starts:

- Vite frontend on `http://localhost:5173`
- Express API server on `http://localhost:8787`
- Vite proxying `/api/*` requests to the local API server

## Available scripts

| Script | Description |
|---|---|
| `npm run dev` | Run the Vite frontend and Express API server together. |
| `npm run build` | Type-check and build the production frontend. |
| `npm run preview` | Preview the built Vite app. |
| `npm run server` | Run the Express server directly. |
| `npm run test` | Run Vitest tests. |
| `npm run test:watch` | Run Vitest in watch mode. |
| `npm run lint` | Run ESLint. |
| `npm run format` | Format the project with Prettier. |

## API routes

| Route | Purpose |
|---|---|
| `GET /api/health` | Reports whether AI is configured and which model is selected. |
| `POST /api/chat` | Generates the next scammer chat reply for a selected archetype. |
| `POST /api/judge` | Judges the full transcript and final action as avoided or scammed. |
| `POST /api/trace` | Produces warm, instructive feedback lines for the player’s trace screen. |

## Scoring model

Each resolved challenge receives a score out of 100 across three dimensions:

- **Detection**: Did the player identify or resist the scam?
- **Caution**: Did the player avoid unsafe actions and risky engagement?
- **Speed**: How quickly did the player resolve the scam?

The event score is the average across attempted challenges and maps to a scam-resistance level: `Rookie`, `Aware`, `Sharp`, or `Guardian`.

## Safety note

This project is for scam-awareness education, product prototyping, and trust & safety analysis. The scam conversations are simulated and should not include real payment links, credential collection, or live fraud infrastructure.
