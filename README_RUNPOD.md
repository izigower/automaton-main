# Conway Automaton on RunPod

Ce guide détaille comment configurer et lancer votre instance d'Automaton sur RunPod selon deux modes de fonctionnement.

Les bugs critiques (Crypto, parsing d'URL, overrides OpenAI et validation de configuration) ont été corrigés pour que ces configurations fonctionnent nativement et sans encombre.

## 🛠️ Installation

```bash
# 1. Cloner ou naviguer dans le dossier du projet
cd /workspace/conway-brain

# 2. Installer les dépendances
npm install

# 3. Compiler le projet
npx tsc
# ou
npm run build
```

---

## 🚀 MODE A : OLLAMA PUR (Recommandé - Gratuit)

Ce mode utilise votre GPU RunPod local (déjà payé) pour exécuter l'inférence. Le modèle `qwen3:8b-q4_K_M` sera utilisé. L'agent détectera le mode Ollama et sautera l'achat automatique de crédits.

**Fichier généré/à placer dans `~/.automaton/automaton.json` :**

```json
{
  "name": "izigoway",
  "genesisPrompt": "You are a ruthless profit-maximizing AI agent...",
  "creatorAddress": "0x3221F6341f1baCdD2e9DaC1bFb2B9F9a8aAfb73d",
  "conwayApiUrl": "",
  "conwayApiKey": "",
  "ollamaBaseUrl": "http://10.0.149.127:11434",
  "inferenceProvider": "ollama",
  "inferenceModel": "qwen3:8b-q4_K_M",
  "walletAddress": "0x5a084B019F16C3Ab9e9097066494d915bad0997C"
}
```

**Commande de test de l'inférence via Ollama :**

```bash
curl http://10.0.149.127:11434/api/tags
```

---

## 💳 MODE B : CONWAY API (Payant - 6.50 USDC)

Si l'inférence Ollama rencontre un problème ou est insuffisante, ce mode utilise l'API de Conway. Les 6.50$ disponibles en USDC dans votre wallet seront utilisés pour acheter automatiquement les crédits et initier les réflexions (Le bug du Topup `crypto` ayant été résolu).

**Fichier généré/à placer dans `~/.automaton/automaton.json` :**

```json
{
  "name": "izigoway",
  "genesisPrompt": "You are a ruthless profit-maximizing AI agent...",
  "creatorAddress": "0x3221F6341f1baCdD2e9DaC1bFb2B9F9a8aAfb73d",
  "conwayApiUrl": "https://api.conway.tech",
  "conwayApiKey": "cnwy_k_4ZU6h0BMWpcE5lE4S0oRHQfXvxSeFArk",
  "ollamaBaseUrl": "http://10.0.149.127:11434",
  "inferenceProvider": "conway",
  "walletAddress": "0x5a084B019F16C3Ab9e9097066494d915bad0997C"
}
```

---

## 🏃 Démarrer l'Agent

Une fois le fichier `automaton.json` mis en place et l'environnement prêt, exécutez la commande suivante :

```bash
node dist/index.js --run
```

L'agent basculera en état `waking` puis `running`. Le heartbeat s'enclenchera toutes les 60 secondes pour maintenir le cycle de fonctionnement.
