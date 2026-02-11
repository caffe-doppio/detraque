# detraque ❌🍪

> Casse le tracking. Reprends le contrôle de tes liens.

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
![Version](https://img.shields.io/badge/version-0.1.0--beta-orange)
![Shell](https://img.shields.io/badge/shell-bash-green)

[🏴󠁧󠁢󠁥󠁮󠁧󠁿 English version](README.en.md)

---

## 🎯 Qu'est-ce que c'est ?

**detraque** est un outil en ligne de commande qui retire automatiquement les paramètres de tracking des URLs. Léger, rapide, avec logging automatique et support des timestamps pour YouTube.

Conçu pour les militant·es, les professionnel·les de la donnée, les fonctionnaires, et toute personne soucieuse de sa vie privée numérique.

### ✨ Fonctionnalités

- 🧹 **Nettoyage automatique** des paramètres de tracking sur YouTube, X/Twitter, Facebook, Instagram
- ⏱️ **Timestamps YouTube** : ajoute facilement un timestamp à tes liens vidéos
- 📝 **Logging automatique** : garde un historique de tous tes liens nettoyés
- ✅ **Vérification d'URLs** : teste si un lien fonctionne avant de le partager
- 📋 **Copie automatique** dans le presse-papier (macOS)

### 🔍 Plateformes supportées

| Plateforme | Paramètres retirés |
|------------|-------------------|
| YouTube | `?si=`, `&feature=`, `&utm_*` |
| X/Twitter | `?s=`, `?t=`, `&utm_*` |
| Facebook | `?fbclid=`, `&utm_*` |
| Instagram | `?igshid=`, `&utm_*` |

---

## 🚨 Pourquoi le tracking est problématique

### 📊 Vos données personnelles sont revendues

Les paramètres de tracking dans les URLs permettent aux plateformes de savoir :
- **Qui** partage un lien avec **qui**
- **Quand** et **où** un lien est partagé
- **Comment** un contenu se propage dans votre réseau

Ces données alimentent des profils publicitaires détaillés qui sont ensuite monétisés. **Quand c'est gratuit, c'est vous le produit.**

### 🏢 Position dominante de la BigTech

Le tracking systématique renforce le pouvoir des GAFAM en leur donnant un avantage informationnel considérable sur :
- Les comportements sociaux
- Les réseaux d'influence
- Les modes de diffusion de l'information

Mais aussi sur vos proches, et sur la nature même de vos communications.

### 🔒 Enjeux de cybersécurité

Les paramètres de tracking peuvent aussi :
- **Révéler des informations sensibles** sur vous ou votre organisation
- **Exposer vos habitudes** de navigation et de communication
- **Faciliter le phishing** en permettant aux attaquants de mieux cibler leurs victimes

Les url bien propres, c'est une **bonne pratique d'hygiène numérique**.

---

## 💡 Pourquoi "detraque" ?

**detraque** c'est un jeu de mots :
Un petit outil qui tourne sur ta machine **pour casser le tracking**

*Fun fact* : Le nom fait aussi référence à la chanson **"Mon inconnu"** de Zaho de Sagazan 🎵

---

## 📦 Installation

### Prérequis

- **bash** (installé par défaut sur macOS et Linux)
- **curl** (généralement préinstallé)
- **sed** et **grep** (outils standard)

### Installation rapide

```bash
# 1. Télécharger le script
curl -O https://raw.githubusercontent.com/caffe-doppio/detraque/main/detraque

# 2. Rendre exécutable
chmod +x detraque

# 3. Déplacer dans un dossier du PATH
sudo mv detraque /usr/local/bin/

# 4. Vérifier l'installation
detraque help
```

### Installation manuelle

```bash
# 1. Cloner le repo
git clone https://github.com/caffe-doppio/detraque.git
cd detraque

# 2. Copier le script
cp detraque ~/bin/detraque
chmod +x ~/bin/detraque

# 3. Ajouter ~/bin au PATH si nécessaire
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.zshrc  # ou ~/.bashrc
source ~/.zshrc
```

---

## 🚀 Utilisation

### Commandes disponibles

```bash
detraque clean <url>                  # Nettoyer une URL
detraque clean-time <url> <hh:mm:ss>  # Nettoyer + ajouter timestamp
detraque timestamp <hh:mm:ss> [url]   # Convertir timestamp
detraque verify <url>                 # Vérifier une URL
detraque logs                         # Afficher les logs du jour
detraque help                         # Aide
```

### Exemples pratiques

#### 1️⃣ Nettoyer un lien YouTube

```bash
detraque clean "https://www.youtube.com/watch?v=abc123&si=tracker123"
```

**Résultat :**
```
Plateforme détectée : YouTube

Original :
https://www.youtube.com/watch?v=abc123&si=tracker123

Nettoyé :
https://www.youtube.com/watch?v=abc123

✓ Loggé dans : ~/Documents/detraque-logs/2025-02-05-cleaned-urls.md
✓ Copié dans le presse-papier
```

#### 2️⃣ Partager un moment précis d'une vidéo (sans tracking)

```bash
detraque clean-time "https://youtube.com/watch?v=abc&si=tracker" 1:08:33
```

**Résultat :**
```
Plateforme détectée : YouTube
Timestamp : 1:08:33 (4113s)

Original :
https://youtube.com/watch?v=abc&si=tracker

Nettoyé + Timestamp :
https://youtube.com/watch?v=abc?t=4113s

✓ Loggé dans : ~/Documents/detraque-logs/2025-02-05-cleaned-urls.md
✓ Copié dans le presse-papier
```

#### 3️⃣ Noter plusieurs moments d'une longue vidéo

Pendant que tu regardes une conférence de 2h :

```bash
# Moment intéressant à 15:30
detraque clean-time "https://youtube.com/watch?v=conf2024" 15:30

# Autre moment à 45:20
detraque clean-time "https://youtube.com/watch?v=conf2024" 45:20

# Récupérer tous les liens
detraque logs
```

Tous tes moments sont loggés avec leurs timestamps, prêts à partager !

#### 4️⃣ Vérifier qu'un lien fonctionne

```bash
detraque verify "https://youtube.com/watch?v=abc123"
```

**Résultat :**
```
Vérification de : https://youtube.com/watch?v=abc123

✓ URL fonctionnelle (HTTP 200)
Titre : Ma super vidéo - YouTube
```

---

## 📊 Logs automatiques

Tous les liens nettoyés sont automatiquement sauvegardés dans :

```
~/Documents/detraque-logs/YYYY-MM-DD-cleaned-urls.md
```

**Format du log :**

```markdown
# URLs nettoyées - 2025-02-05

---

## [2025-02-05 14:30:15] - Timestamp: 1:08:33

**Original :**
```
https://www.youtube.com/watch?v=abc&si=tracker
```

**Nettoyé :**
```
https://www.youtube.com/watch?v=abc?t=4113s
```

---
```

Pour afficher les logs du jour :

```bash
detraque logs
```

---

## 🛠️ Compatibilité

### Systèmes supportés

- 🍎 **macOS** (testé sur macOS 14+)
- 🐧 **Linux** (Ubuntu, Debian, Fedora, Asahi, Arch...)
- 🖥️ **WSL** (Windows Subsystem for Linux)

### Presse-papier

La copie automatique fonctionne avec :
- **macOS** : `pbcopy` (préinstallé)
- **Linux** : `xclip` (à installer si nécessaire)

```bash
# Installation xclip sur Linux
sudo apt install xclip      # Debian/Ubuntu
sudo dnf install xclip      # Fedora
sudo pacman -S xclip        # Arch
```

---

## 🐧 Envie de sauter le pas vers Linux ?

**detraque** fonctionne nativement sur Linux. Si tu veux franchir le pas et découvrir un système libre, voici mes trois distributions préférées :

### 🟠 Ubuntu
**Pour débuter en douceur**
- Interface intuitive et moderne
- Énorme communauté francophone
- Support matériel excellent
- [Télécharger Ubuntu](https://ubuntu.com/download/desktop)

### 🍎 Asahi Linux
**Pour les Macs Apple Silicon**
- Distribution basée sur Fedora optimisée pour les processeurs M1/M2/M3
- Projet ambitieux qui libère les Macs modernes
- [Découvrir Asahi](https://asahilinux.org/)

### 🦜 Parrot OS
**Pour la sécurité et la vie privée**
- Distribution orientée cybersécurité avec **tous les outils préinstallés**
- Hyper stable out-of-the-box
- Peu connue mais incroyablement complète
- [Télécharger Parrot OS](https://parrotsec.org/)

---

## 🤝 Contribuer

Les contributions sont les bienvenues ! 

### Signaler un bug

Ouvre une [issue](https://github.com/caffe-doppio/detraque/issues) en décrivant :
- Le comportement attendu
- Le comportement observé
- Les étapes pour reproduire
- Ton système (macOS, Linux, version)

### Proposer une fonctionnalité

Tu as une idée ? Ouvre une [issue](https://github.com/caffe-doppio/detraque/issues) avec le tag `enhancement`.

### Ajouter une plateforme

Pour ajouter le support d'une nouvelle plateforme :
1. Fork le projet
2. Ajoute les patterns de nettoyage dans les fonctions `clean_url()` et `clean_time()`
3. Teste sur plusieurs URLs
4. Ouvre une Pull Request

---

## 📜 Licence

Ce projet est sous licence **GNU General Public License v3.0**.

Cela signifie que tu peux :
- 🌱 Utiliser cet outil librement
- 🧑🏻‍💻 Étudier et modifier le code source
- ♻️ Redistribuer des copies
- ↩️ Distribuer tes versions modifiées

**Condition importante** : Toute version modifiée doit également être distribuée sous GPL-3.0 (copyleft).

Voir le fichier [LICENSE](LICENSE) pour plus de détails.

---

## 👤 Auteur

Créé par **[@caffe-doppio](https://github.com/caffe-doppio)**

*Développé dans le cadre d'un engagement pour la souveraineté numérique et la protection de la vie privée.*

---

## 🙏 Remerciements

- À toutes les personnes qui militent pour un numérique plus éthique
- À tous·tes celle·eux qui s’engagent pour créer des alternatives libres
- À la communauté open source

---

## 📚 Ressources

### Vie privée et tracking

- [CNIL - Les cookies et autres traceurs](https://www.cnil.fr/fr/cookies-et-autres-traceurs)
- [ANSSI - Guide d'hygiène informatique](https://www.ssi.gouv.fr/guide/guide-dhygiene-informatique/)

### Souveraineté numérique

- [Bases numériques d'intérêt général](https://lesbases.anct.gouv.fr/)
- [La Suite numérique et bien d'autres](https://www.proconnect.gouv.fr/services)

---

**Casse le tracking. Reprends le contrôle.** ❌🍪
