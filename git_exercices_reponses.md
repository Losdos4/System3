# Série d'exercices Git 

---

## Exercice 1 : Ajout et validation des modifications

### 1. Créer un fichier `notes.txt`
```bash
echo "Première ligne de mes notes Git." > notes.txt
```

### 2. Ajouter au suivi Git
```bash
git init          
git add notes.txt
```

### 3. Premier commit
```bash
git commit -m "feat: ajout du fichier notes.txt avec contenu initial"
```

### 4. Modifier et re-committer
```bash
echo "Deuxième ligne ajoutée." >> notes.txt
git add notes.txt
git commit -m "feat: ajout d'une nouvelle ligne dans notes.txt"
```


---

## Exercice 2 : Historique des modifications

### 1. Afficher l'historique
```bash
git log
# Version plus lisible :
git log --oneline --graph --all
```

### 2. Détails d'un commit spécifique
```bash
git show <commit_id>
```

---

## Exercice 3 : Annulation et suppression

### 1. Annuler une modification non validée 
```bash
echo "ligne non voulue" >> notes.txt

git status

git restore notes.txt
```

Si le fichier a déjà été ajouté avec `git add` :
```bash
git restore --staged notes.txt 
git restore notes.txt       
```

### 2. Supprimer le dernier commit 
```bash
echo "commit à supprimer" >> notes.txt
git add notes.txt
git commit -m "test: commit temporaire"

# Garder les modifications dans le working directory
git reset --soft HEAD~1

# Garder les modifications non indexées
git reset --mixed HEAD~1

# Supprimer définitivement les modifications
git reset --hard HEAD~1
```

---

## Exercice 4 : Travail collaboratif avec GitHub

### 1. Créer un dépôt sur GitHub
- Aller sur [github.com](https://github.com) → **New repository**
- Nom : `projet_git_remote`
- Laisser vide (ne pas initialiser avec README)
- Cliquer **Create repository**

### 2. Relier le dépôt local au dépôt distant
```bash
git remote add origin git@github.com:TON_USERNAME/projet_git_remote.git

# Vérifier la liaison
git remote -v
```

### 3. Pousser le code local vers GitHub
```bash
git push -u origin main
# Le -u définit origin/main comme branche de suivi par défaut
# Ensuite, git push suffit
```

### 4. Récupérer les modifications faites sur GitHub
```bash
# Modifier un fichier directement sur GitHub (via l'interface web)
# Puis en local :
git pull origin main
```

> `git pull` = `git fetch` + `git merge` : récupère ET fusionne les modifications distantes.

---

## Exercice 5 : Fichiers ignorés

### 1. Créer le fichier `secret.txt`
```bash
echo "mot_de_passe=1234" > secret.txt
```

### 2. Créer le `.gitignore` et ignorer `secret.txt`
```bash
echo "secret.txt" > .gitignore
```

Contenu du `.gitignore` :
```
# Fichiers sensibles
secret.txt

# Autres exemples courants
*.log
node_modules/
.env
__pycache__/
```

### 3. Vérifier que le fichier est ignoré
```bash
git status
# secret.txt ne doit pas apparaître dans "Untracked files"

# Pour confirmer explicitement :
git check-ignore -v secret.txt
# Résultat attendu : .gitignore:1:secret.txt    secret.txt
```

### Committer le `.gitignore`
```bash
git add .gitignore
git commit -m "chore: ajout du .gitignore"
---

## Exercice 6 : Clonage et collaboration

### 1. Cloner un dépôt existant
```bash
git clone git@github.com:USERNAME/NOM_DU_REPO.git

# Ou en HTTPS :
git clone https://github.com/USERNAME/NOM_DU_REPO.git

# Se placer dans le dossier cloné
cd NOM_DU_REPO
```

### 2. Faire une modification et la pousser
```bash
# Modifier un fichier
echo "Ma contribution" >> README.md

# Ajouter et committer
git add README.md
git commit -m "docs: ajout d'une contribution au README"

# Pousser vers le dépôt distant
git push origin main
```


