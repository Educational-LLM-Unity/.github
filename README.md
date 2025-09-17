
# Projet ASAG — Agents Scolaires pour l'Apprentissage Guidé

## Introduction

### Problématique
Dans le système éducatif actuel, les enseignants du cycle primaire sont confrontés à un défi de taille : la difficulté de fournir des évaluations personnalisées et un suivi continu pour chaque élève.  
La charge de travail conséquente et le temps limité rendent cette tâche ardue, menant souvent à des évaluations génériques et chronophages.  
Ce constat met en lumière un besoin criant d'outils innovants pour soutenir le corps enseignant et améliorer l'expérience d'apprentissage des élèves.

### Objectifs du Projet
L'objectif central du projet **ASAG** est de répondre à cette problématique en développant une plateforme éducative intégrée.  
Cette plateforme s'appuie sur des agents intelligents, basés sur des modèles de langage (LLMs), pour automatiser deux processus clés :

- **La génération d'exercices** de langue arabe (questions ouvertes, fermées, et exercices de lecture).
- **L'évaluation instantanée** des réponses des élèves.

En automatisant ces tâches, la plateforme vise à libérer un temps précieux pour les enseignants et à offrir un feedback immédiat et personnalisé aux élèves, favorisant ainsi un apprentissage plus engageant et efficace.

---

## Analyse Fonctionnelle : Cas d'Utilisation
L'architecture fonctionnelle du système ASAG s'articule autour de plusieurs agents spécialisés, chacun répondant à un besoin pédagogique précis.  
Les diagrammes de cas d'utilisation suivants illustrent les interactions des utilisateurs (**Enseignant** et **Élève**) avec ces modules.

### Agent de Questions Ouvertes
<img width="867" height="566" alt="image" src="https://github.com/user-attachments/assets/cc9d6d1b-2599-44c9-b50d-261812390eee" />


### Agent de Questions Fermées (QCM)
<img width="559" height="378" alt="image" src="https://github.com/user-attachments/assets/a06d7159-fe95-49eb-9f62-eefe9a8225e3" />


### Agent d'Évaluation de la Lecture
<img width="437" height="359" alt="image" src="https://github.com/user-attachments/assets/a03c5a83-1bb3-48b8-b12a-5c7c067b8af3" />


---

## Approche Adoptée et Expérimentations

### Agent de Questions Ouvertes

#### Génération de Questions
Deux approches principales ont été explorées :
- **Candidat 1 : Système RAG Local.** Bonne capacité d’indexation et de récupération de textes, mais limité par une base de connaissances restreinte.
- **Candidat 2 : Architecture via API (Choix Final).** Utilisation de l’API **Google Gemini**, offrant une meilleure qualité de génération, une fiabilité totale et une flexibilité via le *Prompt Engineering*.

#### Évaluation des Réponses
Étude comparative des modèles :
- **Candidat 1 : Encodeur-Seul (AraBERT).** Excellent pour la classification, fiable et performant.
- **Candidat 2 : Encodeur-Décodeur (AraT5).** Fine-tuning effectué mais moins précis que la classification directe.

👉 **Conclusion :** Le modèle **AraBERT** a été retenu pour sa précision et sa fiabilité.

### Agent de Questions à Choix Multiples (QCM)
L’approche retenue combine **fine-tuning** et **assistance par IA** :
- Fine-tuning du modèle **Mistral-7B-Instruct-v0.2** pour générer des QCM en arabe.
- L’API **Gemini** permet aux enseignants de corriger et reformuler les QCMs avant validation.

### Agent d'Évaluation de la Lecture
Approche hybride :
- **Wav2Vec2** pour la transcription de l’audio en texte arabe vocalisé.
- **Gemini** pour l’analyse sémantique et la détection d’erreurs de compréhension.
- **Microsoft Azure Speech** pour fournir un feedback vocal interactif à l’élève.

---

## Gestion des Données et Prétraitement

### Source et Extraction Initiale
La principale source de données est un corpus de textes issus de manuels scolaires de langue arabe pour le cycle primaire.  
Un script Python a été développé pour extraire le texte brut à partir des fichiers PDF.

### Préparation pour l’Agent QCM
1. Génération initiale de QCMs via **Google AI Studio**.  
2. Affinage et correction avec l’assistance IA.  
3. Données formatées en JSON et structurées pour le fine-tuning de **Mistral-Instruct**.  
   - **80%** pour l’entraînement, **20%** pour la validation.

### Préparation pour l’Agent de Questions Ouvertes
- Réutilisation des textes QCM.  
- Script Python basé sur l’API **Groq (Llama-3)**.  
- Génération automatique de **5 questions ouvertes par texte**, créant un corpus de haute qualité.

---

## Ingénierie et Architecture Technique
L'architecture du système ASAG est modulaire et évolutive, intégrant les différents agents pour une expérience fluide.

### Diagrammes Techniques
#### Agent de Questions Ouvertes (Génération)
<img width="1137" height="314" alt="image" src="https://github.com/user-attachments/assets/0c078af9-ce03-465a-81a7-29c26607ebb6" />


#### Agent de Questions Ouvertes (Évaluation)
<img width="2206" height="543" alt="image" src="https://github.com/user-attachments/assets/b71d0f27-b243-4337-b281-f56c3355da0b" />


#### Agent de Questions Fermées (QCM)
<img width="2026" height="562" alt="image" src="https://github.com/user-attachments/assets/3ee27c2e-cc13-4968-9bde-e6dc5be7ea4b" />


#### Agent d'Évaluation de la Lecture
<img width="905" height="396" alt="image" src="https://github.com/user-attachments/assets/485b113b-1f82-4cf9-b631-9ed0395a8036" />




---

## Conclusion
Le projet **ASAG** a abouti à la conception d’une plateforme éducative innovante combinant plusieurs agents intelligents.  
En intégrant le fine-tuning de modèles spécialisés et l’utilisation d’APIs performantes, nous avons démontré la viabilité d’une solution complète pour l’éducation.  

- Pour l’enseignant : un **assistant pédagogique puissant**.  
- Pour l’élève : une **expérience interactive et personnalisée**.  

ASAG montre que l’intégration pragmatique des technologies d’IA peut créer des outils éducatifs réellement efficaces et engageants pour l’avenir.
