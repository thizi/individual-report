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
----------------------------------------------------------------------

# 10.11.2026 # VERSION FRANCAIS

# Rapport d'avancement : revue de littérature et agent vocal local


---

## 1. Vue d'ensemble

Mon travail actuel comporte deux parties complémentaires :

1. **Revue de littérature :** comprendre les risques de sécurité, les techniques d'attaque, les méthodes d'évaluation et les stratégies de défense des systèmes d'IA agentique (Partie A).
2. **Développement pratique :** un prototype local de traitement de la voix et deux approches d'analyse des émotions (Partie B).

La revue de littérature m'aide à comprendre l'état de la recherche, tandis que le prototype me donne une expérience concrète de l'inférence locale, du traitement des données et de l'intégration de composants d'IA.

---

# Partie A : Revue de littérature

## 2. Résumé de la mise à jour de la littérature

Depuis le dernier rapport, j'ai lu **trois articles supplémentaires** sur la sécurité des agents basés sur des LLM. Ils se complètent :

- **L'article 1** est un **état de l'art (survey)** qui cartographie l'ensemble des attaques et des défenses contre les agents basés sur des LLM.
- **L'article 2** est une **étude expérimentale** qui mesure dans quelle mesure des défenses précises protègent les agents utilisant des outils contre l'injection de prompt indirecte, et ce qu'elles coûtent en utilité.
- **L'article 3** est un **article de benchmark** (ASB) qui teste les attaques et les défenses à chaque étape d'un agent (prompt utilisateur, outils, mémoire, prompt système) et propose une nouvelle attaque de type backdoor.

