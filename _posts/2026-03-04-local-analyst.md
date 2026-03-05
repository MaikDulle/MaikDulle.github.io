---
layout: post
title: "I Built a Local AI Analyst So My Colleagues Don't Have to Email Me Anymore"
subtitle: "How I turned 'can you quickly look at this CSV?' into a one-click self-service tool — fully offline, surprisingly powerful, and shamelessly over-engineered."
author: Dr. Maik Dulle
date: 2026-03-04
background: '/img/posts/ai_local_agent/header_ai_agent.png'
---

## Note: I am not a professional developer. Use at your own risk and be ethical about data usage.

Picture this: your Head of Marketing has a CSV. She wants to know which customer segment drives the most revenue. She is not a data scientist. Your calendar is already blocked. And the answer she needs is sitting right there in her file, completely inaccessible to her.

This is the gap I wanted to close. Not by hiring more analysts, not by buying another BI subscription — but by giving non-technical people a tool that **translates raw data into actual insights**, locally, privately, without a single line of code on their end. The bottleneck in most organizations isn't data. It's the distance between data and the person who needs to act on it.

Local Analyst is built for the manager who got handed a spreadsheet, the marketing practitioner running a campaign, the strategy consultant trying to make sense of a client's export — anyone who needs *insight, not infrastructure*.

<br>

## The Idea: Analytics as a Vending Machine

The core concept was almost embarrassingly simple: make statistical analysis as frictionless as possible for people who aren't data scientists. No Python installs for the end-user, no API keys, no "just connect your BigQuery account real quick." You drop a file in, you get analysis out.

But here's where it gets interesting — I didn't want to build yet another "pretty charts" tool. Real analysts need real stats. So Local Analyst covers the full spectrum: **RFM segmentation, A/B significance testing, cohort analysis, multi-touch attribution, funnel drop-off, anomaly detection** — all from a single upload across 12 analysis modules. The Full Scan runs all of them at once and returns a prioritized list of findings with severity ratings.

![Analysis window](/img/posts/ai_local_agent/preview5.webp)
*12 analysis modules — one click each. Results appear immediately below the button, no configuration needed.*

You upload. You click Analyze. You read the result. That's the whole product.

<br>

After uploading, the tool auto-detects which column is your date, revenue, customer ID and so on. You can correct it in two clicks if it guesses wrong — this is what unlocks the more specific analysis modules.

![Upload screen](/img/posts/ai_local_agent/preview1.webp)
*Drag and drop any file format — CSV, Excel, JSON, PDF, PowerPoint, Word. The tool reads it and shows a preview immediately.*

![Column mapping](/img/posts/ai_local_agent/preview2.webp)
*Auto-detected column mapping. Correct in two clicks if needed.*

<br>

There is also a filter panel and direct CSV/Excel export — so if someone just needs to slice a dataset and hand it off, they can do that without opening Python or bothering their analyst. One bonus use case that turned out to be surprisingly popular: upload a business PowerPoint full of messy tables and embedded charts, get a clean, standardized Excel back. No copy-pasting required.

![Filter and export](/img/posts/ai_local_agent/preview3.webp)
*Row filters + CSV/Excel export. Upload a messy PPTX, download a structured spreadsheet.*

---

<br>

## The Architecture (A.K.A. The Part I Over-Engineered)

I structured the project as a set of clearly separated engines. That separation paid off massively when debugging — when something broke in the PDF extractor, I didn't have to dig through visualization logic to fix it.

The four main components:

<ul>
  <li><code>data_upload_engine/</code> — handles everything from clean CSVs to messy PowerPoints with embedded chart images (yes, with OCR)</li>
  <li><code>analysis_engine/</code> — all the statistical heavy lifting: RFM, cohorts, A/B tests, attribution, anomaly detection</li>
  <li><code>viz_engine/</code> — Plotly charts, heatmaps, time series</li>
  <li><code>ai/</code> — an <em>optional</em> local language model layer that runs 100% on your CPU, no internet, no API key</li>
</ul>

``` python
Local_analyst/
├── app/                  # Streamlit UI + tab routing
├── analysis_engine/      # All statistical logic
├── data_upload_engine/   # File readers (CSV, Excel, PDF, PPTX + OCR)
├── viz_engine/           # Charts and visualisations
├── ai/                   # Optional local LLM integration
├── models/               # Drop your .gguf model files here
└── download_model.py     # Downloads an AI model in one step
```

---

<br>

## The AI Layer: Interpretation Without the Cloud

Once you have your analysis results, you can go one step further: hit **"Get AI Interpretation"** and get a plain-English explanation of what the numbers actually mean. No jargon, no follow-up meeting required. The tool offers three modes, switchable in the sidebar at any time:

