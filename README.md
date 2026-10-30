# Prueba GIT    
```bash
##Creción archivo 0-
mkdir prueba_git
cd prueba_git
nano script.sh
    Escribo dentro el texto echo Listado completo ls -l
nano texto.txt
    Escribo dentro el texto uno dos tres
```
## Inicialización 1-
```bash
git init
    Sale esto Initialized empty Git repository in C:/Users/Miguel/prueba_git/.git/
##Comprobamos

$ git status
    Sale: On branch master
    No commits yet
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
            script.sh
            texto.txt
    
    nothing added to commit but untracked files present (use "git add" to track)

##Cambiamos el nombre a main
git branch -m main

##Cambiamos a master de vuelta
$ git branch -m master
```
## Añadir archivos 2-
```bash
##Añadir a archivos rastreados
$ git add script.sh
$ git status

##Hacemos un commit para sincronizar co los equipos remotos
git commit -m "Confirmación inicial"
##Para que funcione necesitamos una cuenta, que se crea con
$ git config --global user.email "macielalvarezn@gmail.com"
$ git config --global user.name "Miguel"
##Tras hacer esto si funciona el commit
$ git commit -m "Confirmación inicial"
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
            texto.txt

##Añadimos texto.txt y comprobamos su creación
git add texto.txt
git commit -m "Añadido archivo texto.txt"
git status
```
## Modificación de archivos 3-
```bash

##Entro a texto.txt y añado 4, posteriormente hago un status
$ git status
    Donde sale: 
     modified:   texto.txt
     
     no changes added to commit (use "git add" and/or "git commit -a")

##Si hacemos un add antes del status el mensaje cambiará a 
    modified:   texto.txt. De color verde

##Modifico texto.txt y hago un status, donde me sale
    modified:   texto.txt. De color rojo.

##Añadimos de nuevo texto
$ git add texto.txt
##Hacemos otro commit
$ git commit -m “Ampliada la explicación del texto”
    [master ac39b50] Ampliada la explicación del texto
     1 file changed, 2 insertions(+)

##Y comprobamos del vuelta el status 
$ git status
    modified:   texto.txt. De color verde
```
## Information -4
```bash

#Tática para resumir el add+commit
$ git commit -a -m “Nueva versión”
    On branch master
    nothing to commit, working tree clean

##Para ver la info
$ git show
    commit ac39b50aacbea6721f9ae1bdc202057b8a60fd63 (HEAD -> master)
    Author: Miguel <macielalvarezn@gmail.com>
    Date:   Fri Oct 30 11:13:22 2026 +0100
    
        Ampliada la explicación del texto
    
    diff --git a/texto.txt b/texto.txt
    index 15bf608..23c83ff 100644
    --- a/texto.txt
    +++ b/texto.txt
    @@ -1,3 +1,5 @@
     uno
     dos
     tres
    +cuatro
    +cinco


##Para ver los cambios a nivel histíco
$ git log
    commit ac39b50aacbea6721f9ae1bdc202057b8a60fd63 (HEAD -> master)
    Author: Miguel <macielalvarezn@gmail.com>
    Date:   Fri Oct 30 11:13:22 2026 +0100
    
        Ampliada la explicación del texto
    
    commit bef841939d15ba7b575b020e86354b9a6ff17a27
    Author: Miguel <macielalvarezn@gmail.com>
    Date:   Fri Oct 30 11:02:22 2026 +0100
    
        Añadido archivo texto.txt
    
    commit 330a524c4470306595e4b28eea899bbb66027e0a
    Author: Miguel <macielalvarezn@gmail.com>
    Date:   Fri Oct 30 10:57:23 2026 +0100
    
        Confirmación inicial
    
    commit 58ac40fe21cb92d2fcce1567860198850086ae84
    Author: Miguel <macielalvarezn@gmail.com>
    Date:   Fri Oct 30 10:55:06 2026 +0100
    
##Mostrar SOLO los objetos commit junto a su hash
$ git cat-file -p ac39b50
    tree ed545ddd6e32c946f3dca5de8058e12fe031840b
    parent bef841939d15ba7b575b020e86354b9a6ff17a27
    author Miguel <macielalvarezn@gmail.com> 1793355202 +0100
    committer Miguel <macielalvarezn@gmail.com> 1793355202 +0100
```
## Diferencias 5-
```bash
##Elimino la linea 3 de texto.txt y añado la 6, usamos el comando que nos permite ver las modificaciones recientes
$  git diff
    diff --git a/texto.txt b/texto.txt
    index 23c83ff..d9126ab 100644
    --- a/texto.txt
    +++ b/texto.txt
    @@ -1,5 +1,6 @@
     uno
     dos
    -tres
    +
     cuatro
     cinco
    +seis
    \ No newline at end of file
    
##Ejecutamos el comando que nos da información sobre lo añadido y eliminado
 git commit -a -m "Probando diff"
    [master f73c68c] Probando diff
    1 file changed, 2 insertions(+), 1 deletion(-)

##Añadimos la linea 7 (antes confirmamos con el commit)
$ git diff
    diff --git a/texto.txt b/texto.txt
    index 06582b9..be6d106 100644
    --- a/texto.txt
    +++ b/texto.txt
    @@ -4,4 +4,4 @@ dos
     cuatro
     cinco
     seis
    -
    +siete
```
## Ignorar archivos 6- 
```bash
Creamos Hola.java con su respectivo contenido, además de los txt importante y temporal. Lo haremos para probar los comandos de ignorar archivos
$ ls -a
    ./  ../  .git/  hola.java  importante.txt  script.sh  temporal.txt  texto.txt
##Ejecutamos el .java para que se cree el class+
$ javac hola.java

##Hacemos el respectivo
$ git status

    On branch master
    Changes not staged for commit:
     (use "git add <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
            modified:   texto.txt
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
            Hola.class
            hola.java
            importante.txt
            temporal.txt

##Creamos el .gitignore
nano .gitignore y lo rellenamos con: 

     ignora los archivos terminados en .class
    ##*.class
     ignora los archivos terminados en ~
    ##*~
     pero no importante~, aun cuando había ignorado los archivos 
    ##terminados en ~ en la linea anterior
    ##!importante~    
##Hacemos
git add .
## y su respetivo
    $ git commit -m "Añadidos fuentes en java y archivos importantes"
    [master d81ebab] Añadidos fuentes en java y archivos importantes
     5 files changed, 13 insertions(+), 1 deletion(-)
     create mode 100644 .gitignore
     create mode 100644 hola.java
     create mode 100644 importante.txt
     create mode 100644 temporal.txt
##Para ver todo
    git ls-tree --name-only -r HEAD
    $ git ls-tree --name-only -r HEAD
    .gitignore
    hola.java
    importante.txt
    script.sh
    temporal.txt
    texto.txt

```
## Tags 7- 
```bash
##Buscamos un hash para probar el comando
    git show ac39b50aacbea6721f9ae1bdc202057b8a60fd63
    commit bef841939d15ba7b575b020e86354b9a6ff17a27
    Author: Miguel <macielalvarezn@gmail.com>
    Date:   Fri Oct 30 11:02:22 2026 +0100

        Añadido archivo texto.txt

    diff --git a/texto.txt b/texto.txt
    new file mode 100644
    index 0000000..15bf608
    --- /dev/null
    +++ b/texto.txt
    @@ -0,0 +1,3 @@
    +uno
    +dos
    +tres

##Para añadir un tag
    git tag v0.7

##Forma resumida de escribir el log
    $ git log --oneline
    d81ebab (HEAD -> master, tag: v0.7) Añadidos fuentes en java y archivos importantes
    d2d7cdb Probando diff
    f73c68c Probando diff
    ac39b50 Ampliada la explicación del texto
    bef8419 Añadido archivo texto.txt
    330a524 Confirmación inicial
    58ac40f Confirmación inicial

##Cambiar a versión antigua
    $ git checkout v0.3
#Volver a la actual
    $ git checkout master

```
## Ramas 8- 
```bash

##Creación de la rama prueba 
    git branch Prueba

##Observamos la existencia de 2 ramas
    $ git log --oneline
    d81ebab (HEAD -> master, tag: v0.7, Prueba) Añadidos fuentes en java y archivos importantes
    d2d7cdb Probando diff
    f73c68c Probando diff
    ac39b50 Ampliada la explicación del texto
    bef8419 Añadido archivo texto.txt
    330a524 Confirmación inicial
    58ac40f Confirmación inicial

##Listado de ramas, trabajamos en *
    $ git branch
    Prueba
    * master

##Para cambiar de rama
    $ git switch Prueba
    Switched to branch 'Prueba'
    (El asterisco cambia de posición)


    $ git log --oneline
    d81ebab (HEAD -> Prueba, tag: v0.7, master) Añadidos fuentes en java y archivos importantes
    d2d7cdb Probando diff
    f73c68c Probando diff
    c39b50 Ampliada la explicación del texto
    bef8419 Añadido archivo texto.txt
    330a524 Confirmación inicial
    58ac40f Confirmación inicial


```
## Eliminar y quitar seguimiento 9- 
```bash

##Eliminamos archivo y hacemos su correspondiente commit 
    $ git rm importante.txt

    1 file changed, 0 insertions(+), 0 deletions(-)
    delete mode 100644 importante.txt

##Quitar seguimiento de archivos .class
    $ git reset HEAD *.class

```
## Repositorio remoto 10- 
```bash

##Clonar repositorio de Github
    $ git clone https://github.com/ColegioVivasCurro/HolaED
    Cloning into 'HolaED'...
    remote: Enumerating objects: 20, done.
    remote: Total 20 (delta 0), reused 0 (delta 0), pack-reused 20 (from 1)
    Receiving objects: 100% (20/20), done.
    esolving deltas: 100% (8/8), done.























