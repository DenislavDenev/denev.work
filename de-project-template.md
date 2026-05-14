# Data Engineering Portfolio Project Description Template

Synthesised from: dataexpert.io, The Data Forge (2026), pipeline2insights, WeCloudData,
Seattle Data Guy, data-engineering-community project template, Benjamin Bennett Alexander,
Resume Worded, Exponent, BeamJobs, 10+ DE GitHub portfolios.

---

## Why This Exists

Most DE portfolios fail for the same reasons:
- Generic projects with no business context ("I built a pipeline")
- Tools listed without explaining why they were chosen
- No mention of what breaks and how you handle it
- No scale numbers (rows, GB, frequency, latency)
- No architecture diagram, so the reader cannot visualise the system

Hiring managers spend 6 to 30 seconds on a portfolio entry before deciding whether
to keep reading. The template below is designed to pass that scan and then hold up
under a technical interview.

---

## The Core Principle

Every bullet answers one of these questions:

| Question | Why it matters |
|---|---|
| What problem does this solve? | Business context, not just "I scraped data" |
| Why this tool over the simpler alternative? | Shows engineering judgment |
| What breaks, and how did you handle it? | Production-readiness signal |
| How big is this? | Scale separates toys from real systems |
| What does the data enable downstream? | Connects engineering to business value |

If a bullet does not answer at least one of these, cut it.

---

## Part 1. The Site Card (public-facing)

This is the short entry shown on the portfolio website.
The `desc` is shown on the card. The `highlights` open in the modal.

### The `desc` Formula

```
[Cadence + orchestrator] pipeline [what it ingests or processes].
[How the hardest engineering problem is solved],
[where output lands], and [what it enables].
```

Rules:
- Name the orchestrator explicitly (Airflow, not "automated")
- Name the storage destination (BigQuery, not "the database")
- End with what the system enables, not what it does
- Two sentences maximum. If you need three, the project is not focused enough.
- No site names, bucket paths, column names, or project IDs

Weak:
> "Built a scraping pipeline that collects price data and loads it to a data warehouse."

Strong:
> "Weekly Airflow pipeline scraping ~20,000 food products from a JS-rendered SPA.
> Selenium on Kubernetes handles JS rendering, output lands in GCS as JSONL,
> and BigQuery serves week-over-week price analysis."

---

### The `tags` Formula

```
[Language], [Compute or scraping], [Orchestrator], [Infrastructure], [Storage], [Transformation]
```

- Five to seven items only. No minor libraries, no versions.
- Order by how central the tool is to the project
- Every tool named in `highlights` must appear in `tags`
- Every tool in `tags` must appear at least once in `highlights`

---

### The `highlights` Structure (5 bullets, one per layer)

Each bullet opens with a layer label in plain text so a recruiter
scanning the modal can instantly locate the part they care about.

---

#### Bullet 1. Ingestion

```
Ingestion: [how data is collected], [why this approach over the simpler one]
```

This is where engineering judgment is demonstrated. Anyone can say
"scraped with Python." The reason is what separates a project from a tutorial.

Weak:
> "Used Selenium to scrape product data from the website."

Strong:
> "Ingestion: listing pages collected with lightweight requests, then individual
> product pages loaded via Selenium Remote WebDriver to capture JS-rendered pricing
> and product metadata absent from static HTML. Splitting pagination from rendering
> keeps the slow path narrow."

What to include:
- Source system and format (API, SPA, JSONL, Parquet, CDC stream)
- The specific reason a heavier tool was needed
- Any volume signal (pages, endpoints, records per run)

---

#### Bullet 2. Orchestration

```
Orchestration: [tool] on [infrastructure] ([deployment method]) [schedule or trigger].
Tasks run [execution model] from [environment] keeping [guarantee]
```

Do not just say "Airflow DAG." Name the execution model, how it is deployed,
and what property it guarantees (reproducibility, isolation, idempotency).

