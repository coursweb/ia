---
layout: page
title: Spec-Then-Code
permalink: spec-then-code.html
---

Question: J'ai vu des codeurs utiliser des fichiers specs.md ou ai-guidelines.md
Est-ce qu'il existe une structure recommandée ?

Réponse: Oui, il existe des structures recommandées pour les fichiers de spécifications ou de directives d'IA. Voici une structure courante que vous pouvez suivre pour créer un fichier `specs.md` ou `ai-guidelines.md` :

## Les fichiers de contexte pour LLM : les conventions qui émergent

### Les fichiers les plus courants

**CLAUDE.md** (spécifique à Claude Code). 
C'est le fichier que Claude Code lit automatiquement au démarrage d'une session. Il sert à donner du contexte persistant sur le projet : stack technique, conventions de code, commandes utiles, ce qu'il ne faut pas toucher.

**specs.md / PRD.md** (Product Requirements Document). 
Décrit ce que l'application doit faire : fonctionnalités, user stories, cas limites. C'est le "quoi".

**ai-guidelines.md / AGENTS.md**. 
Décrit comment le LLM doit travailler : conventions de nommage, règles d'architecture, ce qu'il ne doit jamais faire. C'est le "comment".

### Exemple de structure pour un projet

```
mon-projet/
├── CLAUDE.md              ← Lu automatiquement par Claude Code
├── docs/
│   ├── specs.md           ← Fonctionnalités & requirements
│   ├── architecture.md    ← Décisions techniques & diagrammes
│   └── api.md             ← Contrats d'API
└── .cursorrules           ← Si tu utilises Cursor
```



```markdown# Spécifications et Directives pour l'IA

## Introduction
- Présentation générale du projet et de l'objectif de ce document.
- Contexte et importance des spécifications pour le développement de l'IA.
## Objectifs
- Liste des objectifs spécifiques que l'IA doit atteindre.
- Exemples de cas d'utilisation et de scénarios d'application.
## Fonctionnalités
- Description détaillée des fonctionnalités que l'IA doit posséder.
- Priorisation des fonctionnalités (essentielles, souhaitables, optionnelles).
## Contraintes Techniques
- Liste des contraintes techniques à respecter (ex. : performance, sécurité, compatibilité).
- Exigences en matière de données (ex. : types de données, volume, qualité
).
## Architecture et Design
- Description de l'architecture proposée pour l'IA.
- Diagrammes et schémas pour illustrer la structure et les composants de l'IA
## Algorithmes et Modèles
- Liste des algorithmes et modèles d'IA recommandés pour le projet.
- Justification du choix des algorithmes et modèles.
## Évaluation et Tests
- Méthodes d'évaluation pour mesurer la performance de l'IA.
- Critères de succès et indicateurs de performance clés (KPI).
## Maintenance et Mise à Jour
- Plan de maintenance pour assurer la pérennité de l'IA.
- Stratégies pour les mises à jour et les améliorations futures.
## Conclusion
- Résumé des points clés du document.
- Prochaines étapes pour le développement de l'IA.
```

Cette structure vous aidera à organiser vos idées de manière claire et à fournir des directives précises pour le développement de votre projet d'IA. Vous pouvez adapter cette structure en fonction des besoins spécifiques de votre projet.

## Donner des consignes de comportement à l'IA

Un exemple: 

```
### Process de démarrage

Interviewe-moi avant de faire quoi que ce soit d'autre. Creuse en profondeur :

- Les décisions d'implémentation technique que la spec ne couvre pas
- Les hypothèses UI/UX qui nécessitent validation
- Les ambiguïtés ou contradictions dans la spec
- Les compromis dont je devrais être conscient

Ne pose pas de questions évidentes. Continue l'interview jusqu'à ce qu'on ait tout couvert, une série de questions à la fois.

Pose-moi les questions les unes après les autres, à choix multiple.

Ensuite, à partir de notre discussion, propose :

1. L'architecture et la structure de fichiers
2. Le découpage des tâches avec dépendances et ordre d'exécution
3. Si des sous-agents personnalisés seraient utiles, et si oui, ce qu'ils feraient

Ensuite, de retour en mode accept edits, mets à jour @docs/specs.md avec ce qu'on a discuté et toute l'information manquante nécessaire.

Écris le plan d'implémentation dans docs/PLAN.md. Écris la checklist des tâches dans docs/TODO.md.

```

### Points importants

**"Interviewe-moi avant de faire quoi que ce soit"** — c'est probablement la consigne la plus précieuse de tout le fichier. La plupart des gens donnent une spec et demandent du code immédiatement. Le LLM comble alors les trous avec ses propres hypothèses, souvent silencieusement. Forcer une phase d'interview évite ça.

**"Une série de questions à la fois, à choix multiple"** — très malin. Les LLM ont tendance à dumper 10 questions en bloc, ce qui est épuisant. Le choix multiple force aussi des options concrètes plutôt que des questions ouvertes vagues.

**Les consignes de style** (tabs, code lisible, pas de syntaxe fantaisiste) — mettre ça dans la spec plutôt que de le répéter à chaque session est un vrai gain de temps.

### Instruction visuelles

Si le LLM supporte la vision (GPT-4o, Claude, Qwen-VL), on peut lui donner des exports PNG/JPG des écrans.

Ce que tu dis au LLM :

"Voici la maquette desktop. Implémente index.html en respectant fidèlement cette mise en page. Consulte CLAUDE.md pour les contraintes techniques."

**Avantages :** Le LLM voit exactement ce que tu as dessiné — espacements, typographie, couleurs, disposition des éléments. Très efficace pour le layout global.
**Limite :** Il ne voit pas les états interactifs (hover, modal ouverte) sauf si tu les exportes séparément.

Cette page contient des informations venant de [cette discussion avec Claude.AI](https://claude.ai/share/3cb77af2-e9e6-4aeb-837a-caefb366306d).