# Chatbot con FastAPI y Deep Learning

Este proyecto implementa un chatbot inteligente utilizando FastAPI para la API REST y un modelo de deep learning construido con TensorFlow/Keras.

## Requisitos Previos

- Python 3.8 o superior
- pip (gestor de paquetes de Python)
- Entorno virtual (recomendado)

## Instalación

1. **Clonar el repositorio**
```bash
git clone <url-del-repositorio>
cd <nombre-del-directorio>
```

2. **Crear y activar el entorno virtual**
```bash
# Windows
python -m venv venv
.\venv\Scripts\activate

# Linux/MacOS
python3 -m venv venv
source venv/bin/activate
```

3. **Instalar dependencias**
```bash
pip install -r requirements.txt
```

## Estructura del Proyecto
```
.
├── main.py           # Archivo principal de la API FastAPI
├── chatbot.py        # Lógica del chatbot
├── training.py       # Script de entrenamiento del modelo
├── intents.json      # Datos de entrenamiento
├── requirements.txt  # Dependencias del proyecto
└── README.md
```

## Preparación y Entrenamiento

### 1. Configurar los Datos de Entrenamiento
Antes de comenzar, asegúrate de que el archivo `intents.json` contiene tus datos de entrenamiento. Este archivo define las categorías y respuestas del chatbot:

```json
{
    "intents": [
        {
            "tag": "saludo",
            "patterns": ["Hola", "Buenos días", "Qué tal"],
            "responses": ["¡Hola!", "¡Bienvenido!", "¿En qué puedo ayudarte?"]
        },
        // Añade más categorías según necesites
    ]
}
```

### 2. Entrenar la Red Neuronal
Es **IMPORTANTE** entrenar el modelo antes de ejecutar la API. Sigue estos pasos:

1. Asegúrate de que el entorno virtual está activado
2. Ejecuta el script de entrenamiento:
```bash
python training.py
```

El entrenamiento generará tres archivos esenciales:
- `words.pkl`: Vocabulario procesado
- `classes.pkl`: Clases de intención
- `chatbot_model.h5`: Modelo entrenado

**Nota**: El entrenamiento puede tardar varios minutos dependiendo de la cantidad de datos y la configuración del modelo.

### 3. Verificar los Archivos Generados
Antes de continuar, verifica que se han generado correctamente:
```bash
# Windows
dir *.pkl *.h5

# Linux/MacOS
ls *.pkl *.h5
```

## Uso de la API

1. **Iniciar la API** (después del entrenamiento)
```bash
uvicorn main:app --reload
```
La API estará disponible en `http://localhost:8000`

2. **Documentación de la API**
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## Endpoints

### POST /chat/
Envía un mensaje al chatbot y recibe una respuesta.

**Request:**
```json
{
    "message": "Hola, ¿cómo estás?"
}
```

**Response:**
```json
{
    "response": "¡Hola! Estoy bien, ¿en qué puedo ayudarte?"
}
```

## Personalización

1. **Modificar el entrenamiento**
- Edita `intents.json` para agregar nuevas categorías y respuestas
- Ajusta los parámetros del modelo en `training.py`
- **Importante**: Después de modificar `intents.json`, debes volver a entrenar el modelo

2. **Ajustar el modelo**
Puedes modificar la arquitectura del modelo en `training.py`:
- Número de capas
- Número de neuronas
- Tasas de dropout
- Funciones de activación
- Parámetros de entrenamiento

## Solución de Problemas

Si encuentras errores al ejecutar la API, verifica:
1. Que el modelo está entrenado (existen los archivos .pkl y .h5)
2. Que el entorno virtual está activado
3. Que todas las dependencias están instaladas
4. Que los archivos de entrenamiento son consistentes

## Contribuir
1. Fork el repositorio
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## Licencia
Este proyecto está bajo la Licencia MIT - ver el archivo `LICENSE` para más detalles. 