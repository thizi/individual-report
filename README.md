# Agent vocal local : sécurité et autonomie des agents IA

Prototype d'agent vocal qui fonctionne en local, sans internet, et revue de littérature sur la sécurité des agents IA (doctorat, en cours).

## Contexte

Les agents IA peuvent agir (lire des fichiers, utiliser des outils), ce qui crée de nouveaux risques de sécurité. Ce projet combine la lecture d'articles et la construction d'un prototype pour les étudier concrètement.

## Revue de littérature

| Article | But |
|---|---|
| **From Threat to Trust** | Méthode pour évaluer les risques d'un agent IA, couche par couche |
| **ART** (concours *Security Challenges in AI Agent Deployment*) | Mesurer si des agents respectent leurs règles face à des attaques : 1,8 million d'attaques contre 22 agents, presque tous ont violé leurs règles en 10 à 100 essais |
| **AgentDojo** | Environnement de test pour mesurer la résistance des agents aux *prompt injections* |
| **Large Multimodal Agents: A Survey** (en cours) | État de l'art des agents multimodaux, décrits en 4 composants : perception, planification, action, mémoire |

## Le prototype

### Fonctionnement

```text
Audio / micro -> Faster-Whisper -> texte -> Ollama + Qwen3:8b -> fichier _analyse.txt
```

1. L'entrée est un fichier audio ou le micro.
2. **Faster-Whisper** transcrit la voix en texte.
3. **Qwen3:8b**, exécuté par **Ollama**, analyse le texte.
4. Le résultat (transcription et analyse) est écrit dans un fichier `.txt`.

### Composants

| Composant | Rôle |
|---|---|
| Python 3.14.7 + `.venv` | Langage du programme, environnement séparé |
| `agent_vocal.py` | Script qui coordonne les étapes |
| Faster-Whisper (`small`) | Reconnaissance vocale |
| Ollama | Exécution locale du modèle de langage |
| Qwen3:8b | Analyse du texte transcrit |
| Fichiers `.wav` / `.txt` | Son enregistré / transcription et analyse |

### Lancer le programme

```powershell
cd C:\Users\thizi\agent-vocal
.\.venv\Scripts\python.exe .\agent_vocal.py
```

> On appelle directement `python.exe` du `.venv`, car `Activate.ps1` est bloqué par la politique d'exécution de PowerShell.

## Tests réalisés

- [x] Qwen3:8b répond dans le terminal
- [x] Python communique avec Ollama (« Connexion réussie »)
- [x] Le micro produit un fichier `.wav`
- [x] La transcription et l'analyse produisent un fichier `_analyse.txt`
- [x] Test complet avec le Wi-Fi coupé

## Limites

- Prototype à étapes fixes, pas un agent autonome.
- Qwen reçoit le texte transcrit, pas le son.
- Analyse du ton de la voix NON AJOUTER.


## Fil conducteur

Le survey décrit les composants d'un agent, *From Threat to Trust* aide à évaluer leurs risques, ART et AgentDojo les mesurent, et le prototype sert de petit banc d'essai concret.

## Feuille de route

- [ ] Terminer le survey *Large Multimodal Agents* et rédiger une fiche (but, idée principale, limites, lien avec le prototype)
- [ ] Rendre le prototype plus autonome : Qwen choisit lui-même ses outils (smolagents, LangChain ou appel d'outils d'Ollama)
- [ ] Ajouter l'analyse des émotions et du ton de la voix : librosa, openSMILE, modèle wav2vec2
-------------------------------------------------------------------------------------
------------------------------------------------------------------------------------------
# Local voice agent: security and autonomy of AI agents

A voice agent prototype that runs locally, without internet, plus a literature review on the security of AI agents (PhD work in progress).

## Context

AI agents can act (read files, use tools), which creates new security risks. This project combines reading research papers with building a prototype to study these risks concretely.

## Literature review

