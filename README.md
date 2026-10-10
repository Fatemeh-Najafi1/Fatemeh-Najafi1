<h1 align="center">Fatemeh Najafi</h1>

<p align="center">
  <b>Software developer · AI &amp; ML security</b>
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/fatemeh-najafi-797555382"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=flat-square&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:hedyehwrt2@gmail.com"><img src="https://img.shields.io/badge/Email-7C3AED?style=flat-square&logo=gmail&logoColor=white" alt="Email" /></a>
  <img src="https://img.shields.io/badge/Dubai,_UAE-334155?style=flat-square&logo=googlemaps&logoColor=white" alt="Dubai, UAE" />
  <img src="https://img.shields.io/badge/CS_@_CUD-GPA_3.85-0f766e?style=flat-square" alt="Computer Science at Canadian University Dubai, GPA 3.85" />
</p>

<!-- Hand-written animated SVG: a real picklelens scan, start to verdict -->
<p align="center">
  <img src="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/main/assets/scan-demo.svg" alt="Animated terminal showing picklelens scanning a PyTorch model file, interpreting its pickle opcode stream without executing it, and reporting it malicious with a 100/100 risk score and MITRE ATT&CK tags" width="100%" />
</p>

```
Software Development Intern @ Elchai Group ..... multi-tenant web platform + mobile app (Next.js / NestJS / TS)
B.Sc. Computer Science @ CUD ................... 4th year · expected 2027 · GPA 3.85
Current research ............................... pickle reachability analysis · agent provenance & taint tracking
```

---

# 🛡️ Security work

## `picklelens` — reachability scanner for ML model files

<a href="https://github.com/Fatemeh-Najafi1/picklelens"><img src="https://img.shields.io/badge/repo-picklelens-7C3AED?style=flat-square&logo=github&logoColor=white" alt="picklelens repository" /></a>
<img src="https://img.shields.io/badge/97_tests-passing-238636?style=flat-square" alt="97 tests passing" />
<img src="https://img.shields.io/badge/core-stdlib_only-0f766e?style=flat-square" alt="Standard library only core" />
<img src="https://img.shields.io/badge/output-SARIF_2.1.0-334155?style=flat-square" alt="SARIF 2.1.0 output" />
<img src="https://img.shields.io/badge/licence-MIT-334155?style=flat-square" alt="MIT licence" />

> *Most ML models ship as Python **pickles**. A pickle isn't data — it's a program for a stack machine
> that executes the moment you call `torch.load`. Loading an untrusted model is, worst case, `exec(attacker_code)`.*

The scanner Hugging Face runs in its own pipeline (`picklescan`) reasons about **names** — it grades what a
pickle *references* against an allow/block list. picklelens instead **interprets the opcode stream over
symbolic values** and records every callable the program actually *invokes*, never importing, deserializing
or executing anything. It answers *"does this file call `os.system`?"* rather than *"does the string
`os.system` appear in it?"* — so `getattr(__import__('os'), 'system')` resolves and reports, while a
state dict that merely mentions `OrderedDict` stays clean.

That one choice is what produces the precision:

| evaluation | picklelens | best of picklescan · ModelScan · Fickling · ModelHawk |
|---|---|---|
| Labelled corpus — 23 malicious (incl. evasions) / 11 benign | **100% recall · 0% FP** | 91% recall (ModelHawk) · picklescan 87% |
| 20 real HF models + 10 externally-authored malicious | **0% FP** — only tool at zero · 70% recall | picklescan 5% FP · ModelHawk 10% FP (80% recall) |
| 100 most-downloaded Hub models (761 repos walked) | **0% false positives** | ModelHawk 30% FP |

The only tool at 100% recall with zero false alarms, and the only one holding 0% FP on real models at scale —
ModelHawk's "unfamiliar import is suspicious" heuristic fires on ordinary `training_args.bin` configs that
reference classes but never reach an execution sink. The real-model run also **found a gap in my own tool**
(a `sys.exit` DoS payload both competitors caught), now fixed and pinned by a regression test.

