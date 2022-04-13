# Crear proyecto en github desde la terminal


#Intermedio

**Advertencia:** Si tratas con información sensible, nunca realices `git add`, `commit`, o `push` en un repositorio. La información sensible puede incluir, pero no se limita a:

- Contraseñas
- SSH keys (Claves SSH)
- Llaves API
- Números de tarjetas de crédito
- Números de NIP

Para obtener más información, consulta "[Eliminar datos confidenciales de un repositorio](https://docs.github.com/es/articles/removing-sensitive-data-from-a-repository)".

CLI de GitHub es una herramienta de código abierto para utilizar GitHub desde la línea de comandos de tu computadora. El CLI de GitHub puede simplificar el proceso de agregar un proyecto existente a GitHub utilizando la línea de comandos. Para aprender más sobre el CLI de GitHub, consulta la sección "[Acerca del CLI de GitHub](https://docs.github.com/es/github-cli/github-cli/about-github-cli)".

1. 
    
    En la línea de comandos, navega al directorio raíz de tu proyecto.
    
2.  Inicializar el directorio local como un repositorio de Git.
    
    `**git init -b main**`
    
3.  
    
    Para crear un repositorio para tu proyecto en GitHub, utiliza el subcomando `gh repo create`. Reemplaza a `project-name` con el nombre que deseas dar a tu repositorio. Si quieres que tu proyecto pertenezca a una organización en vez de a tu cuenta de usuario, especifica el nombre de la organización y del proyecto con `organization-name/project-name`.
    
    ```
    gh repo createproject-name
    ```
    
4. 
    
    Sigue los mensajes interactivos. Como alternativa, puedes especificar los argumentos para omitir estos mensajes. Para obtener más información sobre los argumentos posibles, consulta [el manual de CLI de GitHub](https://cli.github.com/manual/gh_repo_create).
    
5.  
    
    Extrae los cambios del repositorio nuevo que creaste. (Si creaste un archivo `.gitignore` o `LICENSE` en el paso anterior, esto extraerá dichos cambios en tu directorio local.)
    
    ```
    git pull --set-upstream origin main
    ```
    
6.  
    
    Prueba, confirma y sube todos los archivos de tu proyecto.
    
    ```
    git add . && git commit -m "initial commit" && git push
    ```
    
7. [Crear un repositorio nuevo](https://docs.github.com/es/articles/creating-a-new-repository) en GitHub.com. Para evitar errores, no inicialices el nuevo repositorio con archivos *README* licencia o `gitingnore`. Puedes agregar estos archivos después de que tu proyecto se haya subido a GitHub.
8. Abre la Terminal.
9. Cambiar el directorio de trabajo actual en tu proyecto local.
10. Inicializar el directorio local como un repositorio de Git. 
    
    ```
    $ git init -b main
    ```
    
11. Agregar los archivos a tu nuevo repositorio local. Esto representa la primera confirmación. 
    
    ```
    $ git add .
    # Agrega el archivo en el repositorio local y lo presenta para la confirmación. Para deshacer un archivo, usa 'git reset HEADYOUR-FILE'.
    ```
    
12. Confirmar los archivos que has preparado en tu repositorio local. 
    
    ```
    $ git commit -m "First commit"
    # Commits the tracked changes and prepares them to be pushed to a remote repository. Para eliminar esta confirmación y modificar el archivo, usa 'git reset --soft HEAD~1' y confirma y agrega nuevamente el archivo.
    ```
    
13. At the top of your repository on GitHub.com's Quick Setup page, click to copy the remote repository URL.
14. En Terminal, [agrega la URL para el repositorio remoto](https://docs.github.com/es/github/getting-started-with-github/managing-remote-repositories) donde se subirá tu repositorio local. 
    
    ```
    $ git remote add origin <REMOTE_URL>
    # Sets the new remote
    $ git remote -v
    # Verifies the new remote URL
    ```
    
15. [Sube los cambios](https://docs.github.com/es/github/getting-started-with-github/pushing-commits-to-a-remote-repository) en tu repositorio local a GitHub.com. 
    
    ```
    $ git push origin main
    # Pushes the changes in your local repository up to the remote repository you specified as the origin
    ```
    
- "[Agregar un archivo a un repositorio](https://docs.github.com/es/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)"