| Paper | Goal |
|---|---|
| **From Threat to Trust** | A method to assess the risks of an AI agent, layer by layer |
| **ART** (*Security Challenges in AI Agent Deployment* competition) | Measure whether agents follow their rules under attack: 1.8 million attacks against 22 agents, and almost all of them broke their rules within 10 to 100 attempts |
| **AgentDojo** | A test environment to measure how well agents resist *prompt injections* |
| **Large Multimodal Agents: A Survey** (in progress) | State of the art on multimodal agents, described through 4 components: perception, planning, action, memory |

## The prototype

### How it works

```text
Audio / microphone -> Faster-Whisper -> text -> Ollama + Qwen3:8b -> _analyse.txt file
```

1. The input is an audio file or the microphone.
2. **Faster-Whisper** transcribes the speech into text.
3. **Qwen3:8b**, run by **Ollama**, analyzes the text.
4. The result (transcription and analysis) is written to a `.txt` file.

### Components

| Component | Role |
|---|---|
| Python 3.14.7 + `.venv` | Programming language and isolated environment |
| `agent_vocal.py` | Script that coordinates the steps |
| Faster-Whisper (`small`) | Speech recognition |
| Ollama | Runs the language model locally |
| Qwen3:8b | Analyzes the transcribed text |
| `.wav` / `.txt` files | Recorded sound / transcription and analysis |

### Running the program

```powershell
cd C:\Users\thizi\agent-vocal
.\.venv\Scripts\python.exe .\agent_vocal.py
```

> We call the `.venv` `python.exe` directly because `Activate.ps1` is blocked by PowerShell's execution policy.

## Tests completed

- [x] Qwen3:8b answers in the terminal
- [x] Python communicates with Ollama ("Connexion réussie")
- [x] The microphone produces a `.wav` file
- [x] Transcription and analysis produce an `_analyse.txt` file
- [x] Full test with Wi-Fi turned off

## Limitations

- Fixed-step prototype, not an autonomous agent.
- Qwen receives the transcribed text, not the sound.
   - No Voice tone analysis.


## Common thread

The survey describes the components of an agent, *From Threat to Trust* helps assess their risks, ART and AgentDojo measure them, and the prototype serves as a small concrete testbed.



------------------------------------------------------------------------
---------------------------------------------------------------------------------------------------------------------------------------------------
-------------------------------------------------------------------------------------------------------------------------------------------
Responsible Agentic AI — Progress Update (English version)
This document summarizes recent progress across two complementary activities: reviewing a paper on attacks and defenses for AI agents, and exploring a local voice-agent prototype.
Research project
The overall goal is to study how to identify, assess, and reduce security risks in autonomous AI agents, especially when they can reason, use tools, store information, and act in real environments. In parallel, the voice prototype provides a practical setting for exploring local speech processing and vocal-signal analysis.
Guiding idea:
Autonomous AI → new capabilities → new attack surfaces → need for security and trust
Initial research question
How can we identify, assess, and reduce security risks in autonomous AI agents to make them more reliable and responsible?

This period at a glance
Activity	Progress
Scientific reading	Read a survey of attacks against LLM-based agents and the defenses discussed in the literature.
Voice prototype	Set up an initial local workflow for recording and transcribing speech, then analyzing the text with a local language model.
Next step	I identified a model for emotion analysis from voice. I plan to integrate it into the prototype over the next few days and then evaluate its results.


Part 1 — Scientific reading
Paper reviewed
Item	Information
Title	Securing LLM-based Agents Against Cyberattacks: A Comprehensive Survey on Attack Techniques and Defense Strategies
Authors	Nyashadzashe Tamuka, Topside Ehleketani Mathonsi, Olwal Thomas Otieno, Solly Maswikaneng, Tonderai Muchenje, and Tshimangadzo Mavin Tshilongamulenzhe
Journal	Journal of Computer Virology and Hacking Techniques, Volume 22, Article 38 (2026)
Publication date	May 7, 2026
DOI	10.1007/s11416-026-00622-3
Type	Open-access literature survey


