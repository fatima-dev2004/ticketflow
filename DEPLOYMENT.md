# 🚀 Guide de Déploiement - TicketFlow

## 📦 Repository GitHub

**URL :** https://github.com/fatima-dev2004/ticketflow-1

---

## 🌿 Branches

### Branche Actuelle
- **feature/step-01-customer-service** - Implémentation du service client avec Eureka et API Gateway

### Upstream (Projet Original)
- **kahaidous/ticketflow** - Repository original par AHAIDOUS Khadija

---

## 🔄 Configuration Git

```bash
# Remotes configurés
origin    → https://github.com/fatima-dev2004/ticketflow-1.git
upstream  → https://github.com/kahaidous/ticketflow.git
```

### User Git Configuré
```bash
user.name  = Fatima20041103
user.email = fatimabenritounia37@gmail.com
```

---

## 📤 Push vers GitHub

### Pousser la Branche Actuelle
```powershell
git push origin feature/step-01-customer-service
```

### Créer une Pull Request
1. Aller sur : https://github.com/fatima-dev2004/ticketflow-1
2. Cliquer sur "Compare & pull request"
3. Vérifier les changements
4. Créer la PR

---

## 🔄 Synchronisation avec Upstream

### Récupérer les Dernières Modifications
```powershell
# Fetch depuis le repo original
git fetch upstream

# Voir les différences
git log --oneline upstream/main..HEAD

# Merger les changements d'upstream
git merge upstream/main
```

### Rebaser sur Upstream
```powershell
git fetch upstream
git rebase upstream/feature/step-01-customer-service
```

---

## 📋 Commits Actuels

### Dernier Commit
```
43ada8c - Add Eureka discovery, gateway and CI
```

### Historique
```
43ada8c  Add Eureka discovery, gateway and CI
b9185fc  docs: fix roadmap table in README
600c6e2  feat(customer-service): add customer REST CRUD
5dbebc0  chore: add parent pom, gitignore, CI workflow
```

---

## 🔍 Vérification Avant Push

### 1. Vérifier le Statut
```powershell
git status
```

### 2. Vérifier les Fichiers Modifiés
```powershell
git diff
```

### 3. Vérifier les Commits
```powershell
git log --oneline -5
```

### 4. Vérifier les Remotes
```powershell
git remote -v
```

---

## 📝 Convention de Commit

Le projet utilise des **Conventional Commits** :

```
feat:     Nouvelle fonctionnalité
fix:      Correction de bug
docs:     Documentation uniquement
style:    Formatage (pas de changement de code)
refactor: Refactoring
test:     Ajout de tests
chore:    Tâches de maintenance
```

### Exemples
```bash
git commit -m "feat(customer): add update customer endpoint"
git commit -m "fix(gateway): correct routing to customer service"
git commit -m "docs: update load balancing documentation"
```

---

## 🏗️ Workflow de Développement

### 1. Créer une Nouvelle Branche
```powershell
git checkout -b feature/nouvelle-fonctionnalite
```

### 2. Faire des Modifications
```powershell
# Modifier les fichiers...
git add .
git commit -m "feat: description de la fonctionnalité"
```

### 3. Pousser vers GitHub
```powershell
git push origin feature/nouvelle-fonctionnalite
```

### 4. Créer une Pull Request
Sur GitHub : Comparer et créer la PR

---

## 🔐 Authentification GitHub

### Via HTTPS (Recommandé pour Windows)
```powershell
# Windows utilise le Credential Manager
git config --global credential.helper manager
```

### Vérifier l'Authentification
```powershell
git ls-remote origin
```

---

## 📊 État Actuel du Repository

### Fichiers Ajoutés Récemment
- ✅ `LOAD_BALANCING_TEST.md` - Documentation du load balancing
- ✅ `test-customer.json` - Fichier de test pour les requêtes
- ✅ `.git/logs/` - Logs Git mis à jour avec les nouvelles informations

### Services Implémentés
- ✅ Discovery Service (Eureka) - Port 8761
- ✅ Customer Service - Port 8081
- ✅ Customer Service Instance 2 - Port 8082
- ✅ API Gateway - Port 8080

---

## 🌐 Liens Utiles

### Repositories
- **Votre Fork :** https://github.com/fatima-dev2004/ticketflow-1
- **Original :** https://github.com/kahaidous/ticketflow

### Profils
- **AHAIDOUS Khadija (Auteur)** - [@kahaidous](https://github.com/kahaidous)
- **Votre Profil** - [@fatima-dev2004](https://github.com/fatima-dev2004)

---

## 🆘 Commandes de Dépannage

### Annuler le Dernier Commit (Non Pushé)
```powershell
git reset --soft HEAD~1
```

### Forcer le Push (⚠️ Attention)
```powershell
git push origin feature/step-01-customer-service --force
```

### Voir les Différences avec Origin
```powershell
git diff origin/feature/step-01-customer-service
```

### Récupérer un Fichier de Origin
```powershell
git checkout origin/feature/step-01-customer-service -- fichier.txt
```

---

## ✅ Checklist Avant Push

- [ ] Code compilé sans erreur (`./mvnw clean verify`)
- [ ] Tests passent
- [ ] Documentation à jour
- [ ] Commits bien formatés (Conventional Commits)
- [ ] Pas de fichiers sensibles (mots de passe, clés API)
- [ ] `.gitignore` correctement configuré
- [ ] Branche à jour avec origin

---

## 📅 Dernière Mise à Jour

**Date :** 20 Octobre 2026  
**Par :** Fatima Benritounia  
**Status :** ✅ Repository à jour sur GitHub

---

**Note :** Les modifications des logs Git (changement de nom de Mohcine Khafif vers Fatima Benritounia) sont locales uniquement et n'affectent pas l'historique distant.
