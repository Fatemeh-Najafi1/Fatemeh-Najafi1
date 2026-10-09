<!-- Header -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1e1b4b,50:4c1d95,100:0f766e&height=220&section=header&text=Fatemeh%20Najafi&fontSize=52&fontColor=ffffff&animation=fadeIn&fontAlignY=36&desc=Software%20Developer%20%C2%B7%20AI%20Security&descSize=22&descAlignY=58" alt="Fatemeh Najafi, Software Developer and AI Security" width="100%" />
</p>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=A78BFA&center=true&vCenter=true&width=760&lines=Full-stack+web+%26+mobile+developer;Next.js+%C2%B7+NestJS+%C2%B7+TypeScript+%C2%B7+Python;Prompt+injection+%C2%B7+memory+poisoning+%C2%B7+model-file+malware;Testing+how+things+break+before+attackers+do" alt="Typing intro" />
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/fatemeh-najafi-797555382"><img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
  <a href="mailto:hedyehwrt2@gmail.com"><img src="https://img.shields.io/badge/Email-Say_hi-7C3AED?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" /></a>
  <img src="https://img.shields.io/badge/Based_in-Dubai-334155?style=for-the-badge&logo=googlemaps&logoColor=white" alt="Based in Dubai" />
  <img src="https://komarev.com/ghpvc/?username=Fatemeh-Najafi1&color=7c3aed&style=for-the-badge&label=Profile+views" alt="Profile views" />
</p>

---

## 👋 About me

I'm **Fatemeh**, a fourth-year Computer Science student at **Canadian University Dubai** (GPA 3.85) and a
**Software Development Intern at Elchai Group**, where I build and security-test a multi-tenant web platform
and its mobile app.

- 💻 I ship features end to end: **Next.js** front end, **NestJS** back end, Stripe payments, SendGrid email, deployed on Vercel and Render behind Cloudflare.
- 🛡️ On the side I build **AI security tools**: detecting malicious ML model files, prompt injection and memory poisoning in AI agents.
- 🔍 I test like an attacker: auth, access control and payment flows are where I start looking.
- 🌍 Speak **Persian** and **English**. Open to remote developer, AI security and AI-training roles.

---

## 🛠️ What I work on

<table>
  <tr>
    <td width="50%" valign="top">
      <h3>🌐 Full-Stack Web &amp; Mobile</h3>
      Next.js and NestJS apps in TypeScript, REST APIs, Stripe and SendGrid integrations, and mobile features, deployed on Vercel, Render and Cloudflare.
    </td>
    <td width="50%" valign="top">
      <h3>🤖 AI Security</h3>
      Static analysis of ML model files, prompt-injection and memory-poisoning detection for AI agents, benchmarked against real datasets.
    </td>
  </tr>
  <tr>
    <td width="50%" valign="top">
      <h3>🛡️ Security &amp; QA Testing</h3>
      End-to-end testing of authentication, identity verification, role-based access control and transaction flows, with clear, reproducible bug reports.
    </td>
    <td width="50%" valign="top">
      <h3>📊 Data &amp; ML</h3>
      Python data pipelines, clustering and classification with scikit-learn, and NLP apps built on sentence embeddings.
    </td>
  </tr>
</table>

---

## 🧰 Tech stack

<p align="center">
  <b>Languages &amp; frameworks</b><br/><br/>
  <img src="https://skillicons.dev/icons?i=ts,js,py,java,c,html,css,react,nextjs,nestjs,nodejs,flask&perline=12" alt="Languages and frameworks" />
</p>

<p align="center">
  <b>Deploy, tools &amp; security</b><br/><br/>
  <img src="https://skillicons.dev/icons?i=git,github,gitlab,githubactions,vercel,cloudflare,mysql,linux,kali,vscode,figma,sklearn&perline=12" alt="Deploy, tools and security" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Stripe-635BFF?style=for-the-badge&logo=stripe&logoColor=white" alt="Stripe" />
  <img src="https://img.shields.io/badge/Render-46E3B7?style=for-the-badge&logo=render&logoColor=black" alt="Render" />
  <img src="https://img.shields.io/badge/SendGrid-1A82E2?style=for-the-badge&logoColor=white" alt="SendGrid" />
  <img src="https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white" alt="Streamlit" />
  <img src="https://img.shields.io/badge/pytest-0A9EDC?style=for-the-badge&logo=pytest&logoColor=white" alt="pytest" />
