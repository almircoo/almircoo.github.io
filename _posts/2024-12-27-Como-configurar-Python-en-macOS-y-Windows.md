
Se detalla los pasos necesarios para configurar Python en sistemas operativos macOS y Windows.

---

## macOS

### Paso 1: Verificar si Python ya está instalado
1. Abre la aplicación **Terminal**.
2. Escribe el siguiente comando:
   ```bash
   python3 --version
   ```
   - Si ves un número de versión (por ejemplo, `Python 3.x.x`), Python ya está instalado.
   - Si no aparece, continúa con el siguiente paso.

### Paso 2: Instalar Python
1. Abre el navegador y visita [python.org](https://www.python.org/).
2. Descarga la última versión de Python compatible con macOS.
3. Abre el archivo `.pkg` descargado y sigue las instrucciones de instalación.

### Paso 3: Verificar la instalación
1. Abre la **Terminal**.
2. Escribe el siguiente comando:
   ```bash
   python3 --version
   ```
   Deberías ver la versión instalada de Python.

### Paso 4: Instalar un gestor de paquetes (pip)
1. Normalmente, `pip` se instala automáticamente con Python. Verifica escribiendo:
   ```bash
   pip3 --version
   ```
   - Si aparece la versión, puedes usar `pip`.
   - Si no, instala `pip` con el siguiente comando:
     ```bash
     curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
     python3 get-pip.py
     ```

### Paso 5: Configurar un entorno virtual (opcional pero recomendado)
1. Crea un entorno virtual con:
   ```bash
   python3 -m venv nombre_del_entorno
   ```
2. Activa el entorno virtual:
   ```bash
   source nombre_del_entorno/bin/activate
   ```
3. Para salir del entorno virtual, escribe:
   ```bash
   deactivate
   ```

---

## Windows

### Paso 1: Verificar si Python ya está instalado
1. Abre el símbolo del sistema (**cmd**) o **PowerShell**.
2. Escribe el siguiente comando:
   ```powershell
   python --version
   ```
   - Si ves un número de versión (por ejemplo, `Python 3.x.x`), Python ya está instalado.
   - Si no aparece, continúa con el siguiente paso.

### Paso 2: Instalar Python
1. Abre el navegador y visita [python.org](https://www.python.org/).
2. Descarga la última versión de Python para Windows.
3. Ejecuta el instalador y selecciona las siguientes opciones:
   - Marca la casilla **Add Python to PATH** antes de continuar.
   - Selecciona **Customize installation** si deseas especificar opciones adicionales.
4. Completa la instalación siguiendo las instrucciones en pantalla.

### Paso 3: Verificar la instalación
1. Abre **cmd** o **PowerShell**.
2. Escribe el siguiente comando:
   ```powershell
   python --version
   ```
   Deberías ver la versión instalada de Python.

### Paso 4: Instalar un gestor de paquetes (pip)
1. `pip` normalmente se instala automáticamente con Python. Verifica escribiendo:
   ```powershell
   pip --version
   ```
   - Si aparece la versión, puedes usar `pip`.
   - Si no, instala `pip` manualmente descargando el script `get-pip.py` de [aquí](https://bootstrap.pypa.io/get-pip.py) y ejecutándolo con:
     ```powershell
     python get-pip.py
     ```

### Paso 5: Configurar un entorno virtual (opcional pero recomendado)
1. Crea un entorno virtual con:
   ```powershell
   python -m venv nombre_del_entorno
   ```
2. Activa el entorno virtual:
   ```powershell
   nombre_del_entorno\Scripts\activate
   ```
3. Para salir del entorno virtual, escribe:
   ```powershell
   deactivate
   ```

---

¡Python está listo para ser utilizado en tu sistema! 🎉
