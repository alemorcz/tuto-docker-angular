# Guía Docker, Angular y pruebas
**1. Instalar Docker:**  
Asegúrate de tener Docker instalado en tu sistema. Puedes seguir la [Documentación oficial de Docker](https://docs.docker.com/get-started/get-docker/) para instalarlo según tu sistema operativo.  
**2. Descarga la imagen de Ubuntu:**
Ejecuta el siguienter comando para descargar la imagen oficial de Ubuntu:
```
docker pull ubuntu
```
***3. Crear un contenedor de Ubuntu:** 
Ejecuta el siguiente comando para crear un contenedor de Ubuntu:
1. La primera opción es para crearlo sin puerto.
2. La segunda opción es para crearlo con puerto y ayuda si se implementa un proyecto angular dentro del contenedor.
```
 docker run -it --name ubuntu-container ubuntu
 docker run -it -p 4200:4200 --name ubuntu-container ubuntu bash
 ```
 - -it: Permite interactuar con el contenedor.
 - --name: Asigna un nombre al contenedor.

**4. Configurar el contenedor de Ubuntu:** 
Una vez dentro del contenedor, actualiza el sistema y configura las herramientas necesarias:
```bash
apt update
apt upgrade
apt install nano
apt install curl
apt install wget
apt install git
apt install -y nodejs npm
npm install -g @angular/cli
apt install -y python3 python3-pip
```
**5. Salir del contenedor de Ubuntu:** 
Para salir del contenedor de Ubuntu, ejecuta el siguiente comando:
```bash
exit
```
**6. Guardar los cambios en una nueva imagen:** 
Una vez que hayas realizado las configuraciones necesarias, puedes guardar los cambios en una nueva imagen de Docker. Para ello, primero detén el contenedor:
```bash
 docker stop ubuntu-container
```
**7. Entrar de nuevo al contendor**
Si saliste del contenedor de Ubuntu, puede singresar de nuevo usando el siguiente comando:
```bash
docker start ubuntu-container
docker exec -it ubuntu-container bash
````

**8. Creación del Menú con bash:**  
En el contenedor colocar el siguiente código para crear un menu con bash. El archivo nombralo menu.sh.  
```bash
#!/bin/bash

while true; do
    clear
    echo "============================="
    echo "       MENÚ PRINCIPAL        "
    echo "============================="
    echo "1. Proyecto Angular"
    echo "2. Pruebas Unitarias"
    echo "3. Hola Mundo"
    echo "4. Salir"
    echo "============================="
    read -p "Seleccione una opción: " opcion

    case $opcion in
        1)
            echo "Iniciando el proyecto Angular..."
            cd /proyecto-angular || { echo "No se encontro el proyecto"; exit 1; }
            npm install
            ng serve --host 0.0.0.0 --port 4200
            ;;
        2)
            echo "Ejecutando pruebas unitarias con Jest..."
            cd /proyecto-angular || { echo "No se encontro el proyecto"; exit 1; }
            npx jest hola-test.spec.js
            ;;
        3)
            echo "Ejecutando script hola.hs..."
            if [ -f "./hola.sh" ]; then
                        ./hola.sh
            else
                echo "El script hola.sh no existe en la ruta actual."
            fi
            ;;
        4)
            echo "Saliendo del menú..."
            exit 0
            ;;
        *)
            echo "Opción no válida. Intente nuevamente."
            ;;
    esac
    read -p "Presione Enter para continuar..."
done
```
**9. Permisos de Ejecución:**
Para poder ejecutar el script, debes darle permisos de ejecución. Ejecuta el siguiente comando en la terminal:
```
chmod +x menu.sh
```
Esto permitirá que el script sea ejecutable.

**10. Ejecutar el script**
Para ejecutar el script, simplemente escribe el siguiente comando en la terminal:
```
./menu.sh
```
Esto mostrará el menú interactivo en la terminal y te permitirá seleccionar las opciones disponibles.

**PASOS PARA QUE EL MENÚ TENGA INTERACCIÓN**


```bash
#!/bin/bash
echo "Hola Mundo!"
```


```javascript
const { execSync } = require("child_process");
const fs = require("fs");

describe("Pruebas para hola.sh", () => {
    test("El archivo hola.sh debe existir", () => {
        expect(fs.existsSync("/hola.sh")).toBe(true);
    });

    test("El script debe imprimir 'Hola Mundo!'", () => {
        const output = execSync("/hola.sh").toString().trim();
        expect(output).toBe("Hola Mundo!");
    });
});

```
