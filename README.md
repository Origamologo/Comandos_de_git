# Apuntes de git
<br>
:octocat: Resumen de los comandos más importantes de git :octocat:

#
## 1.-PRINCIPALES RAMAS EN GIT
## 2.-CÓMO GENERAR Y USAR UNA LLAVE SSH
## 3.-CLONAR UN REPO
## 4.-CONSULTAR ARCHIVOS MODIFICADOS
## 5.-DESCARTAR CAMBIOS
## 6.-CÓMO HACER UN COMMIT
## 7.-EL ARCHIVO .gitignore
## 8.-ACTUALIZAR UNA RAMA CON LOS ÚLTIMOS CAMBIOS DE REMOTO
## 9.-VER LAS MODIFICACIONES REALIZADAS
## 10.-STAGE Y STASH
## 11.-MOVER COMMITS ENTRE RAMAS CON git cherry-pick
## 12.-ELIMINAR UN COMMIT
## 13.-CREAR, MODIFICAR Y ELIMINAR RAMAS CON git branch
## 14.-CÓMO UNIR DOS RAMAS EN UNA CON merge
## 15.-CREAR ETIQUETAS: TAGS
## 16.-CÓMO CONECTAR UN PROYECTO A UN REPOSITORIO GIT
<br>

### 1.-PRINCIPALES RAMAS EN GIT

-**Master**: código publicado en producción

-**Development**: donde se integra la nueva funcionalidad y se prueba antes de pasar a master. Esta rama se crea a partir de la Master

-**Features**: contienen una funcionalidad. Se crean a partir de Development para integrarse con ella al terminar el desarrollo

-**Hotfix**: para corregir errores en producción. Se crean desde la rama Master para integrarse de nuevo en Master y en Development
<br>
#
### 2.-CÓMO GENERAR Y USAR UNA LLAVE SSH

1.-**Generar la llave**:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ ssh-keygen
 
Podemos dejar la contraseña vacía. En caso contrario nos pedirá la contraseña cada vez que realicemos algún cambio en el repo.\
Esto genera dos archivos guardados en el directorio oculto /.ssh:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id_rsa: clave privada que no compartiremos bajo ningún concepto\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;id_rsa.pub: la clave que subiremos a nuestro repositorio\

2.-**Subir la llave a github**:\
Se va a Settings => ssh => New ssh key\
Le damos un nombre, copiamos el contenido de id_rsa.pub y hacemos clic en Add SSH key

Esto nos va a permitir clonar los repositorios a través de SSH
<br>
#
### 3.-CLONAR UN REPO
 
-**Método http**:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git clone <url_del_repo>
 
-**Método ssh**:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git clone <direccion_ssh_del_repo>
 
 
CREAR RAMAS
 
1.-Primero creamos la branch en nuestro equipo\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git checkout -b <nombre_rama>
 
2.-Después subimos los cambios al repo, enviando a origin la nueva rama\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git push --set-upstream origin <nombre_nueva_rama>
<br>
#
### 4.-CONSULTAR ARCHIVOS MODIFICADOS
 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git status\
Si cambiamos de rama y los cambios no están trakeados y no lo commiteamos los cambios en origin, se llevará el status a la rama a la que cambiemos
<br>
#
### 5.-DESCARTAR CAMBIOS
 
Todos los cambios que descartemos serán irrecuperables\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git chekout -- <nombre_archivo>
 
Si lo que queremos es descartar todos los cambios realizados en todos los archivos, no ir uno a uno\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git checkout -- .
<br>
#
### 6.-CÓMO HACER UN COMMIT
 
1.-Primero indicamos qué archivos queremos commitear\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git add . #Para indicar que queremos agregar todos

	1.1.-Si quisiéramos sacar un archivo del commit
 	        $ git reset HEAD <nombre del archivo>
 	Y otra opción para hacer lo mismo:
 	        $ git rm --cached <nombre_del_archivo>
 	
2.- Ahora hacemos el commit con -m para poder poner una breve descripción\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git commit -m "<el_comentario_que_quieras>"
 
