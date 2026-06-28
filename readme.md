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
| test_login_validation | Valida que el inicio de sesion redirija correctamente al inventario |
| test_inventory_title | Verifica que el titulo de la pagina sea "Swag Labs" |
| test_productos_visibles | Confirma que se carguen productos en el catalogo |
| test_ui_elements | Valida la visibilidad del menu y filtro de productos |
| test_cart | Verifica el flujo completo de agregar un producto al carrito |

### Validaciones

- **Login**: Redireccion a inventario despues del login exitoso
- **Inventario**: Titulo correcto, productos cargados, elementos de UI visibles
- **Carrito**: Contador muestra "1", nombre del producto coincide con el seleccionado

### Ejecucion de pruebas

```bash
# Ejecutar todas las pruebas
pytest

# Ejecutar todas las pruebas con reporte HTML
pytest --html=report.html

# Ejecutar una prueba especifica
pytest test/test_cart.py

# Ejecutar con verbose
pytest -v
``` 

