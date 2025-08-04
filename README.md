# 🤖 Agent RAG avec n8n - Système de Q&A Intelligent sur Documents

[![n8n](https://img.shields.io/badge/n8n-Workflow-FF6D6D?style=flat-square&logo=n8n)](https://n8n.io/)
[![Qdrant](https://img.shields.io/badge/Qdrant-Vector%20DB-DC382C?style=flat-square&logo=qdrant)](https://qdrant.tech/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o%20mini-412991?style=flat-square&logo=openai)](https://openai.com/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=flat-square&logo=node.js)](https://nodejs.org/)

Un système RAG (Retrieval-Augmented Generation) complet construit avec n8n pour indexer automatiquement vos documents et répondre intelligemment aux questions avec citations des sources.
## 📚 Sommaire

1. [Fonctionnalités](#-fonctionnalités)
2. [Architecture](#-architecture)
3. [Installation Rapide](#-installation-rapide)
4. [Configuration](#-configuration)
5. [Utilisation](#-utilisation)
6. [Structure du projet](#-structure-du-projet)
7. [Workflow détaillé](#-workflow-détaillé)
8. [Personnalisation](#-personnalisation)
9. [Dépannage](#-dépannage)
10. [Métriques et performances](#-métriques-et-performances)
11. [Contribution](#-contribution)
12. [Licence](#-licence)
13. [Remerciements](#-remerciements)
14. [Support](#-support)

## 🎯 Fonctionnalités

- **Ingestion automatique** de documents (PDF, TXT, DOCX, MD, Java, XML)
- **Recherche sémantique** dans une base vectorielle Qdrant
- **Chat intelligent** avec citations automatiques des sources
- **Interface conversationnelle** intégrée
- **Mémoire de conversation** pour un contexte persistant
- **Analyse multi-documents** avec références croisées

## 🏗️ Architecture

```
📁 Documents locaux
    ↓
🔄 n8n Workflow d'ingestion
    ↓
🗃️ Qdrant Vector Store
    ↓
💬 Interface Chat
    ↓
🤖 Agent RAG + OpenAI GPT-4o mini
```

## 🚀 Installation Rapide

### Prérequis

- Node.js 18+ ([Télécharger](https://nodejs.org/))
- Compte [Qdrant Cloud](https://cloud.qdrant.io/) (gratuit)
- Clé API [OpenAI](https://platform.openai.com/api-keys)

### Étapes d'installation

1. **Installer n8n**
   ```bash
   npm install -g n8n
   ```

2. **Cloner ce repository**
   ```bash
   git clone https://github.com/votre-username/rag-agent-n8n.git
   cd rag-agent-n8n
   ```

3. **Démarrer n8n**
   ```bash
   n8n
   ```
   Puis tapez `o` pour ouvrir dans le navigateur (http://localhost:5678)

4. **Importer le workflow**
   - Menu Workflows → + New Workflow
   - Cliquer sur "Import from File"
   - Sélectionner `rag_agent.json`
   - Save

## ⚙️ Configuration

### 1. Configurer Qdrant

1. Créer un compte sur [Qdrant Cloud](https://cloud.qdrant.io/)
2. Générer une clé API
3. Créer une collection avec :
   - **Nom** : `test_rag` (ou selon votre choix)
   - **Dimensions** : `1536`
   - **Métrique** : `cosine`

### 2. Configurer les credentials dans n8n

**OpenAI API :**
- Nom : `OpenAi account`
- API Key : Votre clé OpenAI

**Qdrant API :**
- Nom : `QdrantApi account`
- API Key : Votre clé Qdrant
- URL : URL de votre cluster Qdrant

### 3. Personnaliser les chemins de documents

Dans le nœud "Read/Write Files from Disk", modifier :
```
D:/Stage_Talan_2025/fist-tast-documentation-master/**/*.*
```
Vers votre dossier de documents :
```
/chemin/vers/vos/documents/**/*.*
```

## 📖 Utilisation

### 1. Indexer vos documents

1. Placer vos documents dans le dossier configuré
2. Cliquer sur "Execute Workflow" dans le workflow d'ingestion
3. Attendre la fin de l'indexation

### 2. Utiliser le chat

1. Activer le workflow principal
2. Ouvrir l'interface de chat (webhook généré)
3. Poser vos questions !

### Exemple de conversation

```
🧑 Question : "Comment configurer l'API Qdrant ?"

🤖 Réponse : Pour configurer l'API Qdrant, vous devez :

1. **Créer une clé API**
   Connectez-vous à votre compte Qdrant et accédez à la section API Keys.

2. **Créer une collection**
   - Nom : selon votre projet
   - Dimensions : 1536 (compatible OpenAI)
   - Métrique : cosine

**Sources :**
- File: rag.pdf | Chunk: chunk_123 | Score: 0.95
```

## 📁 Structure du projet

```
rag-agent-n8n/
├── README.md                # Ce fichier
├── rag_agent.json           # Workflow n8n principal
├── guide_rag_agent/         # Guide détaillé
├── LICENSE/
└── .gitignore
```

## 🛠️ Workflow détaillé

### Partie 1 : Ingestion des documents
- **Read Files** → Lecture récursive des documents
- **Switch** → Filtrage par type de fichier
- **Extract** → Extraction du contenu textuel
- **Token Splitter** → Segmentation en chunks
- **Embeddings** → Conversion en vecteurs
- **Qdrant Store** → Stockage dans la base vectorielle

### Partie 2 : Chat et réponses
- **Chat Trigger** → Réception des messages
- **AI Agent** → Orchestration intelligente
- **Vector Search** → Recherche sémantique
- **OpenAI Model** → Génération de réponses
- **Memory** → Maintien du contexte

## 🎨 Personnalisation

### Modifier le prompt système

Dans le nœud "AI Agent", vous pouvez personnaliser le message système :

```
You are an AI assistant specialized in [YOUR DOMAIN]...
```

### Ajouter de nouveaux types de fichiers

Dans le nœud "Switch", ajouter de nouvelles conditions pour d'autres extensions.

## 🔧 Dépannage

### Problèmes courants

**❌ Erreur de lecture de fichiers**
- Vérifier les chemins absolus (utiliser `/` au lieu de `\`)
- S'assurer des droits d'accès aux fichiers

**❌ Connexion Qdrant échouée**
- Vérifier la clé API
- Confirmer que la collection existe
- Tester la connectivité réseau

**❌ Pas de réponses du chat**
- Vérifier que l'indexation est terminée
- Contrôler les logs n8n pour les erreurs
- S'assurer que OpenAI API fonctionne

## 📊 Métriques et performances

- **Chunk size** : 800 tokens (personnalisable)
- **Overlap** : 100 tokens
- **Limite de résultats** : 4 documents par requête
- **Modèle** : GPT-4o mini (optimisé coût/performance)

## 🤝 Contribution

Les contributions sont les bienvenues ! Voici comment participer :

1. Fork le projet
2. Créer une branche feature (`git checkout -b feature/nouvelle-fonctionnalite`)
3. Commit vos changements (`git commit -m 'Ajout nouvelle fonctionnalité'`)
4. Push vers la branche (`git push origin feature/nouvelle-fonctionnalite`)
5. Ouvrir une Pull Request

## 📄 Licence

Ce projet est sous licence MIT. Voir le fichier [LICENSE](LICENSE) pour plus de détails.

## 🙏 Remerciements

- [n8n](https://n8n.io/) pour la plateforme d'automatisation
- [Qdrant](https://qdrant.tech/) pour la base vectorielle
- [OpenAI](https://openai.com/) pour les modèles de langage

## 📞 Support

Si vous rencontrez des problèmes :

1. Consultez la [documentation complète](docs/guide_complet.pdf)
2. Ouvrez une [issue GitHub](https://github.com/votre-username/rag-agent-n8n/issues)
3. Rejoignez notre [Discord](https://discord.gg/votre-lien) pour la communauté

---

⭐ **N'oubliez pas de donner une étoile si ce projet vous aide !**