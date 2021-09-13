# Git Cheatsheet
_(von Schorsch)_
## Initialisieren

```bash
git init								# initialisiert
git									# (macht wohl woodo - glaub ich aber nicht)
git add -A .								# fügt alle Dateien dem Repo hinzu
```



## Allgemein

```bash
git status 								# Status meiner lokalen Dateien
git branch [erstellen]							# Zeigt alle branches an [oder erstellt einen neuen]
git checkout der-branch							# Wechselt in den branch der-branch

git fetch								# holt sich die Branches (Dateien) von bitbucket
git merge								# ***blubb***
git pull								# git fetch + git merge

git branch -r								# Remote Branches auflisten
git checkout -b localbranchname origin/remotebranchname			# holt sich einen Remotebranch (falls er noch nicht Lokal zu sehen ist)
```



## Hotfix

```bash
git checkout master							# Hotfix immer vom master
git branch hotfix/was-auch-immer-zu-tun-ist				# neuen branch (Hotfix) erstellen
git checkout hotfix/was-auch-immer-zu-tun-ist				# in neuen branch wechseln

git add die/datei/die/geändert.wurde					# Dateien hinzufügen
git commit -m "Beschreibung"						# Dateien in neuen branch übernehmen mit Beschreibung
```

__Staging__

```bash
git checkout previewXXXX						# In preview-branch wechseln
git merge --no-ff hotfix/was-auch-immer-zu-tun-ist			# mit hotfix-branch mergen
git push								# auf github schieben

# SSH auf Server
git branch								# Schauen ob auf richtigem branch (previewXXXX)
git pull								# von github holen
```

__Live__

```bash
git checkout master							# In masterbranch wechseln
git merge --no-ff hotfix/was-auch-immer-zu-tun-ist			# mit hotfix-branch mergen
git push								# auf github schieben

# SSH auf Server
git branch								# Schauen ob auf richtigem branch (master)
git pull								# von github holen
```

## Release

```bash
git tag									# Zeigt alle Tags an

git checkout master							# in master Branch wechseln
git merge --no-ff release-1.2						# mit relese-1.2 Branch mergen
git tag -a 1.1.2 -m 'Release 1.1.2 - DSGVO Module'			# Erstellt einen neuen Tag
git show 1.1.2								# Zeigt Tag Infos an

git push								# pusht alles andere
git push --tags								# pusht die tags
```

## Nützliches

#### Tag anzeigen
```bash
git tag show 1.1.2							# Zeigt Informationen über angegebenen Tag
```

#### Dateien Vergleichen
```bash
git show HEAD:meine/Dat.ei | md5sum					# Holt sich letzten Stand und macht md5 drauf
md5sum meine/Dat.ei							# macht md5 auf lokale Datei -> Danach beide md5 vergleichen
```

#### History anzeigen
```bash
git log --pretty=oneline						# Zeigt den Log einzeilig formatiert an
```

#### Löschen von Branches
```bash
git push origin --delete branchname					# löscht remote
git branch -d branchname						# löscht lokal (-D falls force verwendet werden soll)
```

#### Name/E-Mail nachträglich ändern
```bash
git change-commits GIT_AUTHOR_NAME "old name" "new name"
git change-commits GIT_AUTHOR_EMAIL "old@email.com" "new@email.com" HEAD~10..HEAD	# nur die letzten 10 Commits
```

#### Repository überschreiben/ neu initialisieren
```bash
git init								# Git initialisieren
git remote add origin git@bitbucket.org:fdiecommerce/sozialbau.git					
# .gitignore erstellen/einfügen
# evtl Submodule einbinden
git add .								# alle Dateien Hinzufügen
git push -f https://schorschi@bitbucket.org/fdiecommerce/sozialbau.git master
```

#### Submodule einbinden
```bash
git submodule add git@bitbucket.org:fdiecommerce/burkhard.git ordner	# fügt neues Submodul hinzu
git submodule update --init --recursive					# aktuallisiert bereits bestehende Submodule
```

#### Remote Repository wechseln
```bash
git remote -v								# zeigt aktuelles Remote Repository
git remote set-url origin https://github.com/USERNAME/REPOSITORY.git	# wächselt das Repository
```

#### Änderungen in einem Branch parken (oder verwerfen - z.B. Wordpress Update)
```bash
git stash								# alle Änderungen kommen auf einen Stash -> sauberer Branch
```