**Scope, stated plainly:** pickle-based model files only — not a general antivirus, no PE/ELF analysis, no
signature database. Recall is high but never claimed complete.

<sub>Five-way comparison tables, MITRE ATT&CK mapping, SARIF output, archived run records and the full
methodology live in the <a href="https://github.com/Fatemeh-Najafi1/picklelens">repo</a>.</sub>

<br/>

## `agentaudit` — detecting a hijacked AI agent from its trace

Same idea, new target: **static, post-hoc analysis of something adversarial.** Given an agent's execution
trace, decide whether it was turned against its operator by **indirect prompt injection** or **memory
poisoning**. The core signal is **provenance/taint**, not vibes — an action is a betrayal when its
destination or value originated in untrusted input and *never appeared in the operator's request*.

<!-- Hand-written animated SVG: taint propagating through the provenance graph -->
<p align="center">
  <img src="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/main/assets/taint-flow.svg" alt="Animated provenance graph: a trusted operator request and an untrusted tool result flow into an agent; the email destination traces back to the untrusted content, so the action is flagged BETRAYING" width="100%" />
</p>

Runs **CPU-only with no LLM in the loop**, so it evaluates against third-party attack data at full scale:

| benchmark | configuration | recall | false positives |
|---|---|---|---|
| **InjecAgent** — 1,054 cases | provenance/taint only | 70% *(exfil 100%, direct-harm 38%)* | **0%** |
| **InjecAgent** — 1,054 cases | + capability restriction | **100%** | **0%** |
| **AgentDojo** — 134 pairs, 4 suites | provenance + category | **93%** *(125/134)* | **0%** |

The honest shape of it: taint catches data-stealing perfectly but only part of direct-harm — many harmful
actions carry no data to trace, a *structural* limit — and a per-task tool allowlist closes the gap. Layered
defense, measured rather than asserted. AgentDojo's *travel* suite (24/33) is the documented weak spot,
written up as such instead of quietly dropped from the table.

<sub>Detection rules, the memory plant→trigger lifecycle, per-suite breakdowns and run records are in the
<a href="https://github.com/Fatemeh-Najafi1/picklelens">repo</a>.</sub>

---

# 🧪 Other engineering

## Resume Matcher — a guarantee that is *structural*, not promised

<a href="https://github.com/Fatemeh-Najafi1/resume-matcher"><img src="https://img.shields.io/badge/code-GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="Resume Matcher code" /></a>
<a href="https://resume-m-nkdtv7rpdzsjvtktlqx5zt.streamlit.app/"><img src="https://img.shields.io/badge/live-demo-FF4B4B?style=flat-square&logo=streamlit&logoColor=white" alt="Resume Matcher live demo" /></a>
<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
<img src="https://img.shields.io/badge/sentence--transformers-FFB000?style=flat-square" alt="sentence-transformers" />

Most resume tools suggest adding skills you don't have. This one scores how well you *genuinely* match a role
and reports the gap — and it **cannot fabricate a skill, by construction**: the gap report is a literal set
difference over the two documents, with **no model anywhere in that code path**. The optional LLM analysis is
layered strictly *on top* of that result, never in place of it. The same instinct as the security work —
prefer a property you can prove over a behaviour you have to trust.

<p align="center">
  <img src="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/main/assets/resume-match.svg" alt="Animated pipeline: a resume and job posting flow through Reader, Cleaner, Embedder, Comparator and Generator, producing a match score and a set-difference list of missing skills" width="100%" />
</p>

A five-stage pipeline — **Reader → Cleaner → Embedder → Comparator → Generator** — ingests TXT/DOCX/PDF or
scrapes a posting straight from a URL, normalizes and lemmatizes both documents, extracts structured metadata
(GPA, years of experience, contacts), embeds with `all-MiniLM-L6-v2`, and scores cosine similarity. It then
decomposes the posting into individual **requirements**, matches each against individual resume lines, and
reports the specific line that evidences each one — plus missing keywords ranked by how often the posting
repeats them.