Weak:
> "Orchestrated with Apache Airflow running on a Kubernetes cluster."

Strong:
> "Orchestration: Airflow KubernetesExecutor on k3s (Helm-deployed) schedules
> the full scrape weekly. Tasks run in ephemeral pods from a custom Docker image
> with dependencies pre-installed, keeping the execution environment
> reproducible and isolated per run."

What to include:
- Tool plus deployment method (Helm, Docker Compose, managed service)
- Execution model (KubernetesExecutor, CeleryExecutor, Fargate)
- Schedule or trigger (cron, event, sensor)
- The guarantee this setup provides

---

#### Bullet 3. Engineering Challenge

```
[Problem name]: [specific failure mode] resolved by [concrete solution].
[Quantified outcome or guarantee provided]
```

This is the most memorable bullet. Every production system has one hard thing.
Name it explicitly. "OOM" beats "memory management." "Race condition" beats
"concurrency issue." "Late-arriving records" beats "data quality."

The Data Forge (2026) frames this as explaining failure scenarios: not what
you built, but what breaks and how you handled it.

Weak:
> "Implemented retry logic for improved reliability."

Strong:
> "Reliability: Chrome OOM in long-running pods resolved by recycling each
> Selenium session at a fixed URL interval and reinitialising on
> WebDriverException. Two concurrent workers share a persistent
> selenium/standalone-chrome Deployment via cluster-internal DNS,
> sustaining multi-hour scrapes without failure."

What to include:
- The specific failure mode (not a category, the actual thing that broke)
- The concrete fix (a number, a threshold, a pattern)
- The outcome or guarantee the fix provides

---

#### Bullet 4. Storage and Schema

```
Storage: [write pattern] to [intermediate layer] partitioned by [field],
loaded to [destination] with [schema approach] covering [field categories]
and [audit timestamp field]. Enables [query pattern] without [what you avoided]
```

Show you thought about the write pattern (append vs merge vs overwrite),
the intermediate layer (GCS, S3, landing zone), partitioning, schema
ownership, and downstream query implications.

Weak:
> "Data stored in BigQuery with a defined schema."

Strong:
> "Storage: scraper writes thread-safe JSONL, staged in GCS by date partition,
> then append-loaded to BigQuery staging with an explicit schema covering
> pricing, product attributes, and a scraped_at timestamp.
> Delta queries run directly off the partition without a secondary state table."

What to include:
- Write disposition (WRITE_APPEND, WRITE_TRUNCATE, MERGE)
- Intermediate landing zone and path structure
- Partition strategy and the field used
- Schema approach (explicit vs inferred, number of fields if notable)
- The query capability this enables

---

#### Bullet 5. Output and Business Value

```
[Output label]: [analytical capability] across [scale: rows, cities, records, years],
[establishing or powering or enabling] [the business-level thing this enables]
```

End with why any of this matters. This is the bullet a non-technical hiring
manager reads. Connect the engineering to a decision someone would care about.

Weak:
> "Data can be used for analysis."

Strong:
> "Historical baseline: one-time Airflow DAG backfilled 30 years of property
> prices across 28 cities spanning sales, rentals, and plots into BigQuery
> via GCS JSONL. Establishes the time-series foundation for ongoing
> weekly comparisons."

What to include:
- Scale (time range, geographic scope, record count, frequency)
- The analytical output (dashboard, query layer, model input, report)
- The decision or process it enables or replaces

---

### Complete Blank Card Template