Ensemble, ils font passer ma revue de « quelles attaques existent » à « comment savoir si une défense fonctionne vraiment », et d'une seule surface d'attaque (l'injection de prompt indirecte) à l'ensemble de la chaîne de l'agent.

---

## 3. Articles lus

### Article 1 : Securing LLM-Based Agents Against Cyberattacks: A Comprehensive Survey on Attack Techniques and Defense Strategies

**Référence :** N. Tamuka et al., *Securing LLM-based agents against cyberattacks: a comprehensive survey on attack techniques and defense strategies*, Journal of Computer Virology and Hacking Techniques, 22, article 38, 2026. DOI : [10.1007/s11416-026-00622-3](https://doi.org/10.1007/s11416-026-00622-3)

**Objectif principal.** Donner un aperçu des cyberattaques visant les agents basés sur des LLM et des stratégies de défense proposées contre elles, organisées dans une taxonomie.

**Approche.** Les auteurs ont cherché dans Web of Science et Scopus (2021 à 2026), examiné les études existantes et les ont organisées autour d'une architecture d'agent à cinq couches (entrée, planification, modèle, mémoire, outils/actions). Les attaques sont regroupées en cinq familles (Figure 1 de l'article) :

1. Injection de prompt et détournement d'instructions
2. Fuite d'information
3. Induction de sorties et d'actions malveillantes (y compris le mauvais usage d'outils et l'injection SQL)
4. Épuisement des ressources (déni de service)
5. Transformations adversariales des entrées (encodage, langues rares, prompts indirects)

Les défenses sont regroupées en cinq catégories : nettoyage des entrées, entraînement adversarial et alignement, protections d'architecture (isolation, validation, moindre privilège), surveillance et garde-fous, et filigrane/vérification de provenance.

**Principaux résultats.**
- Les risques de sécurité d'un agent dépassent le modèle de langage : les outils, la récupération d'information, la mémoire et la communication multi-agents ajoutent chacun des possibilités d'attaque.
- Aucune défense ne suffit seule ; les auteurs recommandent la **défense en profondeur**, les protections d'architecture étant considérées comme la plus forte protection contre les actions malveillantes.
- Lacunes persistantes : faible généralisation des défenses face à des attaquants adaptatifs, évaluation limitée du risque lié à l'interaction agent-outil, absence de benchmarks standardisés couvrant tous les types d'attaques, et peu de travaux sur l'empoisonnement de mémoire, la propagation multi-agents et les entrées multimodales.

**Limites (mon analyse).** La recherche ne couvre que deux bases de données, le processus de sélection n'est pas quantifié, certains choix de références semblent faiblement liés aux affirmations qu'ils soutiennent, et le survey n'a pas d'expériences propres.

**Pertinence pour ma recherche.** Il m'aide à structurer mon état de l'art et à identifier des lacunes de recherche. Il guide le choix des menaces et des protections à étudier, en particulier l'injection de prompt, la fuite d'information, le mauvais usage d'outils et la fiabilité des agents.

### Article 2 : Evaluating Indirect Prompt Injection Defenses in Tool-Using LLM Agents: Security, Utility, and Replication

**Référence :** A. Khan, K. AlKhanbashi et A. Mohamed, *Evaluating Indirect Prompt Injection Defenses in Tool-Using LLM Agents: Security, Utility, and Replication*, Computers, 15(9), 570, 2026. DOI : [10.3390/computers15090570](https://doi.org/10.3390/computers15090570)

**Objectif principal.** Mesurer l'efficacité de plusieurs défenses contre l'**injection de prompt indirecte** (IPI), où un agent lit un contenu non fiable (un document, un e-mail, un enregistrement de transaction) qui contient des instructions cachées destinées à orienter son comportement. La question n'est pas seulement « l'attaque réussit-elle ? » mais aussi « que coûte la défense à l'agent ? ».

**Approche.**
- Benchmark : **AgentDojo**, suite *banking* (16 tâches légitimes × 9 objectifs d'injection = 144 cas d'attaque par exécution).
- Modèles : GPT-5.4, GPT-5.4-mini, Claude Sonnet 4.6.
- Configurations : aucune défense, **Spotlighting**, **Repeat User Prompt**, **Prompt Injection Detector** et **Tool Filter** (modèles OpenAI uniquement).
- Métriques : taux de réussite des attaques (ASR), utilité bénigne (BU), utilité sous attaque (UUA), faisabilité des objectifs d'attaque, actions disponibles, mesures opérationnelles.
- Deux réplications indépendantes par configuration, avec des intervalles de confiance de Wilson et des tests de McNemar appariés avec correction de Holm.

**Principaux résultats.**
- L'ASR brut sans défense était de 0/288 (GPT-5.4), 11/288 (GPT-5.4-mini) et 1/288 (Claude Sonnet 4.6). Les auteurs avertissent que ces différences ne mesurent pas proprement la robustesse, car les objectifs d'attaque n'étaient pas également atteignables pour tous les modèles.
- Pour GPT-5.4-mini, le Prompt Injection Detector et le Tool Filter ont donné l'ASR le plus bas, mais aussi une utilité bénigne bien plus faible (37,5 % et 25,0 %, contre 75,0 % sans défense). Le Tool Filter fonctionne en restreignant les actions disponibles.
- Le Prompt Injection Detector a réduit l'utilité bénigne pour les trois modèles.
- Les défenses légères basées sur le prompt ont conservé une meilleure utilité mais ont montré des gains de sécurité limités ou incertains.
- Aucune comparaison appariée sur GPT-5.4-mini n'est restée significative après la correction de Holm. L'utilité bénigne était plus stable d'une exécution à l'autre que les rares succès d'attaque.

**Message principal.** Une défense doit être jugée sur la sécurité **et** l'utilité ensemble, en tenant compte de la faisabilité de l'objectif d'attaque, des actions qui restent disponibles et de la variabilité des résultats entre exécutions.

**Limites (rapportées ou déduites).** Un seul domaine de benchmark, une seule famille d'attaques, très peu d'attaques réussies, seulement deux réplications, traces par instance partiellement manquantes, et résultats propres aux modèles et aux implémentations de défense testés.

**Pertinence pour ma recherche.** Il montre pourquoi les défenses doivent être évaluées par leur effet sur le fonctionnement normal de l'agent autant que par la prévention des attaques. Il se relie aussi directement à ma lecture précédente d'*AgentDojo*, puisque cette étude utilise ce benchmark.

### Article 3 : Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents

**Référence :** H. Zhang, J. Huang, K. Mei, Y. Yao, Z. Wang, C. Zhan, H. Wang et Y. Zhang, *Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents*, International Conference on Learning Representations (ICLR), 2025. arXiv : [2410.02644](https://arxiv.org/abs/2410.02644)

**Benchmark (GitHub) :** [https://github.com/agiresearch/ASB](https://github.com/agiresearch/ASB). Le dépôt contient les scripts d'attaque (DPI, IPI, empoisonnement de mémoire, backdoor PoT), les fichiers de configuration et les outils simulés utilisés dans les expériences de l'article.

**Objectif principal.** Fournir un benchmark qui évalue les attaques et les défenses contre les agents basés sur des LLM à **chaque étape de fonctionnement** de l'agent. Les auteurs soutiennent que les benchmarks précédents (InjecAgent, AgentDojo) testent un seul type d'attaque (l'injection de prompt indirecte) ou seulement quelques scénarios.

**Approche.**
- L'agent est attaqué à quatre points d'entrée : le **prompt utilisateur** (injection de prompt directe, DPI), les **réponses des outils** (injection de prompt indirecte, IPI), la **mémoire** (empoisonnement de mémoire) et le **prompt système** (une nouvelle attaque backdoor Plan-of-Thought (PoT)). Les attaques peuvent aussi être combinées (attaques mixtes).
- La **backdoor PoT** cache un lien entre un déclencheur et un outil dans les démonstrations du prompt système. Elle ne demande aucun entraînement du modèle : l'agent l'apprend par apprentissage en contexte, et se comporte normalement quand le déclencheur est absent.
- Contenu du benchmark : 10 scénarios (e-commerce, finance, conduite autonome, médecine, entre autres), 10 agents, plus de 400 outils, 400 tâches d'attaque, 27 méthodes d'attaque et de défense, et 7 métriques. Les appels d'outils sont simulés pour garantir la reproductibilité.
- 13 LLM de base (LLaMA3 et 3.1, Gemma2, Mixtral, Qwen2, GPT-3.5 Turbo, GPT-4o, GPT-4o-mini, Claude 3.5 Sonnet).
- Métriques : taux de réussite des attaques (ASR), taux de refus (RR), performance sans attaque (PNA), performance bénigne (BP), taux de faux négatifs et de faux positifs (FNR, FPR) pour les détecteurs, et une nouvelle métrique, la **Net Resilient Performance (NRP = PNA × (1 − ASR))**, qui combine utilité et sécurité.
- Huit défenses distinctes : délimiteurs, prévention par instruction, prévention sandwich, paraphrase, réécriture dynamique du prompt, mélange (shuffle), détection par perplexité et détection par LLM.

**Principaux résultats.**
- Toutes les attaques sont efficaces. ASR moyen : attaque mixte **84,30 %**, DPI 72,68 %, backdoor PoT 42,12 %, IPI 27,55 %, empoisonnement de mémoire 7,92 %. Les taux de refus moyens restent faibles (environ 5,7 %).
- Les modèles plus capables sont d'abord **plus vulnérables** (ils suivent mieux les instructions, y compris les malveillantes). La vulnérabilité ne baisse que pour les modèles les plus avancés, qui refusent plus souvent.
- Les défenses sont faibles. Sur la DPI (78,38 % d'ASR sans défense), la paraphrase donne 56,87 % et la réécriture dynamique 44,45 %, tandis que les délimiteurs et la prévention par instruction ne changent presque rien. Sur l'IPI (27,98 % sans défense), la meilleure défense gagne environ 3 points. Les détecteurs contre l'empoisonnement de mémoire ratent environ 66 % des attaques (FNR 0,660).
- Les défenses réduisent aussi légèrement la performance normale (par exemple −6,94 points en moyenne pour les délimiteurs).
- La NRP classe Claude 3.5 Sonnet en premier (43,56 %), puis LLaMA3-70B (30,03 %) et GPT-4o (28,12 %). La performance d'un agent est généralement inférieure à la qualité du modèle sous-jacent sur les classements, donc choisir un modèle uniquement d'après les classements ne suffit pas.

**Limites (rapportées ou déduites).** Les appels d'outils sont simulés, donc une « attaque réussie » signifie que l'agent a appelé l'outil malveillant, pas qu'un dommage réel a eu lieu. L'attaquant est fixe et ne s'adapte pas aux défenses. On suppose que l'attaquant peut ajouter ses propres outils à la liste d'outils de l'agent. L'empoisonnement de mémoire est testé par injection de prompt directe avec un seul modèle. Les modèles de 2024 et le benchmark ne couvrent ni MCP ni les systèmes multi-agents.

**Pertinence pour ma recherche.** ASB propose une taxonomie des surfaces d'attaque par étape de l'agent, que je peux réutiliser pour classer d'autres articles. Il comble une lacune identifiée dans l'article 1 (empoisonnement de mémoire, absence de benchmark couvrant tous les types d'attaques). Sa métrique NRP suit la même idée que l'article 2 (la sécurité et l'utilité doivent être rapportées ensemble). Il étend aussi ma lecture d'*AgentDojo*, qui ne couvre que l'injection de prompt indirecte.

---


## 4. Comparaison et contribution à l'état de l'art

| Aspect | Article 1 : survey complet | Article 2 : évaluation de défenses | Article 3 : ASB |
|---|---|---|---|
| Axe principal | Classification large des attaques et des défenses | Évaluation des défenses contre l'injection de prompt indirecte | Benchmark des attaques et des défenses à chaque étape de l'agent |
| Approche de recherche | Revue de littérature et taxonomie | Évaluation expérimentale sur un benchmark (AgentDojo) | Nouveau benchmark avec expériences à grande échelle (13 LLM, 10 scénarios) |
| Contribution principale | Organise les techniques d'attaque, les composants vulnérables et les stratégies de défense | Montre pourquoi la sécurité, l'utilité, la faisabilité et la réplication doivent être rapportées ensemble | Taxonomie des attaques par étape de l'agent, backdoor PoT, métrique NRP |
| Preuves | Synthèse d'études existantes | Résultats chiffrés avec statistiques | Résultats chiffrés sur de nombreux modèles (sans intervalles de confiance rapportés) |
| Limites principales | Pas d'expériences propres, deux bases de données, sélection non quantifiée | Un seul benchmark, une seule famille d'attaques, peu d'attaques réussies, deux réplications | Outils simulés, attaquant non adaptatif, modèles de 2024, ni MCP ni multi-agents |
| Pertinence pour mon travail | Où se situent les menaces et les lacunes, et quelles directions de recherche prioriser | Comment évaluer l'efficacité et le coût d'une défense | Un cadre pour classer les surfaces d'attaque et mesurer le compromis sécurité-utilité |

**Lecture croisée.** L'article 1 appelle des évaluations qui mesurent ensemble la sécurité et l'utilité et qui restent valides face à des attaquants adaptatifs. L'article 2 est un exemple concret d'une telle évaluation, tout en montrant combien il est difficile d'obtenir des conclusions solides (peu de succès d'attaque, peu de réplications). L'article 3 élargit le champ : il montre que la surface d'attaque n'est pas seulement les réponses des outils mais aussi le prompt utilisateur, la mémoire et le prompt système, et il constate que les défenses qu'il teste protègent peu. Dans les trois articles, deux points reviennent : **aucune défense ne suffit seule**, et **le taux de réussite des attaques seul est trompeur**.

Un point à vérifier plus tard : l'article 2 a observé très peu d'attaques réussies sur des modèles récents (GPT-5.4, Claude Sonnet 4.6), alors qu'ASB a mesuré des taux de réussite élevés sur des modèles de 2024. Les deux études utilisent des benchmarks, des outils et des conceptions d'attaque différents, donc elles ne sont pas directement comparables, mais l'écart suggère que des modèles ou des défenses plus récents pourraient changer les résultats.

---

## 5. Avancement de la revue de littérature

La revue couvre maintenant :

- Les risques de sécurité associés aux systèmes d'IA agentique.
- Les défis de sécurité observés lors du déploiement d'agents.
- Les attaques par injection de prompt et leur évaluation via AgentDojo.
- L'évaluation des défenses contre l'injection de prompt indirecte et le compromis sécurité-utilité.
- Les techniques de cyberattaque plus larges et les stratégies de défense pour les agents basés sur des LLM.
- Les attaques sur chaque étape de l'agent (prompt utilisateur, outils, mémoire, prompt système) et un benchmark qui les mesure ensemble (ASB).

Cette lecture me donne une vision plus claire des problèmes de sécurité qui touchent les agents basés sur des LLM et des méthodes utilisées pour les évaluer et les atténuer.

---

# Partie B : Développement pratique, agent vocal local et analyse des émotions

## 6. Rappel : ce que j'ai fait avant (l'agent vocal local)

À l'étape précédente, j'ai construit et testé un **prototype local de traitement de la voix** qui enregistre ou charge un audio, transcrit la parole, analyse le texte et sauvegarde un rapport. Tout fonctionne sur ma propre machine.

```text
Fichier audio / Microphone -> Faster-Whisper (small) -> Transcription
                           -> Ollama + Qwen3:8B -> Analyse du texte -> *_analyse.txt
```

| Composant | Rôle |
|---|---|
| Python 3.14.7 + `.venv` | Exécute le programme dans un environnement séparé |
| `agent_vocal.py` | Script principal : choisir ou enregistrer un audio, transcrire, demander l'analyse, sauvegarder le rapport |
| `sounddevice` | Enregistre la parole via le microphone |
| Faster-Whisper (`small`) | Transcription de la parole en texte |
| Ollama + Qwen3:8B | Modèle de langage local qui analyse la transcription |

**Ce que le prototype sait faire :**
- Charger un fichier audio existant ou enregistrer la parole avec le microphone.
- Transcrire la parole avec Faster-Whisper.
- Envoyer la transcription à Qwen3:8B via Ollama.
- Demander à Qwen le sujet principal, un résumé, les idées clés, les questions et problèmes mentionnés, et les ambiguïtés à vérifier.
- Sauvegarder la transcription et l'analyse dans un fichier texte.

**Ce qui était déjà testé :**
- [x] Environnement, script principal et simplification du code.
- [x] Ollama et Qwen3:8B installés, communication Python-Ollama testée.
- [x] Enregistrement au microphone et transcription.
- [x] Rapports texte générés (transcription + analyse de Qwen).
- [x] Pipeline exécuté avec le **Wi-Fi coupé** : il a fonctionné en local une fois les modèles et dépendances installés.

Qwen reçoit la **transcription, pas l'audio**, donc son résultat dépend de la précision de la transcription, du prompt et de la réponse du modèle.

---

## 7. Nouveau à cette étape : expériences d'analyse des émotions

J'ai exploré deux façons de détecter l'émotion.

### Expérience 1 : à partir des mots (Qwen)
J'ai modifié les prompts de Qwen pour qu'il identifie les émotions possibles (joie, tristesse, colère, peur, neutre), nomme les mots qui soutiennent sa lecture, dise quand les preuves sont insuffisantes et ne prétende pas connaître l'état réel du locuteur.

- **Avantage :** aucun modèle supplémentaire, seulement un changement de prompt, et cela s'intègre dans le rapport actuel.
- **Limite :** il lit le sens des mots, pas la voix (ni ton, ni hauteur, ni débit). C'est une **interprétation de l'émotion basée sur le texte**, pas une reconnaissance vocale de l'émotion.

### Expérience 2 : à partir de l'audio (emotion2vec+ base)
Testé avec **FunASR 1.4.16** dans un environnement séparé. Il analyse directement le signal audio, sans transcription.

- **Enregistrements courts :** il a renvoyé des catégories d'émotion avec des scores. Un résultat a donné environ **99,98 % `sad`** alors que je parlais simplement doucement. Un seul enregistrement ne permet pas de dire si le modèle s'est trompé ni pourquoi, mais cela montre qu'un score élevé n'est pas une preuve de l'état émotionnel réel d'une personne. D'autres tests sont nécessaires.
- **Long enregistrement (environ 16 min) :** l'analyse a échoué avec un besoin en mémoire **supérieur à 100 Go**, contre mes 8 Go de VRAM. La cause n'est pas confirmée ; elle peut dépendre de la façon dont l'audio est chargé ou traité, donc cela ne signifie pas que le modèle a toujours besoin d'autant.
- **Le découpage en segments plus petits** n'a pas résolu le problème dans ma configuration.

Cette expérience reste **séparée** de `agent_vocal.py`.
Je cherche donc maintenant d'autres outils capables d'analyser l'émotion directement depuis la voix, sans passer par la transcription.

---

## 8. Limites

- Le pipeline suit des étapes fixes et ne choisit pas encore ses propres outils.
- Les résultats d'émotion ne sont pas encore assez fiables : aucune des deux approches ne peut déterminer avec certitude l'état émotionnel réel d'une personne.
- L'analyse vocale directe n'est pas intégrée dans le pipeline principal.

## 9. Prochaines étapes

**Revue de littérature**
1. Comparer systématiquement tous les articles lus (types d'attaques, défenses, benchmarks, métriques, limites).
2. Identifier les lacunes de recherche pertinentes pour mon sujet de doctorat.
3. Porter une attention particulière à la relation entre l'autonomie des agents, l'usage d'outils, l'injection de prompt, la protection des données et la fiabilité des défenses de sécurité.
4. Passer de la compréhension de la littérature à une question de recherche plus précise et à une contribution possible à la sécurité des systèmes d'IA agentique.
5. Poursuivre ma revue de littérature, en me concentrant sur l'empoisonnement de mémoire (l'attaque la moins efficace dans ASB, et une lacune citée dans l'article 1) et sur les défenses qui tiennent face à des attaquants adaptatifs.

**Agent vocal local**

1. Évaluer d'autres outils d'analyse des émotions directement depuis la voix, et les tester sur plusieurs enregistrements.
2. Garder la lecture de Qwen basée sur le texte comme alternative, en séparant les preuves textuelles des preuves acoustiques.

## 10. Conclusion

Côté théorie, la revue de littérature fournit désormais une bonne base sur la sécurité des agents et sur la façon d'évaluer les défenses, en s'appuyant sur un survey des attaques et défenses, une étude expérimentale des défenses contre l'injection de prompt indirecte, et un benchmark qui teste les attaques à chaque étape d'un agent. Les trois lectures s'accordent sur le fait que les agents sont vulnérables en plusieurs points, que les défenses actuelles ne protègent que partiellement, et que la sécurité doit être mesurée avec l'utilité. Côté pratique, le pipeline principal construit précédemment fonctionne en local, y compris hors ligne. À ce stade, la lecture des émotions par Qwen à partir du texte est déjà utilisable, tandis que la détection d'émotion directement depuis la voix doit encore être revue avant de décider si elle peut être intégrée telle quelle ou si elle demande une approche différente.

---

## Références

[1] N. Tamuka et al., « Securing LLM-based agents against cyberattacks: a comprehensive survey on attack techniques and defense strategies », *Journal of Computer Virology and Hacking Techniques*, vol. 22, article 38, 2026. DOI : [10.1007/s11416-026-00622-3](https://doi.org/10.1007/s11416-026-00622-3)

[2] A. Khan, K. AlKhanbashi et A. Mohamed, « Evaluating Indirect Prompt Injection Defenses in Tool-Using LLM Agents: Security, Utility, and Replication », *Computers*, vol. 15, no. 9, article 570, 2026. DOI : [10.3390/computers15090570](https://doi.org/10.3390/computers15090570)

[3] H. Zhang, J. Huang, K. Mei, Y. Yao, Z. Wang, C. Zhan, H. Wang et Y. Zhang, « Agent Security Bench (ASB): Formalizing and Benchmarking Attacks and Defenses in LLM-based Agents », dans *Proc. International Conference on Learning Representations (ICLR)*, 2025. arXiv : [2410.02644](https://arxiv.org/abs/2410.02644). Code : [https://github.com/agiresearch/ASB](https://github.com/agiresearch/ASB)
--------------------------------------------------------------------------------------
# 10.11.2026.  10 novembre 2026 ENGLISH VERSION



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

--------------------------------------------------------------------------------------------------------------------

# État de l'art : LLM audio de bout en bout (SpeechLLM et MERaLiON)

# **Date : 24.11.2026 **

Au cours de ces deux dernières semaines, j'ai lu deux articles relatifs au multimodal et aux agents IA. Voici l'état de l'art qui en résulte.


**Contexte :** dans le cadre de l'état de l'art et de l'avancement de mes lectures, j'ai lu deux articles liés aux agents IA multimodaux (voix + texte). Ce rapport résume chaque article, les compare, puis explique ce que j'en retiens pour mon agent audio, qui doit fonctionner en local.

---

## Article 1 : SpeechLLM (SENSE-ASR)

### Référence

- **Titre :** SpeechLLM: Unified Speech and Language Model for Enhanced Multi-Task Understanding in Low Resource Settings
- **Auteurs :** Jaekwon Yoo, Kunal Chandiramani, Divya Tadimeti, Abenezer Girma, Chandra Dhir (JPMorganChase et Columbia University)
- **Publication :** arXiv:2509.04473, cs.CL, 29 août 2025
- **Lien :** https://arxiv.org/abs/2509.04473
- **Benchmark utilisé :** SLUE (Spoken Language Understanding Evaluation), avec les jeux SLUE-VoxPopuli (reconnaissance d'entités) et SLUE-VoxCeleb (sentiment)
- Article du benchmark : https://arxiv.org/abs/2111.10367
- Code et classement : https://github.com/asappresearch/slue-toolkit

### Introduction : ce que les auteurs ont fait

Relier un encodeur de parole à un grand modèle de langage (LLM) demande beaucoup de données et de ressources. Les auteurs proposent SENSE-ASR, un système de bout en bout qui fait trois tâches en une seule passe : la transcription (ASR), la reconnaissance d'entités nommées (NER : personnes, lieux, dates) et l'analyse de sentiment (SA : positif, négatif, neutre). Leur idée est de ne rien réentraîner de lourd : seul un petit adaptateur est entraîné. Pour compenser le manque de données annotées, un LLM (GPT-4o) annote automatiquement 960 heures de LibriSpeech avec des entités.

### Architecture

- **Encodeur de parole :** Whisper (variantes small et medium), gelé. La voix devient une suite de vecteurs.
- **Adaptateur (la contribution principale) :** un *adaptive average pooling* réduit 1500 vecteurs à 250, une normalisation stabilise les valeurs, puis une projection linéaire adapte la taille à celle du LLM. Environ 1,6 à 2,1 millions de paramètres entraînables.
- **LLM :** TinyLlama (petit modèle entraîné sur 3 000 milliards de tokens), gelé (ou légèrement affiné avec LoRA en fin de parcours).
- **Classifieur régularisateur :** un petit réseau utilisé uniquement pendant l'entraînement. Il essaie de deviner les entités ou le sentiment à partir de la sortie de l'adaptateur, ce qui force celui-ci à bien conserver ces informations. Il est retiré à l'inférence.

### Entraînement

Trois étapes, du général au spécifique :

1. Pré-entraînement sur LibriSpeech (960 h de livres lus) pour apprendre à transcrire.
2. Poursuite sur LibriSpeech annoté automatiquement par GPT-4o (entités), pour apprendre aussi à repérer les entités.
3. Ajustement fin sur les données annotées par des humains : SLUE-VoxPopuli (environ 15 h, discours du Parlement européen) pour les entités, SLUE-VoxCeleb (environ 12,8 h, interviews) pour le sentiment.

Des augmentations de données (changement de vitesse, SpecAugment) sont appliquées.

### Résultats

- **Transcription (LibriSpeech, Whisper medium) :** taux d'erreur de mots de 3,67 % sur test-clean contre 5,01 % pour la méthode de référence SLAM-ASR, soit environ 26 % d'amélioration relative, avec 2,1 M de paramètres entraînables contre 15,2 M.
- **Entités (VoxPopuli) :** le score F1 passe de 62,0 (sans préparation) à 64,3 (LibriSpeech), 65,0 (annotations GPT-4o), 65,8 (classifieur), puis 68,9 (LoRA).
- **Sentiment (VoxCeleb) :** le score F1 passe de 58,9 à 61,0 (LibriSpeech), 63,6 (classifieur), puis 65,9 (LoRA), contre 48,1 à 49,8 pour les références E2E du benchmark.
- **Score global SLUE :** 74,6 contre 68,1 pour le meilleur système E2E de référence (environ 9,5 % d'amélioration relative), proche du système en cascade (75,7).

### Conclusion des auteurs

Un adaptateur très léger, associé à un entraînement en plusieurs étapes qui utilise des annotations synthétiques, suffit à donner à un LLM de bonnes capacités de compréhension de la parole, avec peu de paramètres entraînables et peu d'annotations manuelles.

### Limites (mon analyse)

1. **Tâches et langue restreintes :** seulement transcription, entités et sentiment en trois classes, sur de l'anglais. Pas d'émotions fines (stress, tristesse).
2. **Peu de données humaines et des incohérences de chiffres :** 15 h pour les entités ; certains chiffres diffèrent entre le texte et les tableaux (par exemple 74,3 et 74,6 pour le même score).
3. **Dépendance à un LLM externe pour annoter :** GPT-4o est utilisé pour la préparation des données, ce qui pose un problème si les données sont sensibles et doivent rester en local.

---

## Article 2 : MERaLiON-AudioLLM

### Référence

- **Titre :** MERaLiON-AudioLLM: Bridging Audio and Language with Large Language Models
- **Auteurs :** MERaLiON Team : Yingxu He, Zhuohan Liu, Shuo Sun, Bin Wang, Wenyu Zhang, Xunlong Zou, Nancy F. Chen, Ai Ti Aw (Institute for Infocomm Research, A*STAR, Singapour)
- **Publication :** arXiv:2412.09818, cs.CL, version 3 du 16 janvier 2025
- **Lien :** https://arxiv.org/abs/2412.09818
- **Modèle :** https://huggingface.co/MERaLiON/MERaLiON-AudioLLM-Whisper-SEA-LION
- **Benchmark utilisé :** AudioBench (Wang et al., 2024), avec plusieurs jeux de données de reconnaissance vocale, traduction, questions-réponses, résumé de dialogues, instructions vocales et paralinguistique.
- Article du benchmark : https://arxiv.org/abs/2406.16020
- Code et classement : https://github.com/AudioLLMs/AudioBench

### Introduction : ce que les auteurs ont fait

L'équipe a construit le premier modèle voix-texte conçu pour le contexte multilingue et multiculturel de Singapour (anglais, chinois, malais, tamoul et Singlish). Les systèmes classiques de reconnaissance vocale se trompent souvent avec les accents, les dialectes et les mélanges de langues. Le modèle prend en entrée un couple (audio, consigne écrite) et répond par du texte. Il fait plusieurs tâches : transcription, traduction, questions-réponses sur audio, résumé de conversations, suivi d'instructions vocales et reconnaissance d'informations paralinguistiques (genre, accent, émotion).

### Architecture

- **Encodeur audio :** MERaLiON-Whisper, basé sur l'encodeur de Whisper-large-v2 et réentraîné sur des données locales (1500 vecteurs de dimension 1280 en sortie).
- **Adaptateur :** un perceptron multicouche simple appelé MLP-100. Il regroupe les vecteurs par paquets de 15 et produit 100 vecteurs, à la taille attendue par le LLM.
- **Décodeur de texte :** SEA-LION V3, un LLM local construit à partir de Gemma 2 (9 milliards de paramètres) et poursuivi sur 200 milliards de tokens dans les langues de Singapour et d'Asie du Sud-Est.
- Les vecteurs audio et la consigne tokenisée sont concaténés, puis le LLM génère la réponse.

### Entraînement

1. **Réentraînement de l'encodeur** sur des données de reconnaissance vocale locales nettoyées (corpus national IMDA, données internes et publiques).
2. **Affinage multimodal par instructions** sur 260 000 heures de paires voix-texte, dont une grande partie vient du National Speech Corpus (environ 10 600 h d'anglais de Singapour), complétées par des données synthétiques (résumé de dialogues, questions-réponses, genre).
3. L'encodeur et l'adaptateur sont entièrement réentraînés ; le LLM est partiellement affiné avec LoRA (rang 8). Entraînement : environ 200 000 étapes, 2 jours sur 128 GPU H100, avec augmentation de spectrogrammes.

### Résultats

L'évaluation utilise AudioBench, avec comparaison à Qwen2-Audio 7B, WavLLM, SALMONN et à un système en cascade.

- **Reconnaissance vocale locale :** sur la partie 2 du corpus national de Singapour (lectures avec noms de personnes, plats, lieux, marques locales), le taux d'erreur de mots est de 5 %, contre 19 % pour Qwen2-Audio et 33 % pour Whisper-large-v2.
- **Données jamais vues (Earnings21 et Earnings22) :** meilleur que les autres modèles audio-LLM comparés.
- **Résumé de dialogues et questions-réponses :** compétitif, avec de meilleurs scores que les autres audio-LLM sur la plupart des jeux de données locaux.
- **Point faible :** sentiment et émotion (jeux MELD), où le modèle est clairement moins bon que les autres.

### Conclusion des auteurs

Une curation soignée des données et une optimisation adaptée permettent de réduire nettement l'écart entre parole et texte dans un contexte local. Les modèles généralistes comme Whisper restent performants, mais ont besoin d'être localisés pour atteindre de bons résultats dans un contexte précis.

### Limites (annoncées par les auteurs)

1. **Contexte audio limité à 30 secondes :** pas de longues conversations ni d'échanges à plusieurs tours pour l'instant.
2. **Oubli catastrophique :** l'affinage complet du modèle pour la reconnaissance et la traduction lui a fait perdre une partie de sa capacité à suivre certaines consignes écrites.
3. **Faiblesse sur les émotions et absence d'alignement de sécurité :** les performances sur le sentiment et l'émotion sont inférieures, et le modèle n'a pas été aligné spécifiquement pour la sécurité.

---

## Comparaison des deux travaux

Les deux articles reposent sur la même idée : un encodeur Whisper, un adaptateur et un LLM, le tout de bout en bout, sans passer par une transcription intermédiaire. La différence est l'objectif et l'échelle. **SpeechLLM** vise la sobriété : un adaptateur minuscule (environ 2 millions de paramètres), un petit LLM gelé, quelques centaines d'heures de données, trois tâches en anglais (transcription, entités, sentiment), évalué sur SLUE. **MERaLiON** vise la portée et la localisation : un encodeur et un adaptateur entièrement réentraînés, un LLM de 9 milliards de paramètres légèrement affiné, 260 000 heures de données, six types de tâches et des accents de Singapour, évalué sur AudioBench. Le premier est plus économique et ciblé, le second est plus grand, plus polyvalent et plus coûteux à entraîner. Tous deux ont une faiblesse commune : les émotions fines restent mal couvertes.

---

## Partie pratique : ce que j'en retiens pour mon agent audio local

### Mon constat

Mon agent actuel est un **système en cascade** : la voix passe par Whisper, qui produit une transcription, puis un modèle de langage (Qwen) lit ce texte et répond. Le défaut est que l'analyse des émotions se fait à partir du texte seul : le ton, le stress ou la tristesse contenus dans la voix sont perdus. Après lecture des deux articles, je souhaite passer à un **système de bout en bout** qui lit les émotions directement à partir de la voix, comme dans ces travaux. Contrainte importante : mes données sont sensibles et ne doivent pas être envoyées sur Internet, donc tout doit tourner en local.

### Ce que j'ai retenu des articles

- Un petit adaptateur suffit à relier la voix à un LLM sans tout réentraîner, ce qui réduit beaucoup les besoins en mémoire.
- Entraîner en plusieurs étapes (d'abord du général, puis du spécifique) améliore les résultats quand on a peu de données annotées.
- Un classifieur auxiliaire utilisé seulement pendant l'entraînement aide l'adaptateur à conserver l'information utile (ici, le sentiment).
- Attention : ni l'un ni l'autre n'a résolu les émotions fines. SpeechLLM ne teste que trois classes de sentiment, et MERaLiON est plus faible sur les émotions.

### Trois propositions qui peuvent marcher en local

**Proposition 1 : un modèle d'émotion déjà entraîné en parallèle de la transcription (la plus simple).** La voix passe directement dans un modèle spécialisé dans les émotions, par exemple emotion2vec+, qui classe l'émotion (colère, joie, tristesse, peur, neutre...) sans transcription. En parallèle, Whisper transcrit le contenu, et Qwen rédige l'analyse à partir du texte et de l'étiquette d'émotion. D'après les fiches publiques du modèle, il est léger (environ 90 à 300 millions de paramètres) et peut tourner avec environ 4 Go de mémoire.

**Proposition 2 : un modèle audio direct comme Qwen2-Audio.** Un seul modèle écoute la voix et répond à des consignes comme « quelle émotion exprime cette personne ? ». Les versions compressées demandent d'environ 4 à 16 Go de mémoire selon la compression. Il faut tester sa fiabilité sur les émotions, car les modèles de ce type sont plus faibles sur ce point dans MERaLiON.

**Proposition 3 : construire mon propre adaptateur, comme dans SpeechLLM.** Whisper gelé, un petit adaptateur entraînable et un petit LLM gelé, entraînés sur mes propres émotions cibles (heureux, stressé, triste...). Avantage : je choisis mes catégories. Inconvénients : il faut des enregistrements annotés avec ces émotions et une carte graphique.

**TEST Proposition 1** : J'ai mis en œuvre l'option 1 de mes propositions : ajouter un modèle spécialisé dans les émotions de la voix, emotion2vec, en parallèle de la transcription. Voici comment fonctionne mon agent. Il tourne en local, sans Internet, et il est composé de deux programmes séparés, placés dans le même dossier. Le premier est l'agent : il transcrit l'audio avec faster-whisper, puis envoie la transcription à Qwen, qui tourne avec Ollama. Le second, emotion_analyse.py, détecte les émotions directement dans la voix avec emotion2vec. Comme les enregistrements longs saturaient la mémoire, ce programme découpe d'abord l'audio en tranches de 15 secondes, analyse chaque tranche, puis calcule la moyenne des émotions. L'agent lance ce second programme, récupère les émotions de la voix, et les donne à Qwen avec la transcription. Qwen compare alors ce que la personne dit avec ce que sa voix exprime, et signale les accords et les contradictions. Ainsi, les émotions ne viennent plus seulement des mots, mais aussi du ton de la voix.


### Quels outils pour réaliser ce projet ?

 Exemples concrets :

- **Python :** le langage dans lequel tout se programme.
- **PyTorch :** la bibliothèque qui permet de créer et d'entraîner des réseaux de neurones, comme l'adaptateur.
- **Hugging Face Transformers :** la bibliothèque qui permet de télécharger et d'utiliser des modèles d'IA existants (Whisper, Qwen, TinyLlama, MERaLiON) en local.
- **FunASR :** une bibliothèque qui permet d'utiliser emotion2vec directement.
- **PEFT (pour LoRA) :** une bibliothèque qui permet de modifier légèrement un grand modèle en n'entraînant qu'une petite partie.
- **Ollama ou llama.cpp :** des programmes qui permettent de faire tourner des modèles de langage compressés sur un ordinateur ordinaire.
- **Librosa :** une bibliothèque pour lire et préparer des fichiers audio.

Pour garder les données en local : télécharger les modèles une seule fois, puis couper l'accès Internet pendant le traitement, et stocker les enregistrements sur un disque chiffré.

### Plan d'action proposé

1. Commencer par la Proposition 1, la plus légère et la plus rapide à mettre en place.
2. Tester sur quelques enregistrements et noter les erreurs.
3. Si les catégories d'émotions ne suffisent pas, essayer la Proposition 2.
4. Ne passer à la Proposition 3 que si les deux premières ne répondent pas au besoin, car elle demande des données annotées et plus de calcul.

---

## Références

1. J. Yoo, K. Chandiramani, D. Tadimeti, A. Girma, C. Dhir. *SpeechLLM: Unified Speech and Language Model for Enhanced Multi-Task Understanding in Low Resource Settings.* arXiv:2509.04473, 2025. https://arxiv.org/abs/2509.04473
2. MERaLiON Team (Y. He, Z. Liu, S. Sun, B. Wang, W. Zhang, X. Zou, N. F. Chen, A. T. Aw). *MERaLiON-AudioLLM: Bridging Audio and Language with Large Language Models.* arXiv:2412.09818, 2025. https://arxiv.org/abs/2412.09818
3. S. Shon et al. *SLUE: New Benchmark Tasks for Spoken Language Understanding Evaluation on Natural Speech.* arXiv:2111.10367. https://arxiv.org/abs/2111.10367 ; code : https://github.com/asappresearch/slue-toolkit
4. B. Wang et al. *AudioBench: A Universal Benchmark for Audio Large Language Models.* arXiv:2406.16020, NAACL 2025. https://arxiv.org/abs/2406.16020 ; code : https://github.com/AudioLLMs/AudioBench
-----------------------------
# State of the Art: End-to-End Audio LLMs (SpeechLLM and MERaLiON)

**Date:** 24 November 2026

Over the past two weeks, I read two articles related to multimodal AI and agents. Here is the resulting state of the art.

**Author:** Diya

**Context:** As part of my state-of-the-art review and reading progress, I read two articles related to multimodal AI agents (voice + text). This report summarizes each article, compares them, and then explains what I take from them for my audio agent, which must run locally.

---

## Article 1: SpeechLLM (SENSE-ASR)

### Reference

- **Title:** SpeechLLM: Unified Speech and Language Model for Enhanced Multi-Task Understanding in Low Resource Settings
- **Authors:** Jaekwon Yoo, Kunal Chandiramani, Divya Tadimeti, Abenezer Girma, Chandra Dhir (JPMorganChase and Columbia University)
- **Publication:** arXiv:2509.04473, cs.CL, 29 August 2025
- **Link:** https://arxiv.org/abs/2509.04473
- **Benchmark used:** SLUE (Spoken Language Understanding Evaluation), with SLUE-VoxPopuli (named entity recognition) and SLUE-VoxCeleb (sentiment)
  - Benchmark paper: https://arxiv.org/abs/2111.10367
  - Code and leaderboard: https://github.com/asappresearch/slue-toolkit

### Introduction: what the authors did

Connecting a speech encoder to a large language model (LLM) usually requires a lot of data and compute. The authors propose SENSE-ASR, an end-to-end system that performs three tasks in a single pass: transcription (ASR), named entity recognition (NER: people, places, dates) and sentiment analysis (SA: positive, negative, neutral). The key idea is to avoid heavy retraining: only a small adapter is trained. To compensate for the lack of annotated data, an LLM (GPT-4o) automatically annotates 960 hours of LibriSpeech with entities.

### Architecture

- **Speech encoder:** Whisper (small and medium variants), frozen. Speech becomes a sequence of vectors.
- **Adapter (the main contribution):** An adaptive average pooling layer reduces 1500 vectors to 250, a normalization layer stabilizes the values, and a linear projection matches the LLM's embedding size. Roughly 1.6 to 2.1 million trainable parameters.
- **LLM:** TinyLlama (a small model trained on 3 trillion tokens), frozen (or lightly fine-tuned with LoRA at the end).
- **Regularizer classifier:** A small network used only during training. It tries to predict entities or sentiment from the adapter's output, which forces the adapter to preserve that information. It is removed at inference.

### Training

Three stages, from general to specific:

1. Pre-training on LibriSpeech (960 h of read books) to learn transcription.
2. Continued training on LibriSpeech automatically annotated by GPT-4o (entities), to also learn to detect entities.
3. Fine-tuning on human-annotated data: SLUE-VoxPopuli (about 15 h, European Parliament speeches) for entities, SLUE-VoxCeleb (about 12.8 h, interviews) for sentiment.

Data augmentation (speed perturbation, SpecAugment) is applied.

### Results

- **Transcription (LibriSpeech, Whisper medium):** Word error rate of 3.67% on test-clean versus 5.01% for the baseline SLAM-ASR, about 26% relative improvement, with 2.1M trainable parameters versus 15.2M.
- **Entities (VoxPopuli):** F1 goes from 62.0 (no preparation) to 64.3 (LibriSpeech), 65.0 (GPT-4o annotations), 65.8 (classifier), then 68.9 (LoRA).
- **Sentiment (VoxCeleb):** F1 goes from 58.9 to 61.0 (LibriSpeech), 63.6 (classifier), then 65.9 (LoRA), versus 48.1 to 49.8 for the benchmark's end-to-end baselines.
- **Overall SLUE score:** 74.6 versus 68.1 for the best end-to-end baseline (about 9.5% relative improvement), close to the cascade system (75.7).

### Authors' conclusion

A very lightweight adapter, combined with multi-stage training that uses synthetic annotations, is enough to give an LLM strong speech understanding capabilities, with few trainable parameters and little manual annotation.

### Limitations (my analysis)

1. **Narrow tasks and language:** Only transcription, entities and three-class sentiment, in English. No fine-grained emotions (stress, sadness).
2. **Little human data and number inconsistencies:** 15 h for entities; some figures differ between the text and the tables (for example 74.3 and 74.6 for the same score).
3. **Dependence on an external LLM for annotation:** GPT-4o is used for data preparation, which is a problem if the data is sensitive and must stay local.

---

## Article 2: MERaLiON-AudioLLM

### Reference

- **Title:** MERaLiON-AudioLLM: Bridging Audio and Language with Large Language Models
- **Authors:** MERaLiON Team: Yingxu He, Zhuohan Liu, Shuo Sun, Bin Wang, Wenyu Zhang, Xunlong Zou, Nancy F. Chen, Ai Ti Aw (Institute for Infocomm Research, A*STAR, Singapore)
- **Publication:** arXiv:2412.09818, cs.CL, version 3, 16 January 2025
- **Link:** https://arxiv.org/abs/2412.09818
- **Model:** https://huggingface.co/MERaLiON/MERaLiON-AudioLLM-Whisper-SEA-LION
- **Benchmark used:** AudioBench (Wang et al., 2024), with datasets for speech recognition, translation, question answering, dialogue summarization, speech instruction and paralinguistics.
  - Benchmark paper: https://arxiv.org/abs/2406.16020
  - Code and leaderboard: https://github.com/AudioLLMs/AudioBench

### Introduction: what the authors did

The team built the first speech-text model designed for Singapore's multilingual and multicultural context (English, Chinese, Malay, Tamil and Singlish). Conventional speech recognition systems often struggle with accents, dialects and language mixing. The model takes an (audio, text instruction) pair as input and answers with text. It handles several tasks: transcription, translation, spoken question answering, conversation summarization, spoken instruction following and paralinguistic recognition (gender, accent, emotion).

### Architecture

- **Audio encoder:** MERaLiON-Whisper, based on the Whisper-large-v2 encoder and retrained on local data (1500 vectors of dimension 1280 as output).
- **Adapter:** A simple multilayer perceptron called MLP-100. It groups vectors in blocks of 15 and outputs 100 vectors, at the size expected by the LLM.
- **Text decoder:** SEA-LION V3, a local LLM built from Gemma 2 (9 billion parameters) and further trained on 200 billion tokens in Singapore and Southeast Asian languages.
- The audio vectors and the tokenized instruction are concatenated, then the LLM generates the answer.

### Training

1. **Encoder retraining** on cleaned local speech recognition data (national IMDA corpus, in-house and public data).
2. **Multimodal instruction fine-tuning** on 260,000 hours of speech-text pairs, much of it from the National Speech Corpus (about 10,600 h of Singapore English), complemented by synthetic data (dialogue summarization, question answering, gender).
3. The encoder and adapter are fully retrained; the LLM is partially fine-tuned with LoRA (rank 8). Training: about 200,000 steps, 2 days on 128 H100 GPUs, with spectrogram augmentation.

### Results

Evaluation uses AudioBench, compared against Qwen2-Audio 7B, WavLLM, SALMONN and a cascade system.

- **Local speech recognition:** On part 2 of Singapore's national corpus (readings with local names of people, dishes, places and brands), the word error rate is 5%, versus 19% for Qwen2-Audio and 33% for Whisper-large-v2.
- **Unseen data (Earnings21 and Earnings22):** Better than the other audio LLMs compared.
- **Dialogue summarization and question answering:** Competitive, with better scores than the other audio LLMs on most local datasets.
- **Weak point:** Sentiment and emotion (MELD datasets), where the model is clearly worse than the others.

### Authors' conclusion

Careful data curation and suitable optimization significantly narrow the gap between speech and text in a local context. General-purpose models like Whisper remain strong, but need localization to reach good results in a specific context.

### Limitations (stated by the authors)

1. **Audio context limited to 30 seconds:** No long conversations or multi-turn exchanges for now.
2. **Catastrophic forgetting:** Full fine-tuning for recognition and translation made the model lose part of its ability to follow certain written instructions.
3. **Weakness on emotions and no safety alignment:** Performance on sentiment and emotion is lower, and the model has not been specifically aligned for safety.

---

## Comparison of the two works

Both articles rely on the same idea: a Whisper encoder, an adapter and an LLM, end to end, without an intermediate transcription.

The difference is in goal and scale:

- **SpeechLLM** aims for frugality: a tiny adapter (about 2 million parameters), a small frozen LLM, a few hundred hours of data, three tasks in English (transcription, entities, sentiment), evaluated on SLUE.
- **MERaLiON** aims for breadth and localization: a fully retrained encoder and adapter, a lightly fine-tuned 9-billion-parameter LLM, 260,000 hours of data, six task types and Singaporean accents, evaluated on AudioBench.

The first is cheaper and more targeted, the second is larger, more versatile and more expensive to train. Both share a weakness: fine-grained emotions remain poorly covered.

---

## Practical part: what I take from this for my local audio agent

### My observation

My current agent is a **cascade system**: the voice goes through Whisper, which produces a transcript, then a language model (Qwen) reads that text and answers. The flaw is that emotion analysis is done from text alone: tone, stress or sadness carried by the voice are lost.

After reading both articles, I want to move to an **end-to-end system** that reads emotions directly from the voice, as in these works.

Important constraint: my data is sensitive and must not be sent over the Internet, so everything must run locally.

### What I retained from the articles

- A small adapter is enough to connect speech to an LLM without retraining everything, which greatly reduces memory needs.
- Training in several stages (general first, then specific) improves results when annotated data is scarce.
- An auxiliary classifier used only during training helps the adapter keep useful information (here, sentiment).
- Caution: neither article has solved fine-grained emotions. SpeechLLM only tests three sentiment classes, and MERaLiON is weaker on emotions.

### Three proposals that can work locally

**Proposal 1: A pretrained emotion model running in parallel with transcription (the simplest).**

The voice goes directly into a model specialized in emotions, for example emotion2vec+, which classifies the emotion (angry, happy, sad, fearful, neutral...) without transcription. In parallel, Whisper transcribes the content, and Qwen writes the analysis from the text and the emotion label. According to the model's public pages, it is lightweight (about 90 to 300 million parameters) and can run with about 4 GB of memory.

**Proposal 2: A direct audio model such as Qwen2-Audio.**

A single model listens to the voice and answers instructions such as "what emotion does this person express?". Compressed versions need roughly 4 to 16 GB of memory depending on the compression. Its reliability on emotions must be tested, since models of this type are weaker on this point in MERaLiON.

**Proposal 3: Build my own adapter, as in SpeechLLM.**

Frozen Whisper, a small trainable adapter and a small frozen LLM, trained on my own target emotions (happy, stressed, sad...). Advantage: I choose my categories. Drawbacks: it needs recordings annotated with those emotions and a graphics card.

**TEST Proposal 1**:I implemented option 1 from my proposals: adding a model specialised in vocal emotions, emotion2vec, alongside the transcription. Here is how my agent works. It runs locally, without Internet access, and is made of two separate programs placed in the same folder. The first is the agent: it transcribes the audio with faster-whisper, then sends the transcript to Qwen, which runs through Ollama. The second, emotion_analyse.py, detects emotions directly from the voice using emotion2vec. Because long recordings overloaded the memory, this program first cuts the audio into 15-second segments, analyses each segment, then averages the emotions. The agent runs this second program, collects the emotions detected in the voice, and passes them to Qwen along with the transcript. Qwen then compares what the person says with what their voice expresses, and points out agreements and contradictions. This way, emotions no longer come only from the words, but also from the tone of the voice.


### Which tools can I use to build this project?

A "tool" is simply a program or code library used to build one part of the project. Concrete examples:

- **Python:** The language everything is programmed in.
- **PyTorch:** The library for creating and training neural networks, such as the adapter.
- **Hugging Face Transformers:** A library for downloading and running existing AI models (Whisper, Qwen, TinyLlama, MERaLiON) locally.
- **FunASR:** A library that lets me use emotion2vec directly.
- **PEFT (for LoRA):** A library that lets me lightly modify a large model by training only a small part of it.
- **Ollama or llama.cpp:** Programs that let me run compressed language models on an ordinary computer.
- **Librosa:** A library for reading and preparing audio files.

To keep data local: download the models once, then cut Internet access while processing, and store recordings on an encrypted disk.

### Proposed action plan

1. Start with Proposal 1, the lightest and fastest to set up.
2. Test on a few recordings and note the errors.
3. If the emotion categories are not enough, try Proposal 2.
4. Move to Proposal 3 only if the first two do not meet the need, since it requires annotated data and more compute.

---

## References

1. J. Yoo, K. Chandiramani, D. Tadimeti, A. Girma, C. Dhir. *SpeechLLM: Unified Speech and Language Model for Enhanced Multi-Task Understanding in Low Resource Settings.* arXiv:2509.04473, 2025. https://arxiv.org/abs/2509.04473
2. MERaLiON Team (Y. He, Z. Liu, S. Sun, B. Wang, W. Zhang, X. Zou, N. F. Chen, A. T. Aw). *MERaLiON-AudioLLM: Bridging Audio and Language with Large Language Models.* arXiv:2412.09818, 2025. https://arxiv.org/abs/2412.09818
3. S. Shon et al. *SLUE: New Benchmark Tasks for Spoken Language Understanding Evaluation on Natural Speech.* arXiv:2111.10367. https://arxiv.org/abs/2111.10367 ; code: https://github.com/asappresearch/slue-toolkit
4. B. Wang et al. *AudioBench: A Universal Benchmark for Audio Large Language Models.* arXiv:2406.16020, NAACL 2025. https://arxiv.org/abs/2406.16020 ; code: https://github.com/AudioLLMs/AudioBench





