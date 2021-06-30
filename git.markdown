---
layout: page
title: Git
permalink: /tools/git
---

# Git cheat sheet

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