<ul>
  <li><strong>Rule-based (always available)</strong> — pre-written logic that spots patterns and surfaces them as readable findings. Zero dependencies, instant results. Always works.</li>
  <li><strong>Local LLM — no server needed</strong> — a quantized language model (Qwen 2.5 · 1.5B) running entirely on your CPU via <code>llama-cpp-python</code>. No GPU, no API key, no data leaving the machine. ~30s for the first response.</li>
  <li><strong>Ollama — server required</strong> — if you already run Ollama locally, point the tool at it and use any model you have installed.</li>
</ul>

![AI settings](/img/posts/ai_local_agent/preview4.webp)
*Switch interpretation mode in the sidebar — rule-based, local LLM, or Ollama.*

---

<br>

## Data Quality First

Most self-service tools will cheerfully visualize a five-row sample and let you draw conclusions from it. Local Analyst checks the dataset before running anything and flags problems with severity indicators. Four rows? Critical warning before any analysis runs. Bad input should never produce confident output.

![Data quality indicators](/img/posts/ai_local_agent/preview6.webp)
*Hard stops for datasets too small or too broken to analyze reliably.*

---

<br>

## The Challenges — Where It Got Fun

**Challenge #1: Reading Whatever File Someone Throws at You**

Business data doesn't arrive in clean CSVs. It arrives as a 47-tab Excel file, a PowerPoint with screenshots of charts, or a PDF export from some tool that generates tables as images. Building reliable ingestion for all of these — including OCR via `easyocr` for image-based tables — was easily the messiest part. Edge cases everywhere.

<br>

**Challenge #2: Auto-detecting What Each Column Actually Means**

The tool tries to figure out which column is "date," which is "revenue," which is "customer ID" — automatically. Sounds simple. It is not. People name columns in spectacularly creative ways. The column mapping logic went through about six iterations before it stopped confidently labeling `customer_status` as the revenue field.

<br>

**Challenge #3: Running an LLM Locally on a Plain CPU**

Getting `llama-cpp-python` to install reliably across Windows, Mac, and Linux without requiring a C++ compiler took some creative packaging. The result: one `pip install`, download the model with one Python script, and you have a working local LLM explaining your analysis results in plain English.

---

<br>

## What Makes It Stand Out

<ul>
  <li><strong>🔒 The privacy angle</strong> — your data never leaves localhost. Not for analysis, not for the AI. This matters enormously in corporate environments where sending a customer CSV to some cloud service is a GDPR conversation waiting to happen.</li>
  <li><strong>📦 Zero cloud dependency</strong> — after the initial install, the tool works completely offline. Camp in the mountains, work on a flight, be in a GDPR audit — it doesn't care. It just runs.</li>
  <li><strong>🧠 Real statistics, not just charts</strong> — most "self-service analytics" tools give you bar charts. Local Analyst gives you RFM customer segments, statistical significance on your A/B tests, Pareto breakdowns. The Full Scan runs 11 analysis types at once and surfaces findings with severity ratings.</li>
</ul>

---

<br>

## What I Learned

**Modular from day one saves you later.** The separation into engines meant I could rewrite the PDF reader without touching a single line of statistical analysis code. Adding a new analysis tab is mostly just adding a new module — the rest of the system doesn't care.

**The 80% use case is much harder than you think.** Building something that works with clean test data takes a weekend. Building something that reliably handles whatever a real-world user uploads takes considerably longer. Most of the work was edge cases, not features.

**Local AI is genuinely here.** Running a 1.5B parameter language model on a laptop CPU and getting coherent, contextually relevant analysis summaries in under a minute is impressive. It's not GPT-4, but it doesn't need to be. For explaining a correlation heatmap in plain English? More than good enough.

**Built with [Claude Code](https://claude.ai/code).** The entire project was developed using Claude Code as an AI coding partner — from architecture decisions to debugging edge cases in the PDF extractor. A fitting irony: a tool for making data accessible to non-technical people, built with the help of an AI assistant.

---

<br>

> *"Trust the numbers, question the narrative."* — the last line of the README, and probably a decent life philosophy too.

<br>

That's a wrap for this post. The project is fully open source, MIT licensed, and documented well enough for a non-developer to install. Takes about 10 minutes from zero to running your first analysis. All files stay on your machine, always.

If it saves even one person from forwarding their CSV to a cloud tool they don't fully trust — or from emailing their data analyst at 4pm on a Thursday — I'll count it as a win. Try it yourself and happy experimenting! :)

👉 **[github.com/MaikDulle/Local_analyst](https://github.com/MaikDulle/Local_analyst)**
