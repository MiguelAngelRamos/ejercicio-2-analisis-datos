# Curso de Análisis de Datos con Python

Este proyecto utiliza **pandas** y **numpy** para el análisis y limpieza de datos. A continuación se explica cómo preparar el entorno de desarrollo en Windows desde cero.

---

## ¿Por qué usar un entorno virtual?

Un entorno virtual (`venv`) es una carpeta aislada que contiene su propia instalación de Python y sus propias librerías. Esto evita conflictos entre proyectos: si el Proyecto A necesita `pandas 1.x` y el Proyecto B necesita `pandas 2.x`, cada uno vive en su propio entorno sin interferir con el otro ni con el Python global del sistema.

---

## PowerShell vs CMD — ¿cuál usar?

| Característica | PowerShell | CMD |
|---|---|---|
| Activación del entorno virtual | `.\venv\Scripts\Activate.ps1` | `venv\Scripts\activate.bat` |
| Soporte de scripts `.ps1` | Sí (nativo) | No |
| Soporte de scripts `.bat` | Sí (compatibilidad) | Sí (nativo) |
| Recomendado para este proyecto | **Sí** | Funciona, con advertencias |

> **Recomendación:** Usa **PowerShell** siempre que puedas. CMD no puede ejecutar scripts `.ps1` directamente y en algunas configuraciones la activación del entorno falla silenciosamente o muestra errores. PowerShell es el estándar moderno de Windows y el que mejor soporta el ecosistema Python.

---

## Requisitos previos

Antes de empezar, asegúrate de tener Python instalado. Verifica esto abriendo una terminal y ejecutando:

```
python --version
```