## Dubai Weather & Events — a REST service that degrades gracefully

<a href="https://github.com/Fatemeh-Najafi1/Dubai-Weather-Events"><img src="https://img.shields.io/badge/code-GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="Dubai Weather and Events code" /></a>
<a href="https://dubai-weather-events.onrender.com/"><img src="https://img.shields.io/badge/live-demo-46E3B7?style=flat-square&logo=render&logoColor=black" alt="Dubai Weather and Events live demo" /></a>
<img src="https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white" alt="Flask" />
<img src="https://img.shields.io/badge/Chart.js-FF6384?style=flat-square&logo=chartdotjs&logoColor=white" alt="Chart.js" />

A full-stack Flask app serving live Dubai weather, a 5-day Chart.js forecast, and filterable events over a REST
API. The parts I'd point at in review:

<p align="center">
  <img src="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/main/assets/weather-scan.svg" alt="Animated 48-hour forecast scan: a scanner sweeps across hourly bars scoring each slot, then highlights the best outdoor window" width="100%" />
</p>

- **A cache with a stale fallback** — 10-minute server-side cache, and if OpenWeather is unreachable it serves
  data up to 6 hours old rather than failing the page. Deciding *what to do when the upstream is down* is the
  actual engineering.
- **A recommendation engine** that scans the next 48 hours of forecast, scores each daytime slot by humidity
  and temperature, and surfaces the single best outdoor window.
- Debounced live search across date range / category / keyword, °C↔°F and dark-mode toggles persisted in
  `localStorage`, and staggered auto-refresh (weather 10 min, events 5 min). Deployed on Render behind gunicorn.

## Algorithm visualizers — making complexity *visible*, not just animated

<a href="https://github.com/Fatemeh-Najafi1/rabin-karp-visualizer"><img src="https://img.shields.io/badge/Rabin–Karp-code-181717?style=flat-square&logo=github&logoColor=white" alt="Rabin-Karp code" /></a>
<a href="https://fatemeh-najafi1.github.io/rabin-karp-visualizer/"><img src="https://img.shields.io/badge/live-demo-0f766e?style=flat-square" alt="Rabin-Karp live demo" /></a>
<a href="https://github.com/Fatemeh-Najafi1/Interactive-NP-app"><img src="https://img.shields.io/badge/Knapsack_&_NP-code-181717?style=flat-square&logo=github&logoColor=white" alt="Knapsack and NP-completeness code" /></a>
<a href="https://fatemeh-najafi1.github.io/Interactive-NP-app/"><img src="https://img.shields.io/badge/live-demo-0f766e?style=flat-square" alt="Knapsack live demo" /></a>
<img src="https://img.shields.io/badge/vanilla_JS_+_SVG-F7DF1E?style=flat-square&logo=javascript&logoColor=black" alt="Vanilla JavaScript and SVG" />

Two teaching tools, no frameworks or libraries — just JavaScript and hand-built SVG.

<p align="center">
  <img src="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/main/assets/rabin-karp.svg" alt="Animated Rabin-Karp: a four-character window slides across ABRACADABRA, the rolling hash updates each step, a hash collision triggers a spurious hit, and true matches are found at indices 0 and 7" width="100%" />
</p>

**Rabin-Karp** makes the *failure mode* the subject. A rolling hash is fast until collisions force character
verification, and enough collisions drag O(n+m) down to O(n×m). So the visualizer ships a **collision mode
(Q=101)** that deliberately shrinks the modulus to manufacture spurious hits, a letter-by-letter comparison
panel that opens on every collision, and a **live SVG chart plotting theoretical O(n+m) against actual
cumulative character work** — the divergence is visually dramatic. A performance score,
`windows ÷ (hash ops + char checks)`, approaches 1 in the ideal case and collapses toward 0 under heavy
collisions; a worst-case preset (`AAAAAAAA` / `AAAA`) draws the O(n×m) ceiling as a reference line.

