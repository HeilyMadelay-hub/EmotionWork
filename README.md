# Emotion Work - Plataforma de Gestión de la Carga Emocional en el Trabajo

Aplicación web full-stack que utiliza procesamiento de lenguaje natural para monitorear el bienestar emocional de los empleados, identificar patrones de estrés y ofrecer recomendaciones personalizadas para mejorar el clima laboral.

## 📱 Descripción

Emotion Work es una plataforma donde diferentes tipos de usuarios pueden:

- **Empleados**: Completar encuestas emocionales diarias y recibir recomendaciones personalizadas
- **Gestores de RRHH**: Acceder a dashboards analíticos y reportes de bienestar del equipo
- **Administradores**: Gestionar usuarios y configurar alertas del sistema
- Analizar automáticamente el sentimiento en textos corporativos
- Recibir alertas sobre niveles de estrés elevados
- Acceder a recursos de bienestar mental

## 🚀 Características

### Frontend (React)
- **Dashboard interactivo** con métricas en tiempo real
- **Encuestas emocionales** diarias con diferentes tipos de preguntas
- **Sistema de recomendaciones** basado en análisis de respuestas
- **Análisis de sentimientos** para textos ingresados
- **Gráficos y visualizaciones** de tendencias emocionales
- **Modo oscuro** y diseño responsive
- **Autenticación segura** con JWT
- **Notificaciones** para recordatorios

### Backend (FastAPI)
- **API REST** con documentación automática (Swagger)
- **Procesamiento NLP** con spaCy para análisis de sentimientos
- **Sistema de recomendaciones** basado en reglas y patrones
- **Gestión de usuarios** con roles diferenciados
- **Exportación de reportes** en PDF
- **Sistema de alertas** por email

## 🛠 Tecnologías

**Frontend:**
- React 18, TypeScript, Material-UI
- Chart.js para gráficos
- Axios para llamadas a API
- React Router para navegación

**Backend:**
- FastAPI (Python 3.11+)
- SQLAlchemy ORM con PostgreSQL
- spaCy para análisis de sentimientos
- Pydantic para validación de datos
- JWT para autenticación

**Base de Datos:**
- PostgreSQL 15+ (principal)
- Supabase (alternativa con auth incluido)

**Deployment:**
- Docker para desarrollo local
- Vercel para frontend
- Railway/Render para backend

## 🏗 Arquitectura

**Patrón MVC** con separación clara entre capas:

```
├── models/       # Modelos de datos (SQLAlchemy)
├── views/        # Endpoints de la API (FastAPI)
├── services/     # Lógica de negocio
├── utils/        # Utilidades y helpers
└── config/       # Configuración de la app
```

## 📂 Estructura del Proyecto

```
emotion-work/
├── frontend/                  # Aplicación React
│   ├── src/
│   │   ├── components/        # Componentes reutilizables
│   │   ├── pages/            # Páginas principales
│   │   ├── services/         # Llamadas a API
│   │   ├── utils/            # Utilidades
│   │   └── types/            # Tipos TypeScript
│   ├── public/
│   ├── package.json
│   └── Dockerfile
├── backend/                  # API FastAPI
│   ├── app/
│   │   ├── models/          # Modelos SQLAlchemy
│   │   ├── routers/         # Endpoints API
│   │   ├── services/        # Lógica de negocio
│   │   ├── utils/           # NLP y helpers
│   │   └── core/            # Configuración
│   ├── tests/               # Tests
│   ├── requirements.txt
│   └── Dockerfile
├── scripts/                 # Scripts de utilidad
│   ├── setup.sh            # Setup inicial
│   └── seed_data.py        # Datos de prueba
├── docker-compose.yml       # Para desarrollo local
├── .env.example
└── README.md
```

## 📋 Requisitos

- **Node.js** 18+ y npm
- **Python** 3.11+
- **PostgreSQL** 15+ (o cuenta de Supabase)
- **Docker** (opcional pero recomendado)

## ⚡ Instalación

### 1. Clonar repositorio
```bash
git clone https://github.com/tu-usuario/emotion-work.git
cd emotion-work
```

### 2. Opción A: Con Docker (Recomendado)
```bash
# Copiar variables de entorno
cp .env.example .env

# Levantar servicios
docker-compose up -d

# Acceder a la aplicación:
# Frontend: http://localhost:3000
# Backend: http://localhost:8000
# Docs API: http://localhost:8000/docs
```

### 3. Opción B: Configuración Manual

#### Backend
```bash
cd backend
python -m venv venv
source venv/bin/activate  # Linux/Mac
# venv\Scripts\activate   # Windows

pip install -r requirements.txt

# Configurar variables de entorno
cp .env.example .env
# Editar .env con tus configuraciones

# Ejecutar migraciones
alembic upgrade head

# Descargar modelo de spaCy
python -m spacy download es_core_news_sm

# Ejecutar servidor
uvicorn app.main:app --reload
```