3.-Finalmente hay que subir  los cambios a remoto (origin)\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git push origin <branch_name>
<br>
#
### 7.-EL ARCHIVO .gitignore
 
Nos sirve para decir qué archivos no queremos que suba a git.\
Basta con editarlo y poner el nombre de lo que queremos que ignore.\
Aplica en el directorio en el que está y de forma recursiva en todos los directorios que están dentro.\
Git no tiene en cuenta directorios vacíos.\
Le podemos decir que sólo tenga en cuenta los archivos del directorio raiz en el que se encuentra añadiendo / por ejemplo /*.txt
<br>
#
### 8.-ACTUALIZAR UNA RAMA CON LOS ÚLTIMOS CAMBIOS DE REMOTO

Si hay cambios en remoto nunca nos dejará subir nuestros commits si no hemos bajado los cambios a nuestro equipo.

Para bajar los cambios de remoto a nuestro ordenador:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git pull
 
Para comprobar si hay cambios en remoto:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git fetch

Si no nos deja bajar los cambios porque los tiene que mergear y no puede, tampoco nos dejaría hacer commits y tendríamos que modificar a mano el archivo que causa conflicto
<br>
#
### 9.-VER LAS MODIFICACIONES REALIZADAS

Sólo podemos ver las modificaciones de archivos que estén trackeados por git, primero hay que tenerlos commiteados\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git diff <nombre_del_archivo>
<br>
#
### 10.-STAGE Y STASH

El objetivo es poder guardar cambios que tenemos a medias para poder realizar algún cambio puntual sobre otra rama.\
Si realizamos cambios dentro de una rama e intentamos cambiar de rama sin haberlos commiteado, bien se llevará todos los cambios a la siguiente rama o bien te pedirá que hagas un commit. No nos interesa ninguna de las dos situaciones y para solucionarlo tenemos el stage y el stash.

1.-Pasamos por el stage con git add\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git add .

2.-Lo guardamos en el stash con git stash\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git stash

Y ahora ya no arroja cambios si hacemos un git status

3.-Para ver los cambios almacenados en el stash:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git stash list

4.-Para recuperar los cambios almacenados en el stash:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git stash apply <nombre_stash_del_stashlist>\
Poniendo '$ git stash apply' nos saca el último

5.-Para eliminar cambios del stash\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git stash drop <nombre_stash_del_stashlist>\
Si no ponemos el nombre, nos saca el último del stash
<br>
#
### 11.-MOVER COMMITS ENTRE RAMAS CON git cherry-pick

1.-Primero tenemos que identificar el commit que queremos mover dentro de la rama en la que está inicialmete:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git log

2.-Copiamos el código del commit

3.-Nos movemos a la rama de destino con git checkout

4.-En la rama de destino usamos el cherry-pick:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git cherry-pick <codigo_del_commit>

5.-El commit no se elimina de la rama original, simplemente se copia se copia a otra, así que finalmente hay que eliminar el que nos sobra. Ver el siguiente punto.
<br>
#
### 12.-ELIMINAR UN COMMIT

Sólo es recomendable eliminar un commit cuando lo hemos realizado solo en nuestro repositorio local.\
Los motivos más comunes son haber olvidado agregar un archivo al state para commitearlo más tarde o que hayamos commiteado una funcionalidad antes de terminarla.

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git reset HEAD\~1 # Con esto eliminamos el último commit, con un HEAD~2 sería el penúltimo

Pero lo anterior elimina sólo el commit, no los cambios realizados en el archivo.\
Para cargarnos todo, commit y cambios en el archivo, le decimos que es hard:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git reset --hard HEAD~1
<br>
#
### 13.-CREAR, MODIFICAR Y ELIMINAR RAMAS CON git branch

Para crear una rama nueva sin que nos mueva a ella:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git branch <nombre_rama_nueva>

Para ver todas las ramas que tenemos:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git branch -l

Para cambiar de nombre a una rama existente:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git branch -m <nombre_actual> <nuevo_nombre>

Para eliminar una rama tenemos que posicionarnos fuera de la que nos queremos cargar:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git branch -d <nombre de la rama>

Si hay archivos con cambios en la rama que vamos a eliminar no nos deja con -d y tenemos que poner -D:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git branch -D <nombre de la rama>

De este modo sólo borramos las ramas en local. Para borrarlas también en remoto:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git push origin --delete <nombre_rama_eliminar>
<br>
#
### 14.-CÓMO UNIR DOS RAMAS EN UNA CON merge

1.-Puede ser que git una las dos ramas sin ningún tipo de conflicto, mezclando el contenido de los archivos. Esto se llama Fast-forward:

	1.0.-Añadimos y commiteamos todos los cambios en las ramas que vamos a mergear
 
	1.1.-Nos vamos a la rama de destino
 
	1.2.-Mergeamos la rama que nos interesa con la que estamos situados
 
	        $ git merge <nombre_rama_a_mergear>
	
2.-Puede que tenga que mezclar dos versiones distintas del mismo archivo, por lo que nos pedirá que hagamos un commit:

	2.0.-Añadimos y commiteamos todos los cambios en las ramas que vamos a mergear
 
	2.1.-Nos vamos a la rama de destino
 
	2.2.-Mergeamos la rama que nos interesa con la que estamos situados
 
	2.3.-Da error, así que abrimos el archivo conflictivo en un editor de texto y encontraremos resaltados y marcados los cambios que no puede mergear. Los cambiamos a mano, añadimos los cambios y commiteamos.
	
3.-Puede que git pueda hacer el merge automáticamente pero nos pida commitear antes los cambios:

	3.0.-Añadimos y commiteamos todos los cambios en las ramas que vamos a mergear
 
	3.1.-Nos vamos a la rama de destino
 
	3.2.-Mergeamos la rama que nos interesa con la que estamos situados
 
	3.3.-Nos aparece un mensaje pidiéndonos que commiteemos los cambios para completar el merge. Guardamos y cerramos el editor donde nos sale el mensaje y listo.
<br>

#
### 15.-CREAR ETIQUETAS: TAGS

Conforme vamos creando nuevas funciones y las vamos integrando en la rama develop, iremos creando versiones de nuestra aplicación y esto lo hacemos con los tags.\
Los tags son necesarios para que podamos ir descargando versiones estables de nuestra aplicación.\
Una etiqueta apunta a un determinado commit de una rama.

Para hacer un tag del último commit:\
1.-Nos posicionamos en la rama donde queremos crear el tag\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git tag -a <nombre_tag> -m "<mensaje>" #Así creamos un tag que apunta al último commit de la rama en la que estamos

2.- Para ver los tags de la rama:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git tag -l

Para hacer un tag de un commit pasado:\
1.-Nos posicionamos en la rama donde queremos crear el tag\
2.-Identificar el commit que queremos taguear:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git log

3.-Hacemos el tag al id del commit:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git tag <nombre_tag> <id_tag>

También podemos borrar etiquetas:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git tag -d <nombre_de_la_etiqueta>

Para subir un sólo tag a remoto:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git push origin <nombre_tag>

Para subir todos los tags que tengamos:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git push --tags
<br>
#
### 16.-CÓMO CONECTAR UN PROYECTO A UN REPOSITORIO GIT

1.- Entramos en la carpeta del proyecto e iniciamos git:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git init

2.-Creamos un archivo, añadimos al stage y commiteamos para que nos aparezca la rama master (o main)

3.-Vamos a github y creamos un nuevo repositorio

4.-Volvemos a la terminal para conectar los repos\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git remote add origin <url_del_repo>

5.-Y finalmente pusheamos\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git push

6.- Si la rama en la que estamos no está en remoto:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git push --set-upstream origin <nombre_rama_local>

Tambíén puede ocurrir que queramos desconectar el repo del servidor para conectarlo a otro, por ejemplo:\
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$ git remote remove origin
