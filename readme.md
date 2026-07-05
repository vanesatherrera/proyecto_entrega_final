# Proyecto de Automatizacion QA - Vanesa Herrera

## Descripcion

Proyecto de automatizacion de pruebas realizado con Python, Selenium WebDriver y Pytest.

El objetivo del proyecto es automatizar distintas pruebas funcionales de una aplicacion web.

## Tecnologias usadas
- Python
- Selenium WebDriver
- Pytest
- Pytest HTML
- Git

## Instalacion

`git clone https://github.com/vanesatherrera/Entrega_QA_Automation.git`


## Instalacion dependencias

`pip install -r requirements.txt`

## Entorno de pruebas

- **Navegador**: Chrome
- **URL de aplicacion**: https://www.saucedemo.com

## Funcionamiento de las pruebas

### Listado de pruebas

| Test | Descripcion |
|------|-------------|
| test_login | Valida que el inicio de sesion redirija correctamente al inventario |
| test_inventory | Verifica que el titulo de la pagina sea "Swag Labs" |
| test_api | Valida las pruebas de api |
| test_cart | Verifica el flujo completo de agregar un producto al carrito |

### Validaciones

- **Login**: Redireccion a inventario despues del login exitoso
- **Inventario**: Titulo correcto, productos cargados, elementos de UI visibles
- **Carrito**: Contador muestra "1", nombre del producto coincide con el seleccionado

## Ejecución de pruebas

```bash
# Ejecutar todas las pruebas
pytest

# Ejecutar todas las pruebas con reporte HTML
pytest --html=report.html

# Ejecutar una prueba específica
pytest test/test_cart.py

# Ejecutar únicamente las pruebas de API
pytest -m api

# Ejecutar las pruebas en modo verbose
pytest -v
```