```js
{ num: '0X', title: '',
  desc: '[Cadence] [orchestrator] pipeline [what it ingests]. [How the hard problem is solved], output lands in [storage], and [destination] serves [what it enables].',
  tags: ['', '', '', '', '', ''],
  highlights: [
    'Ingestion: [source and collection method], [specific technique] used to [capture what] that is [absent from simpler approach]. [The tradeoff this resolves].',
    'Orchestration: [tool] on [infrastructure] ([deployment method]) [schedules or triggers] [what]. Tasks run in [execution model] from [environment spec] keeping [reproducibility or isolation or idempotency] guarantee.',
    '[Problem]: [specific failure mode] resolved by [concrete solution with threshold or number]. [Two workers or fixed interval or explicit retry count] [share or recycle or reinitialise] on [failure condition], [outcome guarantee].',
    'Storage: [write pattern] to [intermediate layer] partitioned by [field], loaded to [destination] with [schema approach] covering [field categories] and [audit timestamp field]. [Query pattern] runs without [what you avoided building].',
    '[Output]: [analytical capability] across [scale], [establishing or powering] [the business-level outcome].',
  ]
},
```

---

## Part 2. The Full Project README

Use this for the GitHub repository. The Data Forge and data-engineering-community
template both converge on seven sections. This version is adapted for DE specifically.

```markdown
# [Project Title]

> One-sentence summary. What it does, what stack, what it enables.

## Problem Statement

What business or analytical problem does this solve?
What did the world look like before this pipeline existed?
Who consumes this data and what decisions does it inform?

Keep this to three to five sentences. No technical terms yet.

## Architecture

[Embed diagram here, Mermaid.js, Excalidraw, or draw.io]

Data flow left to right:
Source → Ingestion → Landing Zone → Staging → Production → Serving

Label every arrow with the format or protocol (JSONL, Parquet, NDJSON, SQL MERGE).
Label every box with the tool name and deployment (BigQuery, GCS, Airflow on k3s).

## Data Flow

Step-by-step numbered list of exactly what happens end to end.
Be specific. File names, table names, and schedule all matter here.

1. [Source] to [how collected] to [intermediate file or format]
2. [File] to [uploaded to] to [landing zone path pattern]
3. [Landing zone] to [loaded to] to [staging table] via [load method]
4. [Staging] to [transformed by] to [production table] via [transformation tool]
5. [Production] to [served to] to [consumer or dashboard or downstream model]

## Key Engineering Decisions

For each major decision, state what you chose, what you rejected, and why.

| Decision | Chosen | Rejected | Reason |
|---|---|---|---|
| Execution model | KubernetesExecutor | LocalExecutor | Task isolation, no shared state |
| Ingestion method | Selenium + requests hybrid | Selenium only | Listing pages do not need a browser, 10x faster |
| Write pattern | WRITE_APPEND + scraped_at | WRITE_TRUNCATE | Preserves history for time-series queries |
| Schema | Explicit SchemaFields | Auto-detect | Schema drift caught at load time, not query time |

## Engineering Challenges

Describe the one to three hardest problems encountered and how they were solved.
Use the format: Problem, Root cause, Solution, Outcome.

### [Challenge Name e.g. "Chrome OOM in long-running pods"]

**Problem:** [What was failing and how it manifested]
**Root cause:** [Why it was happening, be specific]
**Solution:** [The concrete fix, include thresholds, patterns, tools]
**Outcome:** [The guarantee or measurable improvement]

## Scale and Performance

- Records per run: ~[N]
- Run frequency: [schedule]
- Average run duration: [time]
- Storage footprint: [GB or TB]
- Partition strategy: [field plus granularity]

## Trade-offs and Limitations

What did you consciously not do, and why?
What would you change at 10x the current scale?
What monitoring or data quality layer is missing?

Be honest here. Hiring managers respect engineers who know their system's limits.

## How to Run

### Prerequisites
- [Tool] [version]
- [Credentials or environment variables needed]
- [Infrastructure requirements]

### Setup
\`\`\`bash
# numbered steps
\`\`\`

### Run locally
\`\`\`bash
# commands
\`\`\`

## Lessons Learned

What would you do differently?
What surprised you?
What would you add next?
```

---

## Part 3. The Pre-Publish Checklist

Run through this before adding any project to the portfolio.

### Card-level (`desc` and `highlights`)