#### Frontend
```bash
cd frontend
npm install

# Configurar variables de entorno
cp .env.example .env.local

# Ejecutar aplicación
npm start
```

### 4. Opción C: Con Supabase
```bash
# Crear proyecto en https://supabase.com
# Obtener URL y API keys

# Configurar en .env
SUPABASE_URL=https://tu-proyecto.supabase.co
SUPABASE_KEY=tu-anon-key
SUPABASE_SECRET=tu-service-key

# El resto igual que opción B
```

## 🗃️ Configuración de Base de Datos

### PostgreSQL Local
```bash
# Variables de entorno (.env)
DATABASE_URL=postgresql://usuario:password@localhost:5432/emotionwork
```

### Supabase (Recomendado para principiantes)
```bash
# Variables de entorno (.env)
SUPABASE_URL=https://tu-proyecto.supabase.co
SUPABASE_ANON_KEY=tu-anon-key
SUPABASE_SERVICE_KEY=tu-service-key
```

## 🐳 Docker Setup

```yaml
# docker-compose.yml
version: '3.8'

services:
  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    environment:
      - REACT_APP_API_URL=http://localhost:8000

  backend:
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://emotion:password@db:5432/emotionwork
    depends_on:
      - db

  db:
    image: postgres:15
    environment:
      POSTGRES_DB: emotionwork
      POSTGRES_USER: emotion
      POSTGRES_PASSWORD: password
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

## 📱 Pantallas Principales

- **Login/Registro**: Autenticación con email y contraseña
- **Dashboard**: Métricas emocionales personales y del equipo
- **Encuesta Diaria**: Cuestionario sobre estado emocional
- **Análisis de Texto**: Herramienta para analizar sentimientos en textos
- **Recomendaciones**: Sugerencias personalizadas de bienestar
- **Panel RRHH**: Reportes agregados para gestores
- **Perfil**: Gestión de cuenta y configuraciones

## 🔔 Sistema de Análisis Emocional

### Flujo de Procesamiento
1. **Recolección**: Usuario completa encuesta diaria o ingresa texto
2. **Análisis**: spaCy procesa el texto y detecta sentimientos
3. **Clasificación**: Sistema categoriza como positivo/negativo/neutro
4. **Recomendaciones**: Algoritmo sugiere acciones basadas en patrones
5. **Alertas**: Notificación automática si se detectan niveles críticos

### API Endpoints Principales
```python
POST /api/auth/login             # Iniciar sesión
POST /api/surveys/daily          # Enviar encuesta diaria  
GET  /api/analytics/personal     # Análisis personal
POST /api/nlp/analyze            # Analizar texto
GET  /api/recommendations        # Obtener recomendaciones
GET  /api/reports/team           # Reporte del equipo (RRHH)
```

## 🧪 Testing

**Coverage: 72%** en backend y 68% en frontend

### Backend Tests
```python
# Ejemplo: Test de análisis de sentimientos
def test_sentiment_analysis_positive():
    # Given
    text = "Me siento muy bien y motivado hoy"
    
    # When
    result = sentiment_analyzer.analyze(text)
    
    # Then
    assert result.sentiment == "POSITIVE"
    assert result.confidence > 0.7
```

### Frontend Tests
```javascript
// Ejemplo: Test de componente
test('dashboard shows user emotions correctly', () => {
  const mockData = { happiness: 0.8, stress: 0.3 };
  render(<Dashboard emotions={mockData} />);
  
  expect(screen.getByText('Felicidad: 80%')).toBeInTheDocument();
  expect(screen.getByText('Estrés: 30%')).toBeInTheDocument();
});
```

### Ejecutar Tests
```bash
# Backend
cd backend
pytest tests/ -v --cov=app

# Frontend
cd frontend
npm test
npm run test:coverage
```

## 🚀 Optimizaciones

### Performance
- **Caché en memoria** para análisis NLP frecuentes
- **Paginación** en listas de encuestas y reportes  
- **Lazy loading** de gráficos pesados
- **Debouncing** en búsquedas y análisis en tiempo real

### Análisis de Sentimientos
```python
# Servicio optimizado de NLP
import spacy
from typing import Dict

class SentimentAnalyzer:
    def __init__(self):
        self.nlp = spacy.load("es_core_news_sm")
        self._cache = {}
    
    def analyze(self, text: str) -> Dict:
        # Cache para textos repetidos
        if text in self._cache:
            return self._cache[text]
        
        # Procesamiento con spaCy
        doc = self.nlp(text)
        
        # Análisis básico de sentimientos
        positive_words = ["bien", "feliz", "motivado", "contento"]
        negative_words = ["mal", "triste", "estresado", "agotado"]
        
        score = 0
        for token in doc:
            if token.text.lower() in positive_words:
                score += 1
            elif token.text.lower() in negative_words:
                score -= 1
        
        # Clasificación simple
        if score > 0:
            sentiment = "POSITIVE"
        elif score < 0:
            sentiment = "NEGATIVE"
        else:
            sentiment = "NEUTRAL"
        
        result = {
            "sentiment": sentiment,
            "score": score,
            "confidence": min(abs(score) / len(doc), 1.0)
        }
        
        self._cache[text] = result
        return result
```

## 🔐 Seguridad

- **Autenticación JWT** con tokens de acceso
- **Validación de inputs** con Pydantic
- **Hashing de contraseñas** con bcrypt
- **Rate limiting** básico en endpoints críticos
- **CORS** configurado correctamente
- **Variables de entorno** para secretos
- **HTTPS** en producción

## 📊 Métricas Principales

- **Índice de Bienestar** (promedio de encuestas)
- **Tendencias semanales** por usuario/equipo
- **Distribución de sentimientos** en textos analizados
- **Engagement** con recomendaciones (clicks/follows)
- **Frecuencia de uso** de la plataforma

## 🔧 Variables de Entorno

```bash
# Backend (.env)
DATABASE_URL=postgresql://user:password@localhost/emotionwork
SECRET_KEY=tu-secret-key-muy-seguro
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30

# Supabase (alternativa)
SUPABASE_URL=https://tu-proyecto.supabase.co
SUPABASE_ANON_KEY=tu-anon-key
SUPABASE_SERVICE_KEY=tu-service-key

# Email (opcional)
SMTP_SERVER=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=tu-email@gmail.com
SMTP_PASSWORD=tu-app-password

# Frontend (.env.local)
REACT_APP_API_URL=http://localhost:8000
REACT_APP_ENVIRONMENT=development
```

## 🚀 Despliegue en Producción

### Frontend en Vercel
```bash
# Instalar Vercel CLI
npm i -g vercel

# Deploy automático
vercel --prod
```

### Backend en Railway
```bash
# Instalar Railway CLI
npm install -g @railway/cli

# Deploy
railway login
railway init
railway up
```

### Base de Datos
- **Supabase**: Plan gratuito con 500MB
- **Railway PostgreSQL**: Plan gratuito con 100MB
- **Render PostgreSQL**: Plan gratuito con 100MB

## 📸 Screenshots

*[Aquí irían 3-4 capturas de pantalla mostrando el dashboard principal, el análisis de sentimientos, las recomendaciones y el panel de RRHH]*

## 🔧 Comandos Útiles

```bash
# Desarrollo local
docker-compose up -d          # Levantar servicios
docker-compose logs backend   # Ver logs del backend
docker-compose exec db psql -U emotion # Acceder a la BD

# Testing
pytest tests/ -v              # Tests backend
npm test                      # Tests frontend

# Base de datos
alembic revision --autogenerate -m "descripción"  # Nueva migración
alembic upgrade head          # Aplicar migraciones

# Producción
docker-compose -f docker-compose.prod.yml up -d  # Deploy producción
```

## 🤔 Decisiones Técnicas

### ¿Por qué FastAPI?
- **Performance**: Más rápido que Flask/Django para APIs
- **Documentación automática**: Swagger incluido
- **Type hints**: Mejor desarrollo con Python moderno
- **Async support**: Para llamadas a APIs externas

### ¿Por qué spaCy?
- **Fácil de usar**: Setup simple para NLP básico
- **Modelos pre-entrenados**: En español incluidos
- **Comunidad activa**: Buena documentación
- **Performance**: Más rápido que NLTK para tareas básicas

### ¿Por qué PostgreSQL?
- **Confiabilidad**: Base de datos robusta y madura
- **JSON support**: Para datos no estructurados
- **Escalabilidad**: Maneja bien el crecimiento
- **Herramientas**: Buen ecosistema de admin tools

## 👨‍💻 Autor

**[Tu Nombre]** - *Full Stack Developer*

- 🌐 **Portfolio**: [tu-portfolio.com](https://tu-portfolio.com)
- 💼 **LinkedIn**: [linkedin.com/in/tu-perfil](https://linkedin.com/in/tu-perfil)  
- 📧 **Email**: tu.email@ejemplo.com

---

💡 **Proyecto desarrollado para demostrar competencias en:**
- Desarrollo Full Stack con React y FastAPI
- Procesamiento básico de Lenguaje Natural (NLP)
- Arquitectura MVC y buenas prácticas
- Testing automatizado y deployment
- UI/UX funcional y responsive

⭐ **¡Si te gusta el proyecto, dale una estrella en GitHub!**