Deberías ver algo como `Python 3.10.x` o superior. Si no está instalado, descárgalo desde [python.org](https://www.python.org/downloads/) y **asegúrate de marcar la opción "Add Python to PATH"** durante la instalación.

---

## Paso 1 — Crear el entorno virtual

Abre una terminal en la carpeta raíz del proyecto (donde está este `README.md`).

### PowerShell

```powershell
python -m venv venv
```

### CMD

```cmd
python -m venv venv
```

> Este comando es idéntico en ambos terminales. Crea una carpeta llamada `venv` en el directorio actual. Puedes nombrarla diferente (ej. `env`), pero `venv` es la convención estándar y está en el `.gitignore` del proyecto.
>
> **¿Qué hace `-m venv`?** Le indica a Python que ejecute el módulo `venv` como un script. Este módulo viene incluido con Python 3.3+ y no necesita instalarse por separado.

---

## Paso 2 — Activar el entorno virtual

Este es el paso donde **PowerShell y CMD difieren** y donde CMD puede presentar problemas.

### PowerShell

```powershell
.\venv\Scripts\Activate.ps1
```

> Si ves el error `"la ejecución de scripts está deshabilitada en este sistema"`, es porque la política de ejecución de PowerShell está restringida. Ejecútalo así para resolverlo (solo la primera vez):
>
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```
>
> Este comando permite ejecutar scripts locales creados por ti sin necesidad de permisos de administrador. Luego vuelve a ejecutar la activación.

### CMD

```cmd
venv\Scripts\activate.bat
```

> En CMD se usa la barra invertida `\` (no `/`) y se llama al archivo `.bat`, no al `.ps1`. Si usas la ruta del archivo `.ps1` dentro de CMD, obtendrás un error porque CMD no entiende la sintaxis de PowerShell.

---

### ¿Cómo sé que el entorno está activo?

Cuando el entorno virtual está activado, el nombre del entorno aparece entre paréntesis al inicio del prompt de tu terminal:

```
(venv) PS C:\Users\Miguel\Desktop\curso-analisis-datos>
```

o en CMD:

```
(venv) C:\Users\Miguel\Desktop\curso-analisis-datos>
```

> Mientras veas `(venv)` al inicio, **todos los comandos `python` y `pip` que ejecutes trabajarán dentro del entorno aislado**, no en el Python global del sistema.

---

## Paso 3 — Instalar las dependencias

Con el entorno activo, instala las librerías necesarias para el ejercicio:

### PowerShell y CMD (idéntico en ambos)

```
pip install pandas numpy matplotlib seaborn
```

> `pip` es el gestor de paquetes de Python. Al estar el entorno activo, `pip` instala las librerías **dentro de `venv\Lib\site-packages\`**, no en el sistema global.
>
> Para verificar que se instalaron correctamente:
>
> ```
> pip list
> ```
>
> Deberías ver `numpy` y `pandas` en la lista junto a sus versiones.

### Instalar varias librerías a la vez (alternativa)

Si el proyecto crece, se puede crear un archivo `requirements.txt` con las dependencias y luego instalarlas todas con un solo comando:

```
pip install -r requirements.txt
```

El archivo `requirements.txt` tendría este contenido:

```
pandas
numpy
matplotlib
seaborn
```

---

## Paso 4 — Desactivar el entorno virtual

Cuando termines de trabajar, desactiva el entorno para volver al Python global del sistema.

### PowerShell y CMD (idéntico en ambos)

```
deactivate
```

> Este comando siempre funciona igual en ambos terminales porque `deactivate` es una función que el propio proceso de activación inyecta en la sesión de la terminal. No es un archivo externo, por eso no hay diferencias entre PowerShell y CMD aquí.
>
> Sabrás que se desactivó correctamente cuando el prefijo `(venv)` desaparezca del prompt.

---

## Resumen de comandos

| Acción | PowerShell | CMD |
|---|---|---|
| Crear entorno | `python -m venv venv` | `python -m venv venv` |
| Activar entorno | `.\venv\Scripts\Activate.ps1` | `venv\Scripts\activate.bat` |
| Instalar dependencias | `pip install pandas numpy` | `pip install pandas numpy` |
| Verificar instalación | `pip list` | `pip list` |
| Desactivar entorno | `deactivate` | `deactivate` |

---

## Estructura del proyecto

```
curso-analisis-datos/
├── venv/                           # Entorno virtual (no se sube a git)
├── empleados_technova_sucio.csv    # Dataset del ejercicio 1 (datos sucios)
├── empleados_technova_limpio.csv   # Resultado de la limpieza del ejercicio 1
├── empleados_technova_2024.csv     # Dataset ampliado (180 empleados) para ejercicios 2 y 3
├── departamentos.csv               # Segunda tabla, para enseñar merge/joins (ejercicio 2)
├── generar_datos.py                # Script que genera los datasets ampliados (semilla fija)
├── ejercicio_1.ipynb               # Guía 1 — Limpieza de datos
├── ejercicio_2.ipynb               # Guía 2 — Series, selección condicional y Data Wrangling
├── ejercicio_3.ipynb               # Guía 3 — Análisis Exploratorio de Datos (EDA)
└── README.md                       # Este archivo
```

---

## Tecnologías utilizadas

- **Python 3.10+**
- **pandas** — Manipulación y análisis de datos en estructuras tipo tabla (DataFrames)
- **numpy** — Operaciones matemáticas y manejo de arrays numéricos
- **matplotlib** — Librería base de gráficos en Python (ejercicio 3, EDA)
- **seaborn** — Gráficos estadísticos de alto nivel sobre matplotlib (ejercicio 3, EDA)
- **Jupyter Notebook** — Entorno interactivo para ejecutar el código paso a paso

---

## Ruta de aprendizaje del curso

| Guía | Tema | Dataset que usa |
|---|---|---|
| `ejercicio_1.ipynb` | Limpieza de datos (nulos, duplicados, formatos) | `empleados_technova_sucio.csv` |
| `ejercicio_2.ipynb` | Series, selección condicional y Data Wrangling (columnas, `apply`, `groupby`, merge/joins, pivotes) | `empleados_technova_2024.csv` + `departamentos.csv` |
| `ejercicio_3.ipynb` | Análisis Exploratorio de Datos: IDA, univariado y multivariado | `empleados_technova_2024.csv` |

> **Nota para el profesor:** los datasets de los ejercicios 2 y 3 se generan con `generar_datos.py`
> (semilla fija, siempre produce los mismos datos). Los datos tienen **patrones escondidos a propósito**
> (la educación y la antigüedad afectan el salario, TI trabaja remoto, los outliers de sueldo son de
> Gerencia) para que el EDA del ejercicio 3 descubra hallazgos reales, no ruido.
