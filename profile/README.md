## Hola a todos 👋

```
En este archivo podrán encontrar algunos de los comandos útiles para trabajar con git y github, recuerda que  siempre puedes regresar a este archivo para consultar los comandos que necesites.
En caso de que no encuentres el comando que necesitas, puedes buscarlo en google o preguntar a un compañero y agregarlo a este archivo.
```

# Comandos básicos de git

1. git status
   > Este comando muestra los archivos que están en el stage y los que no, también muestra los archivos que no están siendo rastreados por git
2. git clone < url del repositorio >
   > Este comando clona un repositorio, la url del repositorio se puede copiar desde la web de github
3. git branch
   > Este comando muestra las ramas que hay en el repositorio, la rama que tiene un asterisco es la rama en la que se está trabajando
4. git checkout < nombre de la rama >
   > Este comando cambia de rama,
5. git checkout -b <nombre de la rama>
   > Este comando crea una rama y cambia a ella
6. git remote
   > Muestra la lista de remotos que hay en el repositorio
7. git remote add < nombre del remoto > < url del remoto >
   - ej. git remote add origin https://github.com/qwerty1234/curso-git.git
     > Este comando agrega un remoto al repositorio, el nombre del remoto es el nombre que se le quiera dar y la url es la url del repositorio remoto
8. git remote -v
   > Este comando muestra la lista de remotos que hay en el repositorio y la url de cada uno
9. git remote remove <nombre del remoto> (Elimina un remoto)
   > Este comando elimina un remoto del repositorio
10. git log (Muestra el historial de commits)
    > Este comando muestra el historial de commits, se puede usar el comando `git log --oneline` para mostrar el historial de commits en una sola linea
11. git reset --hard (Vuelve al estado anterior)
    > Este comando vuelve al estado anterior, se puede usar el comando `git reset --hard <hash del commit>` para volver a un commit especifico

```
Lo signos < > no se deben escribir en el comando, solo se escriben para indicar que se debe escribir el nombre del remoto o el nombre de la rama
```

## Subir cambios a Github

- [x] git add .
  > Este comando agrega todos los archivos modificados al stage, si se quiere agregar un archivo en especifico se debe usar el comando `git add <nombre del archivo>`
- [x] git commit -m"mensaje"
  > Este comando crea un estado de guardado con los archivos que están en el stage, el mensaje se recomienda que sea descriptivo de los cambios que se hicieron
- [ ] git pull origin < rama de la que se quieren traer cambios > ej. git pull origin master
  > El comando trae los cambios del repositorio remoto, es recomendable hacerlo antes de subir los cambios para evitar conflictos
- [x] git push origin < rama que se quiere enviar al remoto > ej. git push origin master
  > El comando sube los cambios al repositorio remoto, si se hizo el pull antes de subir los cambios no debería haber conflictos

```
Se recomienda hacer un pull antes de subir cambios para evitar conflictos, pero no es obligatorio.
Si se hace un pull y hay conflictos se debe resolver los conflictos antes de subir los cambios.
En algunas ocasiones puede surgir un error al subir cambios directos a la rama master, por esto se recomienda trabajar en una rama diferente y después unir las ramas en la web de github con un pull request.
```

> [!IMPORTANT]
> Si se trabaja en una rama diferente a la rama master se debe cambiar el comando `git push origin master` por `git push origin <nombre de la rama>`. Ej. `git push origin develop`. Este comando sube los cambios de la rama que se esta especificando (_la rama que se escribe en el comando_) a la misma rama en el repositorio remoto (_en caso de que la rama especificada no exista en el repositorio esta crea automáticamente_), **es importante recordar que el comando no sube la rama en la que se esta trabajando a la rama especificada, ej. puedes subir la rama develop con `git push origin develop` aunque estés trabajando en la rama bugs**

## Como hacer un pull request en github (unir ramas)

