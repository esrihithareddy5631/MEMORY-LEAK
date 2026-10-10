# MEMORY//LEAK

> Every defense leaves a pattern.


## 🏆 Hackathon Achievement
**MEMORY//LEAK won 2nd Prize at the Amrita Cyber Nation (ACN) Hackathon 2026 conducted at Amrita Vishwa Vidyapeetham, Chennai**
An interactive 3D cybersecurity simulation featuring an AI-inspired, rule-based adaptive adversary, threat investigation, incident response, and strategic decision-making.


A browser-based 3D cybersecurity strategy game where players investigate simulated incidents, choose defensive responses, and face an adaptive attacker that reacts to their behaviour.

Players act as cybersecurity analysts protecting **NEXUS**, a fictional organization. **ZERO**, the game's rule-based attacker, observes investigation habits and defensive decisions to influence future threats.

## Gameplay

Explore a 3D Security Operations Center (SOC), approach the alerted workstation, inspect evidence, and select a response before the incident timer expires. Decisions affect system integrity and mission outcomes.

The core loop is: **Attack → Alert → Investigate → Defend → Consequence → Recover → ZERO adapts.**

## Features

- First-person 3D SOC with interactive workstations, server racks, movement and collision handling.
- Seven threat families: phishing, social engineering, credential theft, malware, network intrusion, data exfiltration, and ransomware.
- Six difficulty levels: Beginner, Easy, Medium, Hard, Pro, and Impossible.
- Five mission slots per level, for 30 total. Impossible's fifth mission is a personalized finale containing three or four stages; it occupies the final mission slot.
- Randomized incident archetypes and evidence that can be informative, inconclusive, or misleading.
- Evidence-aware response evaluation: correct, partial, or wrong decisions.
- System-integrity consequences influenced by outcome, incident severity, and level.
- Rule-based adaptation using category performance, neglected evidence, and repeated defensive actions.
- Mission history, progression, saved settings, and browser-local progress.
- Procedural audio using the Web Audio API, with audio and mouse-sensitivity settings.

## How ZERO adapts

ZERO records outcomes across identity, endpoint, and network categories. It recomputes threat-family weights before sampling the next incident:

1. Strong performance in one category shifts pressure toward other categories; weak performance increases pressure in that category.
2. Frequently overlooked investigation options increase the likelihood of associated threats.
3. Repeated dependence on one defense increases pressure from families where that defense is insufficient.
4. Weights are normalized and used for weighted random selection among the current level's unlocked threats.

The final protocol favours the player's weaker categories. This is **rule-based behavioural adaptation**, implemented directly in JavaScript. It does not use a trained machine-learning model or an external AI service.

## Technology

| Component | Implementation |
| --- | --- |
| Interface | HTML5 and CSS3 |
| Game and adaptation logic | JavaScript |
| 3D rendering | Three.js r128 / WebGL |
| Audio | Web Audio API |
| Progress storage | localStorage |
| Distribution | Static HTML; no build step |

The current browser prototype is implemented in one HTML file. It does not require Node.js, npm, a backend, or a database.

## Run locally

Download or clone this repository, then serve its root directory:

```bash
python -m http.server 8000
```

Open **http://localhost:8000** in a desktop browser with WebGL enabled. Python is only needed for this optional local server.

The game currently loads Three.js from cdnjs, so internet access is required to retrieve that dependency. Click PLAY and interact with the game to enable browser-controlled pointer capture and audio.

## Controls

| Input | Action |
| --- | --- |
| WASD / arrow keys | Move |
| Mouse | Look around |
| Shift | Sprint |
| Space | Jump |
| E | Interact with a workstation |
| Esc | Pause |

## Progress and storage

Progress is saved in the current browser's localStorage under `memoryleak_save_v1`. Saves occur at mission boundaries, level completion, and relevant state changes, rather than continuously during an incident.

Saved data does not synchronize between devices, browsers, or website origins. Clearing site data removes the save; blocked browser storage can prevent persistence.

## Repository contents

- `index.html`: complete browser game, including styling, game logic, scenario definitions, 3D scene, audio, and persistence.
- `docs/project-presentation.pdf`: supplied project presentation.
- `CONTRIBUTING.md`: contribution and manual verification guidance.
- `.gitignore`: excludes common local temporary files.

## Project scope

This is a playable educational prototype using simulated threats and predefined incident archetypes. It does not inspect live traffic or perform real incident containment. No measured learning improvement, model accuracy, or performance benchmark is claimed.

The presentation includes C# and Blender references; the code provided in this repository implements the browser prototype with JavaScript and Three.js.

## Limitations

- Desktop keyboard and mouse interaction is the current control scheme.
- Offline operation requires replacing the external Three.js dependency with a locally hosted copy.
- Adaptation is based on explicit rules and predefined scenarios.
- Browser performance depends on WebGL support and device capabilities.
- No automated test suite is included in this starter repository.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for suggested checks and pull-request guidance.

## License

No project license has been selected in this starter package. Add a LICENSE file after the project owners agree on reuse permissions. Third-party dependencies retain their own licenses.
