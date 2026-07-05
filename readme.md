# Proyecto de Automatización QA - Vanesa Herrera

## Descripción

Proyecto de automatización de pruebas funcionales y de API para la aplicación web [SauceDemo](https://www.saucedemo.com) y la API [ReqRes](https://reqres.in). Implementa pruebas **UI** con Selenium WebDriver siguiendo el patrón **Page Object Model (POM)** y pruebas de **API** con Requests. Además incluye pruebas **BDD** con Behave.

## Tecnologías utilizadas

- Python 3.13
- Selenium WebDriver
- Pytest
- Pytest-HTML (reportes)
- Pytest-check (aserciones suaves)
- Requests (API)
- Behave (BDD)
- WebDriver Manager
- GitHub Actions (CI/CD)
- Logging

## Instalación

```bash
git clone https://github.com/vanesatherrera/proyecto_entrega_final.git
```

```bash
pip install -r requirements.txt
```

## Entorno de pruebas

- **Navegador**: Chrome (headless)
- **URL UI**: https://www.saucedemo.com
- **URL API**: https://reqres.in

## Estructura del proyecto

```
├── .github/workflows/     # CI/CD con GitHub Actions
├── data/                  # Datos de prueba (CSV, JSON)
├── features/              # Pruebas BDD con Behave
│   ├── steps/             # Definiciones de pasos
│   └── login.feature      # Escenarios de login
├── logs/                  # Logs generados por las pruebas
├── page/                  # Page Object Model
│   ├── login_page.py
│   ├── inventory_page.py
│   └── cart_page.py
├── reports/screenshots/   # Capturas en fallos
├── test/                  # Pruebas automatizadas (Pytest)
│   ├── test_login.py
│   ├── test_login_csv.py
│   ├── test_inventory.py
│   ├── test_cart.py
│   ├── test_cart_json.py
│   └── test_api.py
├── utils/                 # Utilidades
│   ├── data_reader.py     # Lectura de CSV y JSON
│   └── logger.py          # Configuración de logging
├── conftest.py            # Fixtures globales de Pytest
├── behave.ini             # Configuración de Behave
└── pytest.ini             # Configuración de Pytest
```

## Pruebas

### Tests UI (Selenium + Pytest)

| Test | Marcador | Descripción |
|------|----------|-------------|
| `test_login_ok` | `smoke` | Login exitoso redirige a `/inventory.html` |
| `test_login_invalid_password` | — | Login con contraseña inválida muestra mensaje de error |
| `test_login` (parametrizado) | — | Login parametrizado con datos desde `data/users.csv` (válidos e inválidos) |
| `test_inventory_title` | — | Verifica que el título de la página sea "Swag Labs" |
| `test_productos_visibles` | `smoke` | Verifica que los productos estén cargados en inventario |
| `test_ui_elements` | — | Verifica que el menú hamburguesa y el filtro de productos estén visibles |
| `test_cart` | `smoke` | Agrega un producto al carrito, verifica contador (1) y nombre del producto |
| `test_cart_json` | — | Agrega múltiples productos desde `data/products.json` y valida nombre y precio en el carrito |

### Tests API (Requests + Pytest)

| Test | Marcador | Descripción |
|------|----------|-------------|
| `test_login_valido` | `api`, `smoke` | POST `/api/login` — credenciales válidas → 200 |
| `test_login_sin_password` | `api` | POST `/api/login` — sin password → 400 "Missing password" |
| `test_login_sin_email` | `api` | POST `/api/login` — sin email → 400 "Missing email or username" |
| `test_create_user` | `api` | POST `/api/users` — creación de usuario → 201, validaciones con pytest-check |
| `test_delete_user` | `api` | DELETE `/api/users/2` → 204 |
| `test_get_user` | `api` | GET `/api/users/2` → 200, tiempo de respuesta < 1s |

### Tests BDD (Behave)

Escenarios en español definidos en `features/login.feature`:

- **Login exitoso** — flujo positivo
- **Login inválido** — contraseña incorrecta
- **Scenario Outline** — login inválido con múltiples combinaciones (usuario vacío, contraseña vacía, etc.)

## Ejecución de pruebas

```bash
# Ejecutar todas las pruebas (Pytest)
pytest

# Con reporte HTML
pytest --html=report.html

# Por marcador
pytest -m smoke          # Pruebas críticas
pytest -m api            # Solo pruebas de API
pytest -m regression     # Pruebas de regresión
pytest -m ui             # Solo pruebas de UI

# Una prueba específica
pytest test/test_cart.py

# En modo verbose
pytest -v

# Pruebas BDD con Behave
behave
```

## CI/CD

El repositorio cuenta con un pipeline en **GitHub Actions** (`.github/workflows/test.yml`) que ejecuta todas las pruebas de Pytest automáticamente al hacer push a la rama `main` y guarda el reporte HTML como artefacto descargable.

## Reportes

- **HTML**: `report.html` (generado automáticamente por pytest-html)
- **Capturas**: `reports/screenshots/` (se toman automáticamente cuando falla una prueba de UI)
- **Logs**: `logs/` (archivos con timestamp por ejecución)

## Datos de prueba

- `data/users.csv` — usuarios y contraseñas con indicador `valid` para pruebas de login
- `data/products.json` — productos con nombre y precio para pruebas de carrito

## Fixtures (conftest.py)

- `driver` — inicializa Chrome en modo headless e incógnito
- `driver_logged` — inicia sesión con el primer usuario válido del CSV
