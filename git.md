## Show resume status
```
git status --short
```
## Submodulos
```
git submodule update --init --recursive
```
```
git submodule update --init --recursive --remote
```
## Mostrar o que não tá tracked
```
git clean -dnf
```
## Contem um commit
```
git branch -a --contains [Commit]
```
## Cherry-pick
```
git cherry-pick [Commit]
```
## Tag
```
git tag [TAG_NAME] -m "Test version for first access"
```
```
git push origin [TAG_NAME]
```
## Apagando a tag no repositório remoto
```
git push --delete origin [TAG_NAME]
```
## Apagando a tag no repositório local
```
git tag -d [TAG_NAME]
```
## Git LOG
### Vendo quais arquivos foram editados
```
git log --stat
```
### Vendo a edição dentro de cada arquivo
```
git log -p
```
## Git Diff
```
git diff <other_branch> -- <file_path>
```
## Limpeza e statsh de branch
```
git stash && git stash drop
```
```
git clean -f -d
```
## Criando novo branch
```
git checkout -b [Nome_branch] origin/develop
```