# ChronoTrack-Mobile
Mobile version of the previously created project

## Technologies used:
- Basic views (Android Studio)
- Kotline
- RetroFit

## Folder structure:
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
