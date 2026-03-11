# TheGreekClawd — One Man...7 brains..

*Built by [@FotiosM](https://x.com/FotiosM) · Art at [fotifoti.art](https://www.instagram.com/fotifoti.art/)*

---

I'm a Greek-American developer building four businesses simultaneously as a 7 brain operation out of Massachusetts. I have a bloodless team and we all share the same obsessive drive to build.

This repo documents **TheGreekClawd (TGC)** — my first Digital Employee, built on the [OpenClaw](https://openclaw.ai) framework. It is not a demo. It is not a side project. It is operational infrastructure that I am building to depend on.

---

## What I'm Building — The Four Workstreams

TGC serves as the autonomous backbone across four active businesses:

| Workstream | What It Is |
|------------|------------|
| **Poor People App (PPA)** | A skills marketplace on the Nostr protocol connecting working-class people to opportunities. Includes an open-source intelligence layer scraping USAspending.gov, federal grants, and nonprofit funding. |
| **FotiFoti** | Automated AI art platform posting colorized artwork autonomously to Instagram and Facebook via AWS EventBridge + Lambda. Gallery outreach and licensing expansion in progress. |
| **Hard-E** | AI sales director system being rebuilt in React + FastAPI for real-time voice interaction. Originally deployed with Patriot Contracting. OpenClaw integration planned. |
| **Personal Services** | Marketing my skills as a developer — web apps, autonomous agents, video editing. TGC handles research and outreach. |

---

## The Infrastructure

TGC runs on AWS Lightsail (Ubuntu, 2GB RAM) and communicates exclusively via Telegram. Everything flows through Telegram — commands, triggers, intelligence reports, video clips. All of it.

**Stack:**
- OpenClaw v2026.2.26 as the agent framework
- Claude Sonnet as the primary model
- AWS Lightsail `3.12.55.229` — the server never sleeps
- Tailscale mesh network connecting server to my laptop
- GitHub for daily workspace backup (3am cron, every night)
- Brave Search API for live intelligence
- yt-dlp + ffmpeg + openai-whisper for media processing

---

## The Podcast Intelligence Pipeline

This is the piece I'm most proud of.

TGC ingests podcast transcripts — All-In, This Week in Startups, Matt Wolfe, Matthew Berman, David Ondrej — and processes every transcript through **8 intelligence lenses**:

1. **TGC Self-Improvement** — agent patterns, architecture ideas, cost techniques
2. **Investment Intelligence** — companies, catalysts, trade signals (structured, queryable)
3. **Industry Trajectory** — directional trends with timeframes and evidence chains
4. **Network Map** — people, roles, investments, relationships
5. **Revenue Application** — specific actionable opportunities for my four workstreams
6. **Build Relevance** — findings tagged to active projects (TGC, Hard-E, FotiFoti, PPA)
7. **Synthesis & Prediction** — cross-transcript patterns, predictions with confidence scores and review dates
8. **Model Benchmarks** — LLM releases, pricing shifts, capability comparisons that might affect TGC's own architecture

Every transcript produces:
- Structured JSON into a persistent intelligence tracker
- A narrative summary saved to `data/transcript-summaries/`
- Actions appended to `data/actions.json`

The pipeline runs on a 05:00 UTC daily cron, or on-demand via Telegram trigger.

---

## The Video Intelligence Pipeline

When I send a YouTube URL to TGC via Telegram, here's what happens:

1. TGC fetches metadata, responds: *"Run full pipeline + 3 clips? YES/SKIP"*
2. yt-dlp pulls the transcript via YouTube's caption CDN
3. 8-lens intelligence analysis runs on the transcript
4. TGC selects 3 high-value clip moments based on active workstreams and open action items
5. yt-dlp downloads the full video through a residential IP proxy (bypasses AWS datacenter blocks)
6. ffmpeg cuts and compresses 3 clips locally
7. Telegram delivers the summary + all 3 clips as video files

**The residential proxy:** YouTube blocks video stream requests from AWS datacenter IPs. The fix is an SSH SOCKS5 tunnel via Tailscale — the server routes yt-dlp traffic through my laptop's Comcast residential IP. autossh keeps the tunnel alive. If the laptop is offline, TGC sends deep-link timestamps as fallback instead of clips.

**The ffmpeg insight** that made this work — downloading the full video first, then cutting locally instead of using `--download-sections` through the SOCKS proxy — came directly from processing a TWIST transcript. The show informed the build.

---

## Cost Engineering

The first full pipeline run cost **$8.63** for one 40-minute video. Unacceptable.

Root cause breakdown:

| Waste Source | Cost | Fix |
|---|---|---|
| Cold starts × 4 | $2.37 | Daily session pruning at 03:30 UTC |
| Transcript injection × 7 | $3.95 | Hard rule: `grep` only, never `cat` the transcript |
| Polling × 19 while waiting for YES/SKIP | $0.99 | No-polling rule — zero AI turns during wait |
| Actual useful work | $1.31 | — |

After optimization: **~$1.00–1.50 per run**. The target is browser-equivalent economics for autonomous operation.

---

## What I've Learned the Hard Way

**The Tailscale Incident.** A previous session set a global exit node on the server with `sudo tailscale set --exit-node=`. This routed ALL server traffic through my laptop, breaking SSH for hours. Recovery required connecting via the Tailscale IP directly and clearing the exit node. The lesson: the `--proxy` flag on yt-dlp is surgical. Global routing changes are catastrophic. Never conflate the two.

**Cursor Agent is a collaborator, not an executor.** When I write prompts that tell Cursor *how* to solve something instead of *what* to solve, I get bad results. The right move is to give Cursor the goal, the constraints, and the failure modes — then let it look at the actual code and propose the approach before touching anything.

**TGC must not self-modify its own scripts.** During a test run, TGC corrupted its own `send_telegram_text` function trying to fix a bug autonomously. The rule now: TGC reports bugs to the operator. It does not patch itself.

---

## What's Next

- **PPA / Claude Code integration** — the next major build phase
- **Nostr skills** (`nostr-social`, `dagny-nostr-nak`) for PPA's protocol layer
- **Gmail / outreach integration** — TGC handling cold outreach autonomously after human approval
- **Hard-E voice pipeline** — React + FastAPI rebuild with OpenClaw integration
- **22-prompt backlog** — features designed but not yet built

---

## The Honest Part

I'm building this with maximum obsession. 

If you're building on OpenClaw, working on autonomous agent systems, or just curious - let's talk shop.

**[@FotiosM on X](https://x.com/FotiosM)**
**[fotifoti.art on Instagram](https://www.instagram.com/fotifoti.art/)**

---

*TheGreekClawd is operational. The lobster never sleeps.*
