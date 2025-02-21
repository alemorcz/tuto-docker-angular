# Guia Docker, Angular y pruebas
**1. Instalar Docker:**  
Asegúrate de tener Docker instalado en tu sistema. Puedes seguir la documentación oficial de Docker para instalarlo según tu sistema operativo.

** Creación del Menu con bash:**  
En el contenedor colocar el siguiente código para crear un menu con bash.  
```bash
#!/bin/bash

while true; do
    clear
    echo "============================="
    echo "       MEN ^z PRINCIPAL        "
    echo "============================="
    echo "1. Proyecto Angular"
    echo "2. Pruebas Unitarias"
    echo "3. Hola Mundo"
    echo "4. Salir"
    echo "============================="
    read -p "Seleccione una opci  n: " opcion

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
                echo "El script hola.hs no existe en la ruta actual."
            fi
            ;;
        4)
            echo "Saliendo del men  ..."
            exit 0
            ;;
        *)
            echo "Opci  n no v  lida. Intente nuevamente."
            ;;
    esac
    read -p "Presione Enter para continuar..."
done
```


```bash
#!/bin/bash
echo "Hola Mundo!"
```


```
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
