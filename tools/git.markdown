---
layout: page
title: Git cheat sheet
exclude: true
---

## Basics

### Initializing

```bash
git clone https://github.com/hl191/hl191.github.io.git
```

### Daily business

```bash
git checkout .
```

```bash
git commit -m "Commit message"
```

```bash
git push
```

### Staging
Stage all changes
```bash
git add .
```
Unstage all files
```bash
git reset
```
Last commit back to staging area
```bash
git reset --soft HEAD^
```

### Tags

Delete all remote tags
```bash
git push origin --delete $(git tag -l)
```
Delete all local tags
```bash
git tag -d $(git tag -l)
```

## Migrating to a mono repository

To reduce pipeline runs and providing the flexibility for sharing code as modules, migrating to a mono repo is a good option.
Here are some helpful commands to do so.

Assumed directory structure
```
monorepo
service1
service2
```

Target directory structure
```
monorepo/
├── service1/
├── service2/
```

Make sure ur fellow developers are informed and not blocked by your migration.

```
cd service1
# Create a directory. This will be our subdirectory in monorepo
mkdir service1
# Move all files into the created directory
ls -a1 | grep -v ^service1 | xargs -I{} git mv {} service1
# Commit the move operation locally (no need to push)
git commit -m "Migrate to monorepo"

# Go into the mono repo
cd ../monorepo
# Add a new git remote which points to our local repository with the migrated directory structure
git remote add service1 ../service1

# Pull changes from master branch from service1 to our monorepo
git pull service1 master --allow-unrelated-histories

# Push monorepo with new content
git push
```

## Encountered problems and solutions:

### HTTP proxy settings

Show current proxy settings for Windows

```
netsh winhttp show proxy
```

Set git configuration

```bash
# All current global settings
git config --global --list

# View current settings
git config --global http.proxy
git config --global https.proxy

# Set the current proxy to http://127.0.0.1:1080
git config --global http.proxy 'http://127.0.0.1:1080'
git config --global https.proxy 'http://127.0.0.1:1080'

# delete the proxy
git config --global --unset http.proxy
git config --global --unset https.proxy
```

### SSL certificate problem
```
fatal: unable to access 'https://github.com/hl191/postgres-sql-playground.git/': SSL certificate problem: self signed certificate in certificate chain
```

Workaround for a self signed certificate in certificate chain when executing git commands:
```bash
git -c http.sslVerify=false clone https://github.com/hl191/hl191.github.io.git
```

Global setting
```bash
git config --global http.sslVerify false
```
