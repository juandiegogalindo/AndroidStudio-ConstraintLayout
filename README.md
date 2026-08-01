# Laboratorio ConstraintLayout - Android

## Descripción

Aplicación Android que implementa dos formularios funcionales utilizando **ConstraintLayout** como sistema de diseño de interfaces. El proyecto consta de una pantalla principal de navegación (`MainActivity`) que da acceso a dos formularios independientes:

1. **Formulario de envío de correo electrónico** (`EmailActivity`): captura destinatario, asunto y mensaje, y delega el envío a una aplicación de correo instalada en el dispositivo.
2. **Formulario de solicitud de compra de combustible** (`FuelActivity`): permite seleccionar un tipo de combustible, calcular el total según los galones ingresados y mantener un historial de registros en pantalla.

Ambos formularios se construyen exclusivamente con `ConstraintLayout`, aplicando restricciones horizontales/verticales, márgenes, alineaciones y `match constraints` (0dp) para lograr interfaces responsivas sin anidar múltiples layouts.

---

## Características

- Navegación entre pantallas (Activities) mediante Intents.
- Envío de correos usando un Intent implícito, delegando la acción a apps externas instaladas.
- Selector desplegable (`Spinner`) que actualiza el precio según el tipo de combustible elegido.
- Cálculo automático del total a pagar (galones × precio por galón).
- Historial de solicitudes registradas, acumulado en memoria durante la sesión.
- Validación básica de campos vacíos y de formato numérico, con retroalimentación mediante `Toast`.

---

## Tecnologías utilizadas

- Java 11
- Android SDK (compileSdk 36, minSdk 23, targetSdk 36)
- Android Studio + Gradle
- ConstraintLayout 2.1.4
- AndroidX (AppCompat, Activity, Material)

---

## Conceptos nuevos

Como es el primer proyecto Android que revisamos juntos, estos son los conceptos propios de este entorno que aparecen por primera vez en tus repos:

- **ConstraintLayout**: sistema de diseño de layouts de Android que posiciona los elementos mediante restricciones (constraints) relativas entre vistas o respecto al contenedor padre, en lugar de anidar `LinearLayout`/`RelativeLayout`. Permite jerarquías planas y más eficientes en el renderizado.
- **Activity y su ciclo de vida (`onCreate`)**: una `Activity` representa una pantalla de la aplicación. `onCreate()` es el primer método que se ejecuta al crearse la pantalla; ahí se infla el layout (`setContentView`) y se inicializan los componentes visuales.
- **Intent (explícito e implícito)**: un `Intent` es un objeto que describe una acción a realizar. Los *explícitos* indican la clase exacta a abrir (por ejemplo, navegar de `MainActivity` a `EmailActivity`); los *implícitos* describen una acción genérica (como `ACTION_SEND`) y el sistema operativo decide qué aplicación instalada puede resolverla.
- **`findViewById`**: método que enlaza en el código Java una vista definida en el XML del layout, a partir de su `id`, permitiendo manipularla programáticamente.
- **`Spinner` + `ArrayAdapter`**: el `Spinner` es un componente de selección desplegable. El `ArrayAdapter` es el intermediario que conecta una fuente de datos (en este caso, un `string-array` definido en `strings.xml`) con la vista del `Spinner`, indicando cómo debe mostrarse cada elemento.
- **`Toast`**: mensaje emergente breve y no interactivo que se muestra al usuario para dar retroalimentación (por ejemplo, errores de validación), y que desaparece automáticamente.
- **`AndroidManifest.xml`**: archivo de configuración central de la app; declara las Activities existentes y cuál de ellas es la pantalla de entrada (`LAUNCHER`) mediante el `intent-filter`.

---

## Estructura del proyecto

```
app/
 └── src/main/
      ├── java/co/edu/unipiloto/laboratorioconstraintlayouts/
      │     ├── MainActivity.java
      │     ├── EmailActivity.java
      │     └── FuelActivity.java
      │
      ├── res/
      │     ├── layout/
      │     │     ├── activity_main.xml
      │     │     ├── activity_email.xml
      │     │     └── activity_fuel.xml
      │     └── values/
      │           └── strings.xml
      │
      └── AndroidManifest.xml
```

---

## Instalación y ejecución

1. Clonar el repositorio:

```bash
git clone https://github.com/juandiegogalindo/AndroidStudio-ConstraintLayout.git
```

2. Abrir **Android Studio**.
3. Seleccionar **Open** y elegir la carpeta del proyecto.
4. Esperar la sincronización de **Gradle**.
5. Ejecutar en un emulador o dispositivo físico (requiere mínimo Android 6.0 / API 23).

---

## Imágenes de referencia

**Formulario de correo electrónico**

<img width="1135" height="517" alt="image" src="https://github.com/user-attachments/assets/69d71dd5-b1d8-46b6-9afe-c33da2561e0b" />

<img width="409" height="430" alt="image" src="https://github.com/user-attachments/assets/43962749-eee2-49cc-b3a0-b673b879c769" />

**Formulario de solicitud de compra de combustible**

<img width="1137" height="518" alt="image" src="https://github.com/user-attachments/assets/5d9c8a87-9658-4694-8f5b-b869502e84d8" />

<img width="406" height="492" alt="image" src="https://github.com/user-attachments/assets/87a5a2d0-753b-4c9e-bc8a-9c2ba1489093" />

---

## Limitaciones conocidas

- Los `strings.xml` de los formularios mezclan texto en inglés (`hints`, `labels`) con lógica y mensajes en español dentro del código Java; no hay una estrategia de internacionalización unificada.
- El historial de solicitudes de combustible (`FuelActivity`) se almacena solo en memoria (`ArrayList`); se pierde al cerrar la Activity o rotar la pantalla, ya que no hay persistencia (base de datos, `SharedPreferences`) ni manejo de `onSaveInstanceState`.
- El envío de correo depende de que el dispositivo tenga una app de correo instalada; si no existe ninguna, el `Intent.createChooser` no encuentra receptor y se captura mediante un bloque `try-catch` genérico.

---

## Autor

**Juan Diego Galindo**
Estudiante de Ingeniería de Sistemas