1. Ir a la web de github
2. Ir al proyecto en el que se quiere hacer el pull request
3. Si acabas de subir cambios a una rama que no es la rama master, github te va a mostrar un mensaje que dice "Compare & pull request" y un botón que dice "Compare & pull request", si no te muestra ese mensaje y ese botón, ve al paso 4
4. Ve a la rama que quiere unir a la rama master
5. Haz click en el dropdown que dice Contribute
6. Haz click en el botón que dice "Open pull request"
7. Puedes escribir un titulo y un mensaje para describir los cambios que se hicieron
8. Da click en el botón que dice "Create pull request"
9. Finalmente da click en el botón que dice "Merge pull request"
10. Con esto se unen las ramas y los cambios se ven reflejados en la rama master

## Como actualizar el servidor(back-end) de producción

1. En el servidor buscas la carpeta del proyecto
2. En la capeta abres una terminal, con botón secundario `git bash here`
3. En la terminal escribes `git pull github master` o `git pull origin master`, depende de como se haya configurado el remoto, algunos proyectos tienen mas de un remoto
4. Si el proyecto tiene mas de un remoto, se puede ver la lista de remotos con el comando `git remote -v`
5. Si en el proyecto se hizo algún cambio en producción y marca conflictos al hacer el pull request se debe resolver los conflictos **(consulta la siguiente sección)**
6. Si no hay conflictos, el servidor ya tiene los cambios actualizados
7. Por ultimo se debe reiniciar el servidor para que los cambios se vean reflejados
8. En una terminal con permisos de administrador se debe correr el comando `pm2 restart <id proyecto>`

```
Puedes ver la lista de los proyectos y sus ids con el comando `pm2 list` desde una terminal con permisos de administrador
```

## Como resolver conflictos

```
Cuando se hace un pull request y hay conflictos la terminal muestra un mensaje que dice "Automatic merge failed; fix conflicts and then commit the result.", esto significa que hay conflictos y se deben resolver antes de hacer el commit, el mensaje también dice "CONFLICT (content): Merge conflict in <nombre del archivo>" y muestra el nombre del archivo en el que hay conflictos.
```

1. Abre el archivo en el que hay conflictos
2. En el archivo se muestran los cambios que se hicieron en la rama actual y los cambios que se hicieron en la rama que se quiere unir
3. Si estas utilizando VS Code, te marcara con colores los cambios que se hicieron stage sera la rama 'actual' y rama 'incoming', ademas tendrás botones para aceptar los cambios de una rama o de la otra.
4. Si estas utilizando otro editor de texto, tendrás que resolver los conflictos manualmente, eliminando los cambios que no quieres y dejando los cambios que si quieres
5. Una vez resueltos los conflictos, debes regresar a la terminal y utilizar los siguientes comandos.
   - git add .
   - git commit -m"mensaje"
6. Con esto se resuelven los conflictos y se completa el pull request

## Como actualizar la webapp(front-end) de producción

1. Abres un terminal en la carpeta del proyecto puedes hacerlo con el botón secundario `git bash here` desde la carpeta del proyecto
2. Para actualizar los cambios en la webapp es completamente necesario utilizar el `git pull origin master`, ya que la webapp se actualiza con los cambios que tienes en tu maquina local, por lo que debes obtener los cambios del repositorio remoto que hicieron otros desarrolladores.
3. En la terminal escribes `npm run build` para compilar los cambios
4. Esto crea una carpeta llamada `codebase` en la carpeta del proyecto en caso de un proyecto de webix y una carpeta llamada `dist` en caso de un proyecto de react
5. WEBIX - Copias el contenido de la carpeta `codebase` y lo pegas en la carpeta `codebase` del servidor, reemplazando los archivos que ya estaban ahí
6. React - Copias el contenido de la carpeta `dist` y lo pegas en la carpeta raíz del servidor, reemplazando los archivos que ya estaban ahí (Elimina los archivos anteriores de ser necesario)
7. Por ultimo si los cambios no se ven reflejados puedes borrar el cache de tu navegador y recargar la pagina, o reiniciar el servicio desde ISS Manager en el servidor

---



<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
