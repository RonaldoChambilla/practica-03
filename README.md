
# 🧠 Detección de Objetos en Tiempo Real con YOLOv4 y OpenCV

En este proyecto tenemos como objetivo implementar un sistema de detección de objetos en tiempo real utilizando la cámara web, haciendo uso del modelo **YOLOv4 preentrenado** junto a OpenCV pero salen varios errores al ejecutar la version base del pdf y aqui documento mi solucion.

## 🔁 Historia del problema y solución

### 🐞 Paso 1: Ejecución inicial del script del profesor

El primer intento fue ejecutar el código base de la guía práctica:

**Comando ejecutado:**

```
python codigo.py
```

**Resultado:**

```
ValueError: Value out of range
```

📷 *Captura del error original*  
 
`images/image1.png`

---

### 🔍 Paso 2: Diagnóstico del error

El error se presentó durante la descarga automática del archivo `yolov4.cfg`. Al investigar, descubrimos que se debía a la librería `progressbar`, que no soportaba correctamente el tamaño del archivo descargado, generando una excepción interna.

---

### 🛠️ Paso 3: Intento de solución actualizando progressbar2

Se ejecutó el siguiente comando para intentar solucionar el problema:

```
pip install --upgrade progressbar2
```

Esto permitió avanzar con la descarga, pero se presentó un nuevo error:

```
cv2.error: (-215:Assertion failed) separator_index < line.size()
```

Este nuevo error indicaba que el archivo `yolov4.cfg` se había descargado de forma corrupta o estaba mal formateado.

📷 *Captura del segundo error (cfg corrupto)*  

`images/image2.png`

---

### 🚫 Conclusión: el código original dependía de descargas automáticas poco fiables

Decidi reescribir el código para evitar depender de `cvlib` y manejar directamente la descarga y carga de los modelos YOLO de forma controlada.

---

## ✅ Solución final implementada

### 📁 Archivos necesarios (manual)

Se descargaron manualmente los siguientes archivos y se colocaron en la carpeta `model/yolo/`:

- `yolov4.cfg`  
  https://raw.githubusercontent.com/AlexeyAB/darknet/master/cfg/yolov4.cfg

- `coco.names`  
  https://raw.githubusercontent.com/pjreddie/darknet/master/data/coco.names

- `yolov4.weights` 
  https://pjreddie.com/media/files/yolov4.weights

📷 *Captura de como se agrego manualmente los archivos*  

`images/image3.png`
---

### 🧠 Script final (`codigo.py`)

Se implementó un nuevo script que:

- Carga la cámara web  
- Usa OpenCV y `cv2.dnn` para cargar el modelo YOLOv4  
- Detecta objetos en tiempo real como (personas, celulares, botellas etc.)
- Muestra etiquetas solo para objetos con más del 70% de confianza

### Capturas de evidencias finales respondiendo a las preguntas
- identificacion de objetos: 
📷 *Captura reconosiendo una botella*   
`images/image4.png`
📷 *Captura reconosiendo una persona*   
`images/image5.png`
📷 *Captura reconosiendo un celular*   
`images/image6.png`
- actividad:
📷 *Captura reconociendo una persona y un celular*   
`images/image7.png`
- personalizacion:
todas la pruebas anteriores ya cumplen con mostrar solo objetos con mas del 70 % de confianza.
📷 *Captura cambiando el color de las cajas*   
`images/image8.png`
---

## 🚀 Cómo ejecutar este proyecto

1. Clonar el repositorio:

```
git clone https://github.com/TU_USUARIO/TU_REPO.git
cd TU_REPO
```

2. Crear y activar un entorno virtual:

```
python -m venv tf-env
.	f-env\Scriptsctivate
```

3. Instalar dependencias:

```
pip install -r requirements.txt
```


4. Ejecutar el script:

```
python codigo.py
```

Presiona `ESC` para cerrar la ventana de detección.

---

## 📂 Estructura final del proyecto

```
.
├── codigo.py
├── requirements.txt
├── README.md
├── .gitignore
├── images/
│   ├── images.png
└── model/
    └── yolo/
        ├── yolov4.cfg
        ├── coco.names
        └── yolov4.weights  
```

---


---

**💡 Trabajo realizado.**  
Autor: [Ronaldo_Chambilla]
