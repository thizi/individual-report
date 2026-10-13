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

## Roadmap

- [ ] Finish the *Large Multimodal Agents* survey and write a summary sheet (goal, main idea, limitations, link to the prototype)
- [ ] Make the prototype more autonomous: Qwen chooses its own tools (smolagents, LangChain, or Ollama tool calling)
- [ ] Add emotion and voice tone analysis: librosa, openSMILE, wav2vec2 model
