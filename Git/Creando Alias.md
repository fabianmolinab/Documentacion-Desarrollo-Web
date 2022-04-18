# Creando Alias para nuestros comandos

Puedes crear todo tipo de aliases, pero la condición es que solo funcionan dentro del repositorio git, es decir, **SOLO** para comandos que empiezan en “git” como (git status, git add, git commit, etc…) y puedes hacerlo globalmente o por repositorio

## Creando Alias Globales

`git config --global alias.[atajo] "[comando]"`

## Creando Alias por repositorio
**Dentro del repositorio**
`` git config alias.[atajo] "[comando]"``

## Ejemplo
`git config --global alias.lg "log --oneline --decorate --all --graph"`

Al escribir seria ⇒ `git lg`

## Eliminando Alias
`git config --global --unset alias.[nombre de alias]`