- [ ] `desc` names the orchestrator explicitly
- [ ] `desc` names the storage destination explicitly
- [ ] `desc` ends with what the data enables, not what it does
- [ ] Every tool in `tags` appears at least once in `highlights`
- [ ] Every tool in `highlights` appears in `tags`
- [ ] Bullet 3 names a specific failure mode, not a category
- [ ] At least one bullet contains a number (rows, cities, years, workers, interval)
- [ ] No site names, bucket paths, project IDs, or column names exposed
- [ ] Each bullet opens with a layer label (Ingestion, Orchestration, etc.)
- [ ] Each bullet explains why, not just what

### README-level

- [ ] Architecture diagram included
- [ ] Data flow numbered step by step
- [ ] Key decisions table filled out (chosen vs rejected vs reason)
- [ ] At least one engineering challenge documented with root cause
- [ ] Scale numbers present (records, frequency, duration)
- [ ] Trade-offs and limitations section is honest
- [ ] How to Run is complete enough for someone else to reproduce it

### Seniority signals (aim for at least three)

- [ ] Idempotency mentioned or demonstrated
- [ ] Failure scenario documented with recovery mechanism
- [ ] Partitioning strategy explained with the reason for the chosen field
- [ ] Cost or resource constraint influenced a decision
- [ ] An alternative approach was considered and rejected with a reason
- [ ] Schema is explicit (not auto-detected)
- [ ] The downstream consumer of the data is identified

---

## Part 4. Language Reference

### Strong action verbs (open every bullet with one)

| Category | Verbs |
|---|---|
| Build | Engineered, Designed, Implemented, Architected |
| Optimise | Resolved, Reduced, Eliminated, Optimised |
| Own | Orchestrated, Deployed, Maintained, Owned |
| Enable | Enabling, Powering, Establishing, Surfacing |
| Validate | Enforced, Validated, Caught, Detected |

### Weak phrases to avoid

| Avoid | Replace with |
|---|---|
| "built a pipeline" | "Engineered an Airflow KubernetesExecutor pipeline that..." |
| "used Selenium" | "Loaded via Selenium Remote WebDriver to capture JS-rendered..." |
| "stored in BigQuery" | "Append-loaded to BigQuery staging with explicit SchemaFields..." |
| "for improved reliability" | "resolving [specific failure], sustaining [specific outcome]" |
| "data can be used for" | "enables [specific query pattern] without [what you avoided]" |
| "various tools" | Name every tool |
| "large amounts of data" | Give a number |

### The TAR formula (Task, Action, Result)

Every highlight bullet should map to this pattern even if not written in this
exact sequence:

- **Task**: What needed to happen (Chrome needed to run in Kubernetes)
- **Action**: What you did (recycled session every 20 URLs, reinitialised on exception)
- **Result**: What it guaranteed (multi-hour scrapes without OOM failure)

---

## Part 5. What Separates Junior, Mid, and Senior Descriptions

| Signal | Junior | Mid | Senior |
|---|---|---|---|
| Tool mention | Lists tools | Explains how tools are used | Explains why tools were chosen over alternatives |
| Failure handling | Not mentioned | Retries mentioned generically | Specific failure mode plus root cause plus concrete fix |
| Scale | No numbers | Record counts mentioned | Records plus frequency plus duration plus partition strategy |
| Trade-offs | None | One decision explained | Decision table with rejected alternatives |
| Business context | Missing | Implied | Explicit: who uses this and what they decide |
| Schema | Auto-detected | Defined | Explicit, versioned, with drift detection |
| Idempotency | Not considered | Mentioned | Demonstrated with the specific mechanism |

---

## Part 6. Avoiding the AI Tell

LLM-generated text has recognisable patterns. Even strong technical writing
will read as AI-generated if it includes any of these.

### Punctuation tells

The single most obvious AI marker is the em dash. Cut it everywhere.

- **Em dashes (—)** used as parenthetical interrupters. Replace with periods,
  commas, semicolons, or parentheses.