**0/1 Knapsack** goes further than *how* an algorithm runs and shows *why the problem is hard*. It walks the
NP-completeness argument interactively: a **verifier** you feed candidate certificates to, which counts
operations to demonstrate that verification is O(n) — exactly what "in NP" requires — and a live
**Subset Sum → Knapsack reduction** where editing the Subset Sum instance updates the Knapsack instance in
place, with both proof directions (⇒ and ⇐) explorable. It explains why pseudo-polynomial O(nW) DP doesn't
contradict NP-completeness, then animates Brute-Force, DP (with dependency arrows drawn across the table) and
Greedy side by side — **automatically flagging the inputs where greedy disagrees with DP.**

## NYC Air Quality — clustering and classification pipeline

<a href="https://github.com/Fatemeh-Najafi1/Datamining"><img src="https://img.shields.io/badge/code-GitHub-181717?style=flat-square&logo=github&logoColor=white" alt="NYC air quality code" /></a>
<img src="https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikitlearn&logoColor=white" alt="scikit-learn" />
<img src="https://img.shields.io/badge/pandas-150458?style=flat-square&logo=pandas&logoColor=white" alt="pandas" />

End-to-end data mining over ~18,800 rows of the NYC Community Air Survey (NO₂, PM2.5, O₃ across 59 community
districts), asking whether distinct air-quality regimes can be discovered automatically and then predicted.

<p align="center">
  <img src="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/main/assets/clustering.svg" alt="Animated K-means clustering: scattered air-quality readings resolve into three pollution regimes as the centroids converge" width="100%" />
</p>

