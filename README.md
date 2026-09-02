# MSK Content Pipeline

**Headless vlog ingestion → auto content package.** A proof-of-concept that ingests a YouTube vlog transcript (no scrapers, no manual downloads) and auto-generates a creator-ready package: timestamped chapters, a YouTube description, Shorts/Reels hooks, and hashtags.

Built in ~30 minutes as a live demo for a Mumbai lifestyle vlogger — to prove the entire "watch → package" loop can run automatically on every upload.

## What it produces

Given one vlog, the pipeline outputs:

1. **Chapters** — 5 timestamped chapters aligned to the story arc
2. **Description** — one energetic ~80-word YouTube description
3. **Hooks** — 3 curiosity-driven Shorts/Reels hooks
4. **Hashtags** — 5 relevant tags

Real output generated from a live vlog: [`MSK_DEMO.md`](./MSK_DEMO.md)

## Architecture

```
YouTube auto-captions (hi/en)
        │  youtube-transcript-api — headless, no scrapers
        ▼
Timestamped transcript
        │  content-strategist prompt
        ▼
Groq (Llama) fast inference
        ▼
Chapters + Description + Hooks + Hashtags → MSK_DEMO.md
```

## Run it

```bash
python3 -m venv venv && source venv/bin/activate
pip install -r requirements.txt
export GROQ_API_KEY=your_key   # free at console.groq.com
# set VID in demo.py to any YouTube video ID
python demo.py
```

## Stack

- Python
- youtube-transcript-api (headless ingestion)
- Groq SDK (low-latency LLM inference)
- Prompt engineering for content packaging

## Roadmap (next iteration)

- Webhook trigger on every new upload (fully automatic)
- Auto-captioned Shorts clipping from peak moments
- Comment/DM triage routing brand deals to one inbox

— [Parth Keskar](https://github.com/parthkeskar05-byte) · AI/ML Engineer, Mumbai