What is the paper about?
The paper studies the security of agents based on large language models (LLMs). An agent may do more than generate text: it can plan steps, access memory, retrieve information, and call external tools. These capabilities make agents useful, but they also create additional attack opportunities.
This is a survey paper, not a report of one new experimental method. The authors review previous studies, organize attack techniques into categories, map defenses to risks, and identify gaps in current research.
Why can agents be more exposed?
An agent may process user instructions, webpages, retrieved documents, and tool outputs. If untrusted content contains a malicious instruction, the agent may treat it as a command, carry it into its context, or use it when proposing an action. The risk is greater when the agent has tools or permissions that let it affect external systems.
Risk surface	Example
Input and context	A malicious instruction is hidden in a document or webpage.
Prompts and instructions	Content attempts to redirect the agent or bypass its rules.
Memory and retrieval	Harmful information is stored or reintroduced later.
Tools and actions	A manipulated agent calls a tool or performs an unwanted action.
Sensitive information	The system reveals information that should remain private.
Resources and availability	An input or series of calls consumes excessive resources.


Review methodology
The authors report a structured literature search using Web of Science and Scopus, covering studies published from 2021 to 2026. Relevant work on attacks, defenses, threat models, benchmarks, and evaluation methods for LLM-based agents was examined and synthesized.
The paper also uses a five-layer reference architecture:
1. Input and perception — prompts, documents, webpages, and incoming messages.
2. Orchestration and planning — organizing tasks and assembling context.
3. Model inference — generating responses or proposed actions.
4. Memory and retrieval — storing and reusing information.
5. Tools and actions — APIs, databases, browsers, and other services.
Main attack categories
Category	General idea
Prompt injection and instruction hijacking	Introducing instructions that attempt to change the agent’s intended behavior.
Information leakage	Extracting internal instructions, private data, or sensitive information.
Malicious outputs or actions	Causing the agent to produce harmful content or misuse a tool.
Resource exhaustion	Using costly inputs or interactions to degrade availability.
Adversarial input transformations	Altering or hiding an instruction to make detection more difficult.


Main defense categories
Defense	Principle	Limitation to consider
Input filtering and sanitization	Detect or neutralize potentially malicious content before it reaches the agent.	Rephrased, obfuscated, or adaptive attacks may bypass some filters.
Adversarial training and alignment	Improve model resistance to adversarial examples and unauthorized instructions.	Robustness may decline against new attacks or examples unlike training data.
Architectural safeguards	Limit permissions, isolate memory, and separate roles or components.	Extra controls may reduce flexibility or increase processing time.
Validation, monitoring, and guardrails	Check actions, inspect outputs, and detect suspicious behavior.	False positives and false negatives remain possible.
Provenance and watermarking	Verify the source or integrity of some content where possible.	These methods do not prevent every type of manipulation.


Key takeaways
- Agent security must be evaluated at the whole-system level, not only at the language-model level.
- Tool use, memory, and external content increase the attack surface.
- Defenses can reduce risk, but no single method guarantees complete protection.
- A defense-in-depth strategy is needed: input filtering, least-privilege access, action validation, monitoring, and continuous testing.
- Defenses should be tested against adaptive attacks and realistic use cases.
Critical perspective
The paper provides a useful synthesis of a rapidly developing field, but its conclusions depend on the studies included in the review. The authors highlight challenges such as limited generalization of defenses, inconsistent evaluation, and the need to study agent-tool interactions more carefully. Multimodal agent security is another area that requires more research.
Part 2 — Local voice-agent project
Goal
Gradually develop a local prototype that can accept a voice recording, transcribe speech, and analyze the resulting text. In the longer term, I also want to explore emotion analysis based on vocal characteristics.
Current workflow
Audio file or recording
          ↓
Faster-Whisper: transcription
          ↓
Ollama + Qwen3:8B: text analysis
          ↓