Profiling → missing-value handling → **Isolation Forest** outlier removal → **filtering to summer months to
control for seasonal confounding** → z-score standardization → one-hot encoding → **K-means** (K=3 chosen by
elbow, validated at silhouette 0.34 / Calinski-Harabasz 687) → **Random Forest** trained on the cluster labels
and cross-validated. The three recovered regimes: clean (109 districts), moderate (356), high-traffic (420).
Built with [@MahnourAslam](https://github.com/MahnourAslam).

---

# 🧠 Skills

What I can reason about and do, independent of any particular tool.

| Area | |
|---|---|
| **Program analysis** | Static analysis · symbolic/abstract interpretation of bytecode · reachability &amp; call-graph construction · taint and provenance tracking · information-flow control (FIDES / CaMeL paradigm) |
| **AI &amp; ML security** | Indirect prompt injection · memory poisoning and cross-session plant→trigger lifecycles · ML supply-chain and model-file attacks · deserialization RCE · capability restriction / tool allowlisting · agent trace auditing |
| **Offensive &amp; defensive testing** | Threat modelling · authentication and authorization testing · role-based access-control bypass · payment and transaction flow abuse · evasion-technique analysis · MITRE ATT&amp;CK mapping · reproducible defect reports with severity and root cause |
| **Benchmarking &amp; evaluation** | Labelled corpus design · recall/false-positive tradeoff analysis · evaluation against third-party benchmarks (InjecAgent, AgentDojo) · reproducibility and provenance-stamped runs |
| **Software engineering** | OOP · data structures &amp; algorithms · REST API design · client–server architecture · relational schema design &amp; normalization · CI gating · test-driven regression pinning |
| **Data &amp; ML** | NLP with sentence embeddings · clustering · classification · outlier detection · feature engineering · data pipelines |

---

# 🧰 Tools

<p align="center">
  <b>Languages</b><br/>
  <img src="https://skillicons.dev/icons?i=py,ts,js,java,c,mysql,html,css&perline=8" alt="Python, TypeScript, JavaScript, Java, C, SQL, HTML, CSS" />
</p>

<p align="center">
  <b>Frameworks &amp; libraries</b><br/>
  <img src="https://skillicons.dev/icons?i=nextjs,nestjs,nodejs,react,flask,sklearn&perline=8" alt="Next.js, NestJS, Node.js, React, Flask, scikit-learn" />
  <br/>
  <sub>pandas · NumPy · NLTK · sentence-transformers · Streamlit · pytest · Chart.js</sub>
</p>

<p align="center">
  <b>Platform, infra &amp; security tooling</b><br/>
  <img src="https://skillicons.dev/icons?i=git,github,gitlab,githubactions,vercel,cloudflare,linux,kali,vscode,figma&perline=10" alt="Git, GitHub, GitLab, GitHub Actions, Vercel, Cloudflare, Linux, Kali, VS Code, Figma" />
  <br/>
  <sub>Render · Stripe · SendGrid · Wireshark · SARIF · Claude Code</sub>
</p>

---

# 📜 Certifications

<p align="center">
  <a href="https://www.credly.com/badges/70684a94-262c-4028-982a-7323c5dfff4b/public_url"><img src="https://img.shields.io/badge/Cisco-Networking_Devices_&_Initial_Configuration-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco: Networking Devices and Initial Configuration — verify on Credly" /></a>
  <a href="https://www.credly.com/badges/37e51572-9aa7-4ec6-9a41-e4a8ade6aceb/public_url"><img src="https://img.shields.io/badge/Cisco-C_Essentials_1-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco: C Essentials 1 — verify on Credly" /></a>
  <a href="https://www.credly.com/badges/80e946f2-54b7-4c0d-b98c-c24bc5b85da1/public_url"><img src="https://img.shields.io/badge/Cisco-Introduction_to_Modern_AI-1BA0D7?style=for-the-badge&logo=cisco&logoColor=white" alt="Cisco: Introduction to Modern AI — verify on Credly" /></a>
</p>

<p align="center">
  <sub>Every badge above links to its public Credly verification page.</sub>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/IELTS_Academic-7.5-0f766e?style=for-the-badge" alt="IELTS Academic 7.5" />
  <img src="https://img.shields.io/badge/IEEE-Student_Member-00629B?style=for-the-badge&logo=ieee&logoColor=white" alt="IEEE Student Member" />
  <img src="https://img.shields.io/badge/Languages-Persian_·_English-334155?style=for-the-badge" alt="Persian native, English fluent" />
</p>

### Activities &amp; coursework

<img src="https://img.shields.io/badge/Cybersecurity_Club-CUD_2025-da3633?style=flat-square" alt="Cybersecurity Club, Canadian University Dubai, 2025" />
<img src="https://img.shields.io/badge/IEEE-CTF_participant-00629B?style=flat-square" alt="IEEE CTF participant" />
<img src="https://img.shields.io/badge/workshops-Wireshark_·_Kali_Linux-1793D1?style=flat-square" alt="Wireshark and Kali Linux workshops" />

<img src="https://img.shields.io/badge/Data_Mining-A%2B-238636?style=flat-square" alt="Data Mining A plus" />
<img src="https://img.shields.io/badge/Databases-A%2B-238636?style=flat-square" alt="Databases A plus" />
<img src="https://img.shields.io/badge/Data_Structures-A%2B-238636?style=flat-square" alt="Data Structures A plus" />
<img src="https://img.shields.io/badge/Operating_Systems-A%2B-238636?style=flat-square" alt="Operating Systems A plus" />
<img src="https://img.shields.io/badge/Algorithms-·-334155?style=flat-square" alt="Algorithms" />
<img src="https://img.shields.io/badge/Communication_Networks-·-334155?style=flat-square" alt="Communication Networks" />

---

<p align="center">
  <a href="https://www.linkedin.com/in/fatemeh-najafi-797555382">LinkedIn</a> ·
  <a href="mailto:hedyehwrt2@gmail.com">Email</a> ·
  <a href="https://github.com/Fatemeh-Najafi1/picklelens">picklelens</a>
</p>
