# Bienvenido

>Aquí encontrarás diccionarios enfocados en diferentes tecnologías para realizar fuzzing. 

---

## 🛠️ Clonar solo un subdirectorio con Git `sparse-checkout`

Este método permite clonar **solo una carpeta específica** (por ejemplo `wordlist`) de un repositorio grande sin tener que descargar todo.

### 🔧 Requisitos previos

- Tener **Git v2.25+** instalado.
- Acceso al repositorio que deseas clonar.

---

### 🚀 Pasos


#### 1. Clona el repositorio SIN descargar los archivos completos

```bash
git clone --filter=blob:none --no-checkout https://github.com/Josfull/josfull.github.io.git
```

#### 2. Entra al directorio clonado
```bash
cd josfull.github.io
```

#### 3. Inicializa el modo de checkout parcial ("sparse")
```
git sparse-checkout init --cone
```

#### 4. Indica qué subdirectorio deseas incluir (solo "wordlist" en este caso)
```
git sparse-checkout set wordlist
```
#### 5. Realiza el checkout de los archivos seleccionados
```
git checkout
```

---

### 📂 Resultado

Tras ejecutar estos comandos, solo tendrás descargado el contenido de `wordlist/`, sin el resto del repositorio.


---

## 🛠️ Descargar un archivo específico con `wget`

#### 1.Si quieres **descargar un archivo suelto** (por ejemplo, `example.txt` dentro de `wordlist`), ve al archivo en GitHub y copia la URL cruda (_raw_), que sería algo así:

```
https://raw.githubusercontent.com/Josfull/josfull.github.io/main/wordlist/example.txt
```

#### 2. lo descargas con:

```bash
wget https://raw.githubusercontent.com/Josfull/josfull.github.io/main/wordlist/example.txt
```

---

## Resumen

- **Para descargar el subdirectorio completo:** usa `git sparse-checkout`.
    
- **Para descargar un archivo individual:** usa la URL raw y `wget`.
    


---
⚠️ **Descargo de responsabilidad**: El contenido de este repositorio es solo para fines educativos e informativos; los autores no se hacen responsables de un uso indebido. Asegúrate de contar con la autorización adecuada antes de utilizarlo, actúa de forma responsable bajo tu propio riesgo y cumple todas las directrices legales y éticas.

---
