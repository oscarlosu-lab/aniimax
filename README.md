# Aniimaster

Optimizador integral de producción y planificación del Hogar para **Aniimo**. Calcula la ruta más rápida y rentable para generar monedas del hogar, subir de nivel tu Casa rodante (RV), optimizar la colocación de instalaciones con múltiples unidades de almacenamiento y gestionar a tus Aniimos de forma eficiente.

> **Créditos y Agradecimientos:**  
> **Aniimaster** es una versión extendida y localizada al español basada en el extraordinario proyecto de código abierto [**Aniimax**](https://github.com/ae-bii/aniimax) creado por [**@ae-bii**](https://github.com/ae-bii). Expresamos nuestro sincero agradecimiento a su creador original por la concepción de la herramienta, su motor de resolución matemática con programación lineal (HiGHS) y la recopilación de datos de la comunidad.

---

## 🌟 Novedades y Mejoras en Aniimaster

1. **Traducción Integral al Español:**
   - Interfaz de usuario, explicaciones matemáticas del modelo lineal, guía paso a paso de ayuda, nombres de instalaciones, recetas y materiales completamente adaptados al español oficial del juego.
   - Botón de modo **Bilingüe (ES/EN)** para facilitar la consulta de nombres tanto en español como en inglés.

2. **Recomendador de Aniimos con Alternativas:**
   - Sugerencia automática del equipo óptimo de criaturas según las habilidades requeridas por tu plan de producción.
   - **Detección de criaturas no salvajes:** Si una criatura solo se consigue por evolución (ej. *Inferlupa*, que evoluciona de *Flameruff*), huevos u otros métodos no silvestres, el sistema muestra una advertencia y propone una **alternativa salvaje directa** con la misma aptitud y su ubicación exacta en el mapa.
   - Botón interactivo *"Usar alternativa"* para cambiar de criatura con un solo clic y filtro para *"Priorizar Aniimos salvajes"*.

3. **Soporte de Múltiples Unidades de Almacenamiento (UA):**
   - En el juego real, a medida que sube el nivel de RV se desbloquean más almacenes (hasta 3 en nivel 10, y más en niveles superiores).
   - El plano interactivo del hogar distribuye automáticamente las instalaciones optimizando los viajes de acarreo hacia la **Unidad de Almacenamiento más cercana**, reduciendo las distancias totales recorridas.

4. **Monitor de Nutrición y Autonomía AFK:**
   - Cálculo del consumo energético por minuto de la cuadrilla de trabajo activa.
   - Selector de platos de comida para estimar la duración exacta del comedero (1.000 raciones) en días y horas de autonomía sin supervisión.

5. **Banner de Métricas Clave (KPIs):**
   - Resumen visual rápido en la parte superior: Tasa neta de monedas, tiempo estimado para subir de RV, plazas de Aniimos ocupadas/libres y días de comida en comedero.

---

## 🚀 Características Principales

- **Modo Simple o Avanzado:** Configura tu hogar en un segundo eligiendo solo tu nivel de Casa rodante (RV), o personaliza en detalle la cantidad y nivel de cada instalación y módulo de mejora.
- **Resolución Matemática Exacta con HiGHS:** El motor formula un problema de Programación Lineal Entera Mixta (MIP) que considera parcelas completas, tiempos de riego, bonificaciones de personalidad (+20%), niveles de aptitud de Aniimos y solapamiento de edificios ambientales (Horno de calor, Unidad de enfriamiento y Lámpara solar).
- **Estrategia Doble:**
  - *Subir de nivel:* Calcula el camino óptimo para reunir los materiales y monedas requeridos para tu siguiente nivel de RV en el menor tiempo posible, teniendo en cuenta tus existencias actuales.
  - *Prioridades:* Establece y ordena tus metas de producción (Monedas del Hogar, EXP de Aniimo, Aniipods, Bloques de madera, Arena mineral o Puntos del Festival de la Luna).
- **Semillas y Costes Claros:** Desglose exacto de cuántas semillas comprar por ciclo y el coste neto de reposición.
- **Privacidad Total:** Todos los cálculos se realizan localmente en tu navegador; tus ajustes se guardan en el almacenamiento local y nunca se envían a ningún servidor externo.

---

## 💻 Ejecución y Desarrollo Local

### Requisitos Previos

- Navegador web moderno con soporte para WebAssembly (Chrome, Edge, Firefox, Safari).
- Python 3 (o cualquier servidor HTTP estático) para servir la carpeta localmente.
- Opcional para compilar el backend Rust / WASM:
  - [Rust](https://www.rust-lang.org/tools/install) (1.70 o superior)
  - `wasm-pack` (`cargo install wasm-pack`)

### Iniciar la Web en Local

1. Clona el repositorio:
   ```bash
   git clone https://github.com/oscarlosu-lab/aniimax.git
   cd aniimax
   ```

2. Inicia un servidor web local en la carpeta `web`:
   ```bash
   python -m http.server 8080 --directory web
   ```

3. Abre en tu navegador:
   ```text
   http://localhost:8080
   ```

### Compilar WebAssembly (si modificas código Rust)

```bash
# En Windows (PowerShell) o Linux/macOS:
wasm-pack build --target web --out-dir web/pkg
```

### Ejecutar Tests

```bash
# Validar traducciones y catálogos de idioma:
node tests/locale.test.mjs

# Tests del motor en Rust:
cargo test
```

---

## 📁 Estructura del Proyecto

```text
web/
├── index.html              # Interfaz de usuario de Aniimaster
├── app.js                  # Lógica del cliente, modales y coordinación de planes
├── aniimo-recommender.js   # Recomendador de Aniimos y gestor de alternativas salvajes
├── extra-features.js       # Monitor de nutrición, KPIs y utilidades bilingües
├── layout.js               # Algoritmo de distribución física del hogar y multi-almacén
├── layout-worker.js        # Web Worker para cálculo en segundo plano del plano
├── facility-config.js      # Definición de instalaciones, niveles de RV y almacenes
├── style.css               # Estilos y diseño visual responsive
├── data/                   # Datos datamine de criaturas, recetas y pedidos
├── locales/                # Catálogos de idiomas (es, en, ru, zh-TW)
├── pkg/                    # Binario compilado WebAssembly
src/
├── exact.rs                # Modelo matemático de optimización con HiGHS (LP/MIP)
├── coverage.rs             # Geometría de cobertura ambiental
├── optimizer.rs            # Planificador heurístico de respaldo
├── models.rs               # Estructuras de datos de recetas e instalaciones
└── wasm.rs                 # Puentes de comunicación JS <-> WebAssembly
```

---

## 📄 Licencia

Este proyecto se distribuye bajo la licencia **MIT**, en consonancia con la licencia del proyecto original [Aniimax](https://github.com/ae-bii/aniimax). Consulta el archivo [LICENSE](LICENSE) para más detalles.