Results saved to a .txt file
Progress so far
- [x] Installed and tested Ollama with Qwen3:8B locally.
- [x] Checked communication between Python and Ollama.
- [x] Tested audio recording and creation of a .wav file.
- [x] Tested transcription and text analysis, with results saved to a file.
- [x] Checked that the processing workflow runs locally.
I have also identified Emotion2Vec Plus Base (emotion2vec_plus_base), a model I can explore for emotion analysis directly from the voice signal. This feature has not yet been integrated into the prototype. I plan to add the model over the next few days and then assess how stable the results are and what limitations remain.
Current limitations
- The prototype follows predefined steps; it is not yet a fully autonomous agent.
- Qwen3:8B analyzes the transcribed text and does not directly process the audio signal in the current workflow.
- Voice-based emotion analysis is a planned next development step.
Connection to the research project
This prototype provides practical experience with the input and processing stages of an AI system. The connection to agent security will become more direct if the system evolves into an agent that can use tools or take actions. In that case, principles from the paper—limiting permissions, validating actions, and monitoring behavior—will be particularly relevant.
Next steps
- [ ] Integrate Emotion2Vec Plus Base (emotion2vec_plus_base) to explore voice-based emotion analysis.
- [ ] Test the prototype on several recordings and compare result stability.
- [ ] Later, consider adding real-time microphone input.
- [ ] Read and analyze additional scientific papers to progressively build the state of the art on attacks, defenses, and evaluation methods for AI agents.
Conclusion
This period combined theoretical progress with practical exploration. Reading the paper improved my understanding of common attacks against AI agents and the defenses discussed in the literature. In parallel, the voice prototype allowed me to test local speech and language tools while exposing the challenges of inferring emotion directly from the voice. The next step is to stabilize the prototype, evaluate its results more carefully, and clearly document its limitations.
Reference
Tamuka, N., Mathonsi, T. E., Otieno, O. T., Maswikaneng, S., Muchenje, T., & Tshilongamulenzhe, T. M. (2026). Securing LLM-based agents against cyberattacks: a comprehensive survey on attack techniques and defense strategies. Journal of Computer Virology and Hacking Techniques, 22, Article 38. https://doi.org/10.1007/s11416-026-00622-3

--------------------------------------------------------------------------------------
# 10.11.2026.  10 novembre 2026



# Research Progress Update: Literature Review and Local Voice Agent


---

## 1. Overview

My current work has two complementary parts:

1. **Literature review:** understanding the security risks, attack techniques, evaluation methods, and defense strategies of agentic AI systems (Part A).
2. **Practical development:** a local voice-processing prototype and two approaches to emotion analysis (Part B).

The literature review helps me understand the research landscape, while the prototype gives me hands-on experience with local inference, data processing, and integrating AI components.

---

# Part A: Literature Review

## 2. Summary of the literature update

Since the previous report, I have read **three additional articles** on the security of LLM-based agents. They complement each other:

- **Article 1** is a **survey** that maps the whole landscape of attacks and defenses against LLM-based agents.
- **Article 2** is an **experimental study** that measures how well specific defenses protect tool-using agents against indirect prompt injection, and what they cost in usefulness.
- **Article 3** is a **benchmark paper** (ASB) that tests attacks and defenses at every stage of an agent (user prompt, tools, memory, system prompt) and proposes a new backdoor attack.

Together, they extend my review from "which attacks exist" to "how do we know whether a defense really works", and from one attack surface (indirect prompt injection) to the full agent pipeline.

---

## 3. Articles read

### Article 1: Securing LLM-Based Agents Against Cyberattacks: A Comprehensive Survey on Attack Techniques and Defense Strategies

