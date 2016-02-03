# How to Use Git and GitHub

# Configurando Ambiente

## Instalando no Ubuntu

```bash
$ sudo apt-get install git
$ git --version
```
## Configuração inicial de usuário

```bash
$ git config --global user.name "Leonardo Eiji Koshimura"
$ git config --global user.email "leonardo.koshimura@gmail.com"
```

para verificar
```bash
$ git config --get user.name
$ git config --get user.email
```

# Scaffolding

```bash
$ cd [diretório-do-projeto]
$ git init
$ touch .gitignore
$ git add .gitignore
$ git remote add origin git@bitbucket.org:lekoshimura/hello_app.git
```

# Repositório Remoto - Configuração e Uso

## Configuração inicial de repositório remoto

Adicionar chave ao bitbucket ou github e criar repositório remoto. Ver: [Generating SSH Keys.pdf](GeneratingSSHKeys.pdf)
```bash
$ git remote add origin git@bitbucket.org:lekoshimura/hello_app.git
$ git push -u origin --all # pushes up the repo and its refs for the first time
$ git push -u origin --tags # pushes up any tags
```

## Clonar de repositório remoto

```bash
$ git clone git@bitbucket.org:lekoshimura/hello_app.git
```

# Commit

```bash
# Adicionar ao staging area
$ git commit -m "Initialize repository"
```

```bash
# Isso:
$ git commit -am "mensagem"

# pode ser substituído por:
$ git add .
$ git commit -m "mensagem"
```

# Reset

```bash
# Apaga último commit. ATENÇÃO: o que está gravado no
# working diretory é substituído pelo penúltimo commit.
$ git reset --hard HEAD^
```

```bash
# Reverte todas as alterações do working directory
# e da staging area. Fica tudo igual ao que está no último commit.
$ git reset --hard
```

# Log

```bash
# Só os dois últimos commits
$ git log -n 2

# Listagem dos commits completa: data, autor e
# lista de arquivos incluídos, modificados e excluídos
$ git log --stat

# listagem simplificada dos commits
$ git log --oneline
```

# Diff

```bash
# Lista diferença entre working dir e stage
# area (mudanças não rastreadas)
$ git diff

# Lista diferença entre stage area e
# repositório (mudanças rastreadas)
$ git diff --staged

# Lista diferenças entre commits
$ git log --oneline -n 3
4e37299 Diminuido o intervalo de troca de banner
0a1c4cf Banner ao abrir a página
869484e Inserindo arquivo principal.js

$ git diff 869484e..4e37299

# Diff pode ser usado para ver diferenças entre commits e/ou branches
$ git diff [nome-do-branch1] [nome-do-branch2]

# Diff com listagem dos nomes do arquivos que têm diferenças
# entre 2 branches diferentes.
$ git diff --name-status master..branchName

# Show: faz um diff do commit com seu pai.
$ git show [ID-do-commit]
```

# Checkout

```bash
# Alterna para o brach master
$ git checkout master

# Recupera um commit
$ git checkout 654b654d54fa5d54a6a654a54a

# Recupera arquivo do staging area
$ git checkout -f
```

# Branch

Pense em branch como um label para um conjunto de commits. Quando um branch é apagado, os commits referentes a ele permanecem.

```bash
# Criar um branch e alterna para o branch criado.
$ git branch [nome-do-branch]
$ git checkout [nome-do-branch]

# Criar um branch e alterna para ele.
$ git checkout -b [nome do branch]

# Lista os branches existentes com destaque para o atual
$ git branches

# Mostra árvore de commits alinhados com seus branches.
# A listagem dos commits ($ git log) é ordenada por data.
# Assim, os commits que vieram de branches diferentes vão aparecer
# intercalados. Para ver a diferença de um commit para sua versão
# anterior (no mesmo branch) use $ git show [ID do commit]
$ git log --graph --oneline master [outro branch]
```

## Fundir branch

```bash
# Verificar se você está no branch master:
$ git branch
coins
easy-mode
*master

# Se você não estiver no branch master:
$ git checkout master

# Fazer o merge:
$ git merge master coins
```

## Apagar branch

```bash
# Cuidado: o git não pede confirmação antes de apagar.
$ git branch -d [nome-do-branch]
Deleted coins branch
```
# Remote e Push

```bash
# OOs guias dizem para fazer assim depois de criar o repositório:
$ git remote add origin https://github.com/lekoshimura/repository.git
# mas o git fica pedindo usuário e senha.

# If you already have your SSH keys set up and are still getting the
# password prompt, make sure your repo URL is in the form
# git+ssh://git@github.com/username/reponame.git
# as opposed to
# https://github.com/username/reponame.git
# To see your repo URL, run:
# git remote show origin
# You can change the URL with:
# $ git remote set-url origin git+ssh://git@github.com/username/reponame.git

# Para enviar os commits ao repositório:
$ git push origin master
```
# Fetch

O "git fetch" faz um pull no branch "origin/master" e evita que o último commit do "master" (no repositório local) seja sobrescrito.

```bash
$ git fetch origin
$ git log origin/master
$ git diff origin/master master
```

```bash
$ git pull origin master
# é o mesmo que:
$ git fetch origin
$ git merge master origin/master
```

# Editar

$ git mv arq1.txt arq2.txt

## Forçar o merge de um branch no master

Bom para recuperar um master que está estragado.

```bash
$ git checkout [branch "saudável"]
$ git merge -s ours master
$ git checkout master
$ git merge [branch "saudável"]
```

## Clonar um repositório numa máquina sem git(bitbucket) configurado

```bash
$ sudo apt-get install xclip
$ xclip -sel clip < ~/.ssh/id_rsa.pub
$ git clone git@bitbucket.org:lekoshimura/sample_app.git
```

# Bibliografia

http://sethrobertson.github.io/
http://git-scm.com/book/pt-br/v1 e http://git-scm.com/book/en/v2