- **En dashes (–)** between phrases. Same fix.
- **Double dashes (--)** used as em dash substitutes. Same fix.
- Avoid the construction "X — Y" entirely. Split into two sentences if needed.

The rewrite test: if a bullet contains an em dash, rewrite it. The replacement
is usually two shorter sentences which read more naturally anyway.

Before:
> "Reliability: Chrome OOM in long-running pods resolved by recycling each
> Selenium session every 20 URLs — sustaining multi-hour scrapes without failure."

After:
> "Reliability: Chrome OOM in long-running pods resolved by recycling each
> Selenium session every 20 URLs. Sustains multi-hour scrapes without failure."

### Vocabulary tells

Words that signal AI-generated prose:

| Avoid | Why | Replace with |
|---|---|---|
| leverage, leveraging | overused marketing term | use, or name the action |
| comprehensive | vague | name what is covered |
| robust | vague | name the property (idempotent, fault-tolerant) |
| seamless | meaningless | cut |
| harness | overused | use |
| delve into, dive into | hedging | describe the thing directly |
| intricacies | vague | name the specific complexity |
| realm, tapestry, landscape | metaphor inflation | describe the actual domain |
| embark, journey | tutorial framing | cut |
| underscores, highlights the importance of | filler | cut and state the point |

### Sentence structure tells

- Three-item lists with parallel structure ("designed X, implemented Y, deployed Z")
- "Not only X but also Y" construction
- Sentences starting with "Crucially," "Notably," "Indeed," "Importantly"
- "A testament to" anything
- "It is worth noting that" or "It bears mentioning"
- Excessive "moreover" and "furthermore"
- Balanced sentence pairs where each clause mirrors the other

### Framing tells

- Restating the prompt back ("To address this challenge, ...")
- Closing with a forward-looking summary ("This approach paves the way for...")
- Excessive hedging ("can potentially help to...")
- Ending bullets with what would happen in an ideal future state
- "In essence" or "In summary" anywhere
- "It is important to note"

### The voice test

Read each bullet aloud. If it sounds like a press release or a textbook
introduction, rewrite it. Technical writing for a portfolio should sound like
an engineer talking to another engineer, not a marketing department.

---

*Sources:*
- [Data Engineering Portfolio: 5 Projects That Get Hired, dataexpert.io](https://www.dataexpert.io/blog/data-engineering-portfolio-projects-get-hired)
- [How to Build a Senior-Level DE Portfolio (2026), The Data Forge](https://thedataforge.medium.com/how-to-build-a-senior-level-data-engineering-portfolio-2026-version-56f045146acc)
- [The Data Engineer's GitHub Portfolio (2026), pipeline2insights](https://pipeline2insights.substack.com/p/how-to-create-data-engineering-data-engineers-github-portfolio-in-2026)
- [Portfolio Projects That Get You Hired, dataengineeringjobs.co.uk](https://dataengineeringjobs.co.uk/career-advice/portfolio-projects-that-get-you-hired-for-data-engineering-jobs-with-real-github-examples-)
- [Stop Building Random Projects, Medium/@tshraddhac](https://medium.com/@tshraddhac/stop-building-random-projects-build-these-3-data-engineer-portfolio-projects-instead-0deb723eb80a)
- [Data Engineer Portfolio Project, WeCloudData](https://weclouddata.com/career-guides/data-engineer/data-engineer-portfolio-project/)
- [Why Your Portfolio Is Not Getting You Hired, Benjamin Bennett Alexander](https://benjaminbennettalexander.substack.com/p/why-your-data-portfolio-is-not-getting)
- [Data Engineering Project Template, data-engineering-community](https://github.com/data-engineering-community/data-engineering-project-template)
- [Data Engineer Resume Guide, Exponent](https://www.tryexponent.com/blog/data-engineering-resume)
- [28 Data Engineer Resume Examples, BeamJobs](https://www.beamjobs.com/resumes/data-engineer-resume-examples)