**Reference:** N. Tamuka et al., *Securing LLM-based agents against cyberattacks: a comprehensive survey on attack techniques and defense strategies*, Journal of Computer Virology and Hacking Techniques, 22, article 38, 2026. DOI: [10.1007/s11416-026-00622-3](https://doi.org/10.1007/s11416-026-00622-3)

**Main objective.** To give an overview of the cyberattacks targeting LLM-based agents and the defense strategies proposed against them, organized in a taxonomy.

**Approach.** The authors searched Web of Science and Scopus (2021 to 2026), reviewed existing studies, and organized them around an agent architecture of five layers (input, planning, model, memory, tools/actions). Attacks are grouped into five families (Figure 1 of the article):

1. Prompt injection and instruction hijacking
2. Information leakage
3. Malicious output and action induction (including tool misuse and SQL injection)
4. Resource exhaustion (denial of service)
5. Adversarial input transformations (encoding, rare languages, indirect prompts)

Defenses are grouped into five categories: input sanitization, adversarial training and alignment tuning, architectural safeguards (isolation, validation, least privilege), monitoring and guardrails, and watermarking/provenance verification.

**Main findings.**
- The security risks of an agent go beyond the language model: tools, retrieval, memory, and multi-agent communication all add attack opportunities.
- No single defense is enough; the authors recommend **defense in depth**, with architectural safeguards seen as the strongest protection against malicious actions.
- Persistent gaps: weak generalization of defenses against adaptive attackers, limited evaluation of agent-tool interaction risk, no standardized benchmarks covering all attack types, and little work on memory poisoning, multi-agent propagation, and multimodal inputs.

**Limitations (my analysis).** The search covers only two databases, the selection process is not quantified, some reference choices seem loosely matched to the claims they support, and the survey has no experiments of its own.

**Relevance to my research.** It helps structure my state of the art and identify research gaps. It guides the choice of specific threats and protections to study, especially prompt injection, information leakage, tool misuse, and agent reliability.

### Article 2: Evaluating Indirect Prompt Injection Defenses in Tool-Using LLM Agents: Security, Utility, and Replication

**Reference:** A. Khan, K. AlKhanbashi, and A. Mohamed, *Evaluating Indirect Prompt Injection Defenses in Tool-Using LLM Agents: Security, Utility, and Replication*, Computers, 15(9), 570, 2026. DOI: [10.3390/computers15090570](https://doi.org/10.3390/computers15090570)

**Main objective.** To measure how effective several defenses are against **indirect prompt injection** (IPI), where an agent reads untrusted content (a document, an email, a transaction record) that contains hidden instructions meant to steer its behavior. The question is not only "does the attack succeed?" but also "what does the defense cost the agent?".

**Approach.**
- Benchmark: **AgentDojo**, *banking* suite (16 legitimate tasks × 9 injection goals = 144 attack cases per run).
- Models: GPT-5.4, GPT-5.4-mini, Claude Sonnet 4.6.
- Configurations: no defense, **Spotlighting**, **Repeat User Prompt**, **Prompt Injection Detector**, and **Tool Filter** (OpenAI models only).
- Metrics: attack success rate (ASR), benign utility (BU), utility under attack (UUA), feasibility of attack goals, available actions, operational measures.
- Two independent replications per configuration, with Wilson confidence intervals and paired McNemar tests with Holm correction.

**Main findings.**
- Undefended raw ASR was 0/288 (GPT-5.4), 11/288 (GPT-5.4-mini) and 1/288 (Claude Sonnet 4.6). The authors warn that these differences are not a clean measure of robustness, because the attack goals were not equally reachable for every model.
- For GPT-5.4-mini, the Prompt Injection Detector and the Tool Filter gave the lowest ASR but also much lower benign utility (37.5% and 25.0%, versus 75.0% undefended). The Tool Filter works by restricting the available actions.
- The Prompt Injection Detector lowered benign utility for all three models.
- Lightweight prompt-based defenses kept utility higher but showed limited or uncertain security gains.
- No paired comparison on GPT-5.4-mini remained significant after Holm correction. Benign utility was more stable between runs than rare attack successes.

**Main message.** A defense should be judged on security **and** usefulness together, while taking into account whether the attack goal was feasible, which actions remain available, and how much results vary between runs.

**Limitations (as reported or deduced).** One benchmark domain, one attack family, very few successful attacks, only two replications, partly missing per-instance traces, and results specific to the tested models and defense implementations.

**Relevance to my research.** It shows why defenses must be evaluated by their effect on normal agent functionality as well as by attack prevention. It also connects directly to my previous reading of *AgentDojo*, since this study uses that benchmark.

### Article 3: Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents

**Reference:** H. Zhang, J. Huang, K. Mei, Y. Yao, Z. Wang, C. Zhan, H. Wang, and Y. Zhang, *Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents*, International Conference on Learning Representations (ICLR), 2025. arXiv: [2410.02644](https://arxiv.org/abs/2410.02644)

**Benchmark (GitHub):** [https://github.com/agiresearch/ASB](https://github.com/agiresearch/ASB). The repository contains the attack scripts (DPI, IPI, memory poisoning, PoT backdoor), the configuration files, and the simulated tools used in the paper's experiments.

**Main objective.** To provide a benchmark that evaluates attacks and defenses against LLM-based agents at **every operational step** of the agent. The authors argue that earlier benchmarks (InjecAgent, AgentDojo) test a single attack type (indirect prompt injection) or only a few scenarios.

**Approach.**
- The agent is attacked at four entry points: the **user prompt** (direct prompt injection, DPI), the **tool responses** (indirect prompt injection, IPI), the **memory** (memory poisoning), and the **system prompt** (a new Plan-of-Thought (PoT) backdoor attack). Attacks can also be combined (mixed attacks).
- The **PoT backdoor** hides a trigger-to-tool link in the demonstrations of the system prompt. It needs no model training: the agent learns it through in-context learning, and behaves normally when the trigger is absent.
- Benchmark content: 10 scenarios (e-commerce, finance, autonomous driving, medicine, and others), 10 agents, more than 400 tools, 400 attack tasks, 27 attack and defense methods, and 7 metrics. Tool calls are simulated for reproducibility.
- 13 LLM backbones (LLaMA3 and 3.1, Gemma2, Mixtral, Qwen2, GPT-3.5 Turbo, GPT-4o, GPT-4o-mini, Claude 3.5 Sonnet).
- Metrics: attack success rate (ASR), refusal rate (RR), performance under no attack (PNA), benign performance (BP), false negative and false positive rates (FNR, FPR) for detectors, and a new **Net Resilient Performance (NRP = PNA × (1 − ASR))** that combines utility and security.
- Eight distinct defenses: delimiters, instructional prevention, sandwich prevention, paraphrasing, dynamic prompt rewriting, shuffle, perplexity-based detection, and LLM-based detection.

**Main findings.**
- All attacks are effective. Average ASR: mixed attack **84.30%**, DPI 72.68%, PoT backdoor 42.12%, IPI 27.55%, memory poisoning 7.92%. Average refusal rates stay low (about 5.7%).
- More capable models are first **more vulnerable** (they follow instructions better, including malicious ones). Vulnerability falls only for the most advanced models, which refuse more often.
- Defenses are weak. On DPI (78.38% ASR without defense), paraphrasing gives 56.87% and dynamic prompt rewriting 44.45%, while delimiters and instructional prevention change almost nothing. On IPI (27.98% without defense), the best defense gains about 3 points. Detectors against memory poisoning miss about 66% of attacks (FNR 0.660).
- Defenses also slightly reduce normal performance (for example, −6.94 points on average for delimiters).
- The NRP ranks Claude 3.5 Sonnet first (43.56%), then LLaMA3-70B (30.03%) and GPT-4o (28.12%). Agent performance is generally below the underlying model's leaderboard quality, so choosing a backbone only from leaderboards is not enough.

**Limitations (as reported or deduced).** Tool calls are simulated, so a "successful attack" means the agent called the malicious tool, not that real damage occurred. The attacker is fixed and does not adapt to defenses. The attacker is assumed able to add its own tools to the agent's tool list. Memory poisoning is tested through direct prompt injection with a single model. The 2024 models and the benchmark do not cover MCP or multi-agent systems.

**Relevance to my research.** ASB gives a taxonomy of attack surfaces by agent stage, which I can reuse to classify other papers. It fills a gap identified in Article 1 (memory poisoning, no benchmark covering all attack types). Its NRP metric follows the same idea as Article 2 (security and utility must be reported together). It also extends my reading of *AgentDojo*, which covers only indirect prompt injection.

---


## 4. Comparison and contribution to the state of the art

| Aspect | Article 1: Comprehensive Survey | Article 2: Evaluating Defenses | Article 3: ASB |
|---|---|---|---|
| Main focus | Broad classification of attacks and defenses | Evaluation of indirect prompt injection defenses | Benchmark of attacks and defenses at every agent stage |
| Research approach | Literature review and taxonomy | Experimental evaluation on a benchmark (AgentDojo) | New benchmark with large-scale experiments (13 LLMs, 10 scenarios) |
| Main contribution | Organizes attack techniques, vulnerable components, and defense strategies | Shows why security, utility, feasibility, and replication must be reported together | Attack taxonomy by agent stage, PoT backdoor, NRP metric |
| Evidence | Synthesis of existing studies | Quantified results with statistics | Quantified results across many models (no confidence intervals reported) |
| Main limits | No own experiments, two databases, selection not quantified | One benchmark, one attack family, few attack events, two replications | Simulated tools, non-adaptive attacker, 2024 models, no MCP or multi-agent |
| Relevance to my work | Where threats and gaps lie, and which research directions to prioritize | How to evaluate the effectiveness and cost of a defense | A framework to classify attack surfaces and measure the security-utility trade-off |

**Cross-reading.** Article 1 calls for evaluations that measure security and utility together and that remain valid against adaptive attackers. Article 2 is a concrete example of such an evaluation, while also showing how hard it is to obtain solid conclusions (few attack successes, few replications). Article 3 widens the scope: it shows that the attack surface is not only the tool responses but also the user prompt, the memory, and the system prompt, and it finds that the defenses it tests protect little. Across the three articles, two points repeat: **no single defense suffices**, and **attack success rate alone is misleading**.

One point to check later: Article 2 observed very few successful attacks on recent models (GPT-5.4, Claude Sonnet 4.6), while ASB measured high success rates on 2024 models. The two studies use different benchmarks, tools, and attack designs, so they are not directly comparable, but the gap suggests that newer models or newer defenses may change the results.

---

## 5. Progress of the literature review

The review now covers:

- Security risks associated with agentic AI systems.
- Security challenges observed during agent deployment.
- Prompt injection attacks and their evaluation through AgentDojo.
- Indirect prompt injection defense evaluation and the security-utility trade-off.
- Broader cyberattack techniques and defense strategies for LLM-based agents.
- Attacks on every agent stage (user prompt, tools, memory, system prompt) and a benchmark that measures them together (ASB).

This reading gives me a clearer view of the security problems affecting LLM-based agents and of the methods used to evaluate and mitigate them.

---

# Part B: Practical Development, Local Voice Agent and Emotion Analysis

## 6. Reminder: what I did before (the local voice agent)

In the previous stage, I built and tested a **local voice-processing prototype** that records or loads audio, transcribes the speech, analyzes the text, and saves a report. Everything runs on my own machine.

```text
Audio file / Microphone -> Faster-Whisper (small) -> Transcription
                        -> Ollama + Qwen3:8B -> Text analysis -> *_analyse.txt
```

| Component | Role |
|---|---|
| Python 3.14.7 + `.venv` | Runs the program in a separate environment |
| `agent_vocal.py` | Main script: select or record audio, transcribe, request analysis, save report |
| `sounddevice` | Records speech through the microphone |
| Faster-Whisper (`small`) | Speech-to-text |
| Ollama + Qwen3:8B | Local language model that analyzes the transcription |

**What the prototype can do:**
- Load an existing audio file or record speech with the microphone.
- Transcribe the speech with Faster-Whisper.
- Send the transcription to Qwen3:8B through Ollama.
- Ask Qwen for the main topic, a summary, key ideas, questions and problems mentioned, and ambiguities to verify.
- Save the transcription and the analysis in a text file.

**What was already tested:**
- [x] Environment, main script, and code simplification.
- [x] Ollama and Qwen3:8B installed, with Python-to-Ollama communication tested.
- [x] Microphone recording and transcription.
- [x] Text reports generated (transcription + Qwen's analysis).
- [x] Pipeline run with **Wi-Fi off**: it worked locally once models and dependencies were installed.

Qwen receives the **transcription, not the audio**, so its result depends on transcription accuracy, the prompt, and the model's answer.

---

## 7. New in this stage: emotion analysis experiments

I explored two ways of detecting emotion.

### Experiment 1: from the words (Qwen)
I changed Qwen's prompts so it identifies possible emotions (joy, sadness, anger, fear, neutral), names the words that support its reading, says when evidence is insufficient, and does not claim to know the speaker's real state.

- **Advantage:** no extra model, only a prompt change, and it fits in the current report.
- **Limit:** it reads the meaning of the words, not the voice (no tone, pitch, or speaking rate). It is **text-based emotion interpretation**, not vocal emotion recognition.

### Experiment 2: from the audio (emotion2vec+ base)
Tested with **FunASR 1.4.16** in a separate environment. It analyzes the audio signal directly, without transcription.

- **Short recordings:** it returned emotion categories with scores. One result gave about **99.98% `sad`** while I was just speaking softly. One recording cannot show whether the model was wrong or why, but it shows that a high score is not proof of a person's real emotional state. More tests are needed.
- **Long recording (about 32 min):** the analysis failed with a memory requirement **above 100 GB**, against my 8 GB of VRAM. The source is not confirmed; it may depend on how the audio is loaded or processed, so it does not mean the model always needs that much.
- **Splitting into smaller segments** did not solve the problem in my setup.

This experiment is still **separate** from `agent_vocal.py`.
So I am now looking for other tools that can analyze emotion directly from the voice, without going through the transcription.

---

## 8. Limitations

- The pipeline follows fixed steps and does not choose its own tools yet.
- Emotion results are not reliable enough yet: neither approach can determine a person's real emotional state with certainty.
- The direct voice analysis is not integrated in the main pipeline

## 9. Next steps

**Literature review**
1. Compare all reviewed papers systematically (attack types, defenses, benchmarks, metrics, limitations).
2. Identify research gaps relevant to my doctoral topic.
3. Pay particular attention to the relationship between agent autonomy, tool use, prompt injection, data protection, and the reliability of security defenses.
4. Move from understanding the literature toward a more precise research question and a possible contribution to the security of agentic AI systems.
5. Continue my literature review, with a focus on memory poisoning (the lowest-scoring attack in ASB, and a gap named in Article 1) and on defenses that hold against adaptive attackers.

**Local voice agent**

1. Evaluate other tools for emotion analysis directly from the voice, and test them on several recordings.
2. Keep Qwen's text-based reading as an alternative, separating textual evidence from acoustic evidence.

## 10. Conclusion

On the theory side, the literature review now provides a good foundation on agent security and on how defenses are evaluated, drawing on a survey of attacks and defenses, an experimental study of indirect prompt injection defenses, and a benchmark that tests attacks at every stage of an agent. The three readings agree that agents are vulnerable at several points, that current defenses protect only partly, and that security must be measured together with usefulness. On the practical side, the main pipeline built earlier works locally, including offline. At this stage, Qwen’s text-based emotion reading is already usable, while emotion detection directly from the voice still needs to be reviewed before deciding whether it can be integrated as it is or requires a different approach.

---

## References

[1] N. Tamuka et al., "Securing LLM-based agents against cyberattacks: a comprehensive survey on attack techniques and defense strategies," *Journal of Computer Virology and Hacking Techniques*, vol. 22, article 38, 2026. DOI: [10.1007/s11416-026-00622-3](https://doi.org/10.1007/s11416-026-00622-3)

[2] A. Khan, K. AlKhanbashi, and A. Mohamed, "Evaluating Indirect Prompt Injection Defenses in Tool-Using LLM Agents: Security, Utility, and Replication," *Computers*, vol. 15, no. 9, article 570, 2026. DOI: [10.3390/computers15090570](https://doi.org/10.3390/computers15090570)

[3] H. Zhang, J. Huang, K. Mei, Y. Yao, Z. Wang, C. Zhan, H. Wang, and Y. Zhang, "Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents," in *Proc. International Conference on Learning Representations (ICLR)*, 2025. arXiv: [2410.02644](https://arxiv.org/abs/2410.02644). Code: [https://github.com/agiresearch/ASB](https://github.com/agiresearch/ASB)
