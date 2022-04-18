# Cuando Origin Master esta fuera de HEAD

Tags: Ramas

El problema ocurre cuando el repositorio remoto esta en otra rama o por fuera de la linea temporal del repositorio local. Normalmente debe estar de esta manera: 

![[cuando-origin.png]]

### Cuando `origin/master` está en otra rama o en conflicto

1. Nos ubicamos en master o main con **`git checkout main o master`**
2. `git merge origin/main` [Opcional]
3. **`git branch -u origin/main`** Para conectar origin/main a  main
4. **`git push`** Manda los cambios realizados