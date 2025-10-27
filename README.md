# ChronoTrack-Mobile
Mobile version of the previously created project

## Technologies used:
- Basic views (Android Studio)
- Kotline
- RetroFit

## Folder structure:
#### (This is just an example, the actual entities and services must be created)
```
ChronoTrack/
│
├── app/
│   ├── build.gradle
│   ├── proguard-rules.pro
│   └── src/
│       ├── main/
│       │   ├── AndroidManifest.xml
│       │   ├── java/
│       │   │   └── com/
│       │   │       └── chronotrack/
│       │   │           ├── data/
│       │   │           │   ├── api/
│       │   │           │   │   ├── ApiClient.kt
│       │   │           │   │   └── ApiService.kt
│       │   │           │   │
│       │   │           │   ├── models/
│       │   │           │   │   ├── User.kt
│       │   │           │   │   ├── Task.kt
│       │   │           │   │   └── AuthResponse.kt
│       │   │           │   │
│       │   │           │   └── repositories/
│       │   │           │       ├── AuthRepository.kt
│       │   │           │       └── TaskRepository.kt
│       │   │           │
│       │   │           ├── domain/
│       │   │           │   ├── models/          # Opcional si quieres separar los modelos de dominio de los de red
│       │   │           │   └── usecases/
│       │   │           │       ├── LoginUseCase.kt
│       │   │           │       └── GetTasksUseCase.kt
│       │   │           │
│       │   │           ├── contexts/             # Aquí entran tus “slices” o viewmodels compartidos
│       │   │           │   ├── AuthContext.kt
│       │   │           │   └── TaskContext.kt
│       │   │           │
│       │   │           ├── ui/
│       │   │           │   ├── auth/
│       │   │           │   │   ├── LoginActivity.kt
│       │   │           │   │   ├── RegisterActivity.kt
│       │   │           │   │   └── ForgotPasswordActivity.kt
│       │   │           │   │
│       │   │           │   ├── home/
│       │   │           │   │   ├── HomeActivity.kt
│       │   │           │   │   └── fragments/
│       │   │           │   │       ├── TaskListFragment.kt
│       │   │           │   │       └── CalendarFragment.kt
│       │   │           │   │
│       │   │           │   ├── components/      # Elementos UI reutilizables
│       │   │           │   │   ├── TaskItemView.kt
│       │   │           │   │   └── LoadingView.kt
│       │   │           │   │
│       │   │           │   └── theme/
│       │   │           │       ├── Colors.kt
│       │   │           │       ├── Typography.kt
│       │   │           │       └── Styles.kt
│       │   │           │
│       │   │           ├── utils/
│       │   │           │   ├── Constants.kt
│       │   │           │   └── Extensions.kt
│       │   │           │
│       │   │           └── ChronoTrackApp.kt     # Application class (para inicializar cosas globales)
│       │   │
│       │   └── res/
│       │       ├── layout/
│       │       │   ├── activity_login.xml
│       │       │   ├── activity_home.xml
│       │       │   ├── fragment_task_list.xml
│       │       │   └── fragment_calendar.xml
│       │       │
│       │       ├── values/
│       │       │   ├── colors.xml
│       │       │   ├── strings.xml
│       │       │   └── styles.xml
│       │       │
│       │       └── drawable/
│       │           └── ic_launcher_foreground.xml
│       │
│       └── test/
│           └── ...
│
└── build.gradle
```
- Data/ → Everything related to data access (Retrofit, network models, repositories).
- Domain/ → Use cases or business logic (ideal if you later use Clean Architecture).
- Contexts/ → Equivalent to your global state slices (you could use ViewModel + LiveData or StateFlow).
- Ui/ → Everything visual: activities, fragments, and reusable components.
- Utils/ → Helper functions, extensions, global constants.
- ChronoTrackApp.kt → Application class to initialize Retrofit, ViewModels, or dependencies with Hilt/Koin.

---
## ⚙️ Backend

El backend de **ChronoTrack** está construido con:

- **NestJS** (Node.js + TypeScript)
- **PostgreSQL** como base de datos relacional.
- Arquitectura de **3 capas (Controllers, Services, Repositories)**.
- Autenticación mediante **JWT**.
- Documentación y endpoints disponibles a través de **Swagger** (`/api/docs`).

### Ejemplo de endpoints
| Módulo | Método | Endpoint | Descripción |
|--------|---------|-----------|--------------|
| Auth | POST | `/auth/login` | Inicia sesión con email y password |
| Auth | POST | `/auth/register` | Crea un nuevo usuario |
| Tasks | GET | `/tasks` | Obtiene todas las tareas del usuario |
| Tasks | POST | `/tasks` | Crea una nueva tarea |
| Tasks | PATCH | `/tasks/:id` | Actualiza una tarea existente |
| Tasks | DELETE | `/tasks/:id` | Elimina una tarea |

---

## 🔌 Comunicación API

La app usa **Retrofit** con un `ApiService` para manejar las peticiones HTTP hacia el backend.

```kotlin
interface ApiService {
    @POST("auth/login")
    suspend fun login(@Body request: LoginRequest): Response<AuthResponse>

    @GET("tasks")
    suspend fun getTasks(@Header("Authorization") token: String): Response<List<Task>>
}
