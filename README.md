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
