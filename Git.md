# GIT CHEAT SHEET


## Instalación 
🪟 En windows [descargar y ejecutar instalador oficial](https://git-scm.com/download/win)  
🐧 En linux `$ apt-get install git`  
🍏 En mac `$ xcode-select --install`   


## Configuración

- Configurar modo global: `git config --global <parametro> "valor"`
- Configurar para un único repositorio `cd <mi repo>` y 
    `git config <parametro> "valor"`

- Configuraciones principales:
    ``` c++
    git config --global user.name "<tu nombre>" // Nombre 
    git config --global user.email "<tu email>" // Correo
    git config --global core.editor "code" // VSCode como editor por defecto
    ```
- Comprobar configuración:
    ``` c++
    git config --list // Mostrar toda la configuración 

    git config --global --list // Config global de git
    git config --local --list // Config repo local (si existe)
    git config --system --list // Config del sistema (si existe)

    git config --list --show-scope // Mostrar toda la config con su origen

    git config <configuración> // Mostrar valor config particular
    ```
  
### Creación llave SSH
Podemos conectarnos a GitHub vía SSH, para generar esta clave:

1. Creamos la llave:
    ``` c++
        ssh-keygen -t rsa -b 4096 -C “tu@email.com”
        // Dejar ruta por defecto, pulsar enter
        // Asignar passphrase y pulsar enter
        // Se crearán dos llaves:
        //  - id_rsa     -> llave privada
        //  - id_rsa.pub -> llave pública
    ```
2. Ahora, desde la consola de GitBash comprobamos que el servidor de llaves ssh de Windows está activo
    > eval $(ssh-agent -s)
    Nos deberá aparecer el pid de agente activo

3. Añadir nuestra llave privada *id_rsa* al servidor de llaves ssh:
    ``` c++
        // ssh-add ruta-donde-guardaste-tu-llave-privada
        ssh-add ~/.ssh/id_rsa
    ```
4. Ya podemos registrar nuestra llave pública *id_rsa.pub* en GitHub


## Git de forma local

### Creación de repositorio
``` c++
git init // Inicializar repo en la carpeta actual
git init <nuevo-proyecto> // Crear carpeta e inicializar dentro el repo
```

### Comprobar estado del repositorio

``` c++
git status // Mostrar estado de los archivos
git status -s // Mostrar estado de los archivos de forma resumida
```

### Deshacer cambios

- Si has modificado un archivo o directorio previamente comiteado:
    ``` c++
    git restore archivo.cs // Restaurar fichero archivo.cs 
    git restore . // Restaurar todo el directorio
    git restore '*.cs' // Restaurar ficheros terminado en .cs
    ```
> [!WARNING]
> Con `git restore` perderás todos lo cambios

> [!NOTE]  
> El comando `git restore` está disponible a partir de la versión de Git 2.23. Anteriormente se utilizaba el comando `git checkout` pero aunque sigue disponible se desaconseja su utilización.

- Si el archivo o directorio no existía previamente (no rastreados por Git aún) tenemos dos opciones:
  - Eliminar los nuevos archivos con nuestro explorador de archivos
  - Utilizar el comando `git clean`
    ``` c++
    git clean -n // Muestra ficheros a borrar sin hacerlo (dry-run)
    git clean -f // Borra archivos sin rastrear
    git clean -d // Borra archivos y directorios sin rastrear
    git clean -i // Pregunta antes de borrar cada archivo
    ```  