</p>

---

## 🚀 Featured project: [picklelens](https://github.com/Fatemeh-Najafi1/picklelens)

**Is this AI model file safe to load?** Most ML models ship as Python *pickles*, which can run code the moment
you load them. picklelens reads the file **without ever loading it** and tells you exactly what it would do.

- 🔬 Replays the pickle's instructions symbolically to find code a model would run on load (PyTorch, Keras, NumPy, pickle and 7z files).
- 🏷️ Classifies the behaviour (ransomware, reverse shell, dropper, infostealer) with **MITRE ATT&CK** tags, extracted indicators and a 0–100 risk score.
- 📈 Benchmarked against picklescan, the scanner Hugging Face uses: **19/19 malicious samples blocked vs. 16/19**, with 0 false alarms.
- 🕵️ Includes **agentaudit**, which spots AI agents hijacked by prompt injection or memory poisoning. On the 1,054-case InjecAgent benchmark it caught **94% of data-exfiltration attacks** at a 3% false-positive rate.
- ⚙️ JSON, HTML and SARIF reports, plus a CI gate that blocks unsafe models.

---

## 📂 More projects

| Project | What it is | Stack | Links |
|---|---|---|---|
| **Dubai Weather & Events** | Live weather, events and a 48-hour activity recommender | Python, Flask, JavaScript | [Code](https://github.com/Fatemeh-Najafi1/Dubai-Weather-Events) · [Live](https://dubai-weather-events.onrender.com/) |
| **Resume Matcher** | Scores how well a resume fits a job description using NLP embeddings | Python, Streamlit, sentence-transformers | [Code](https://github.com/Fatemeh-Najafi1/resume-matcher) · [Live](https://resume-m-nkdtv7rpdzsjvtktlqx5zt.streamlit.app/) |
| **Rabin-Karp Visualizer** | Step-by-step rolling-hash animation with a live complexity chart | JavaScript, SVG | [Code](https://github.com/Fatemeh-Najafi1/rabin-karp-visualizer) · [Live](https://fatemeh-najafi1.github.io/rabin-karp-visualizer/) |
| **0/1 Knapsack & NP-Completeness** | Animates Brute-Force, DP and Greedy, plus a Subset Sum → Knapsack reduction | JavaScript, SVG | [Code](https://github.com/Fatemeh-Najafi1/Interactive-NP-app) · [Live](https://fatemeh-najafi1.github.io/Interactive-NP-app/) |
| **NYC Air Quality Mining** | Outlier detection, K-means clustering and Random Forest on ~18,800 rows | Python, scikit-learn | [Code](https://github.com/Fatemeh-Najafi1/Datamining) |

---

## 🧭 How I work

```text
verify  > assume      every fix checked in the browser and against the API
proof   > claims      benchmark it, then state the limits honestly
break   > hope        ask how it fails before calling it done
```

---

## 🐍 Contribution activity

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/output/github-snake-dark.svg" />
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/output/github-snake.svg" />
    <img alt="Contribution snake animation" src="https://raw.githubusercontent.com/Fatemeh-Najafi1/Fatemeh-Najafi1/output/github-snake-dark.svg" />
  </picture>
</p>

---

<p align="center">
  <b>Building things that work, and testing that they can't be broken.</b><br/>
  <a href="https://www.linkedin.com/in/fatemeh-najafi-797555382">LinkedIn</a> ·
  <a href="mailto:hedyehwrt2@gmail.com">Email</a>
</p>

<!-- Footer -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:1e1b4b,50:4c1d95,100:0f766e&height=120&section=footer" alt="" width="100%" />
</p>
