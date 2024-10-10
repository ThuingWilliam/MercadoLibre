
# Proyecto: Web Scraping de MercadoLibre usando Selenium y Almacenamiento en Bases de Datos

Este proyecto tiene como objetivo realizar scraping de productos desde el sitio web de **MercadoLibre** utilizando **Selenium** y almacenar los datos extraídos en bases de datos **MySQL** y **MongoDB**. A continuación se explica el paso a paso para ejecutar este proyecto.

## Requisitos previos

1. **Instalar las siguientes dependencias**:
   - `Selenium`: para la automatización del navegador.
   - `pandas`: para manipular los datos.
   - `MySQL Connector`: para la conexión con bases de datos MySQL.
   - `SQLAlchemy`: para trabajar con MySQL mediante ORM.
   - `pymongo`: para trabajar con MongoDB.

   Puedes instalar todas las dependencias con el siguiente comando:

   ```bash
   pip install selenium pandas mysql-connector-python sqlalchemy pymongo
   ```

2. **Configurar el WebDriver**:
   - Descargar el [ChromeDriver](https://sites.google.com/a/chromium.org/chromedriver/downloads) compatible con tu versión de Google Chrome.
   - Coloca el archivo del driver en una ruta accesible.

3. **Instalar un servidor de MySQL y MongoDB**:
   - Tener un servidor de MySQL corriendo con una base de datos disponible.
   - Tener un servidor de MongoDB en funcionamiento.

---

## Paso 1: Importar las bibliotecas necesarias

```python
from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import pandas as pd
import time
import mysql.connector
from sqlalchemy import create_engine
import numpy as np
from pymongo import MongoClient
```

## Paso 2: Configurar y lanzar el WebDriver

```python
# Ruta del ChromeDriver
RUTA = r"C:\WebDriver\chromedriver.exe"

# Inicializar el WebDriver
service = Service(RUTA)
driver = webdriver.Chrome(service=service)

# URL del sitio a hacer scraping
url = 'https://www.mercadolibre.com.do/'
driver.get(url)
```

## Paso 3: Especificar el artículo a buscar

```python
articulo = 'Television'
```

## Paso 4: Realizar la búsqueda en MercadoLibre

```python
searc = '//input[@id="cb1-edit" and @name="as_word"]'
boton = '//button[@type="submit" and @class="nav-search-btn"]'
botonBusqueda = driver.find_element(By.XPATH, searc)
botonBusqueda.send_keys(articulo)
enviar = driver.find_element(By.XPATH, boton)
enviar.click()
time.sleep(2)
```

## Paso 5: Extraer los datos de los productos

```python
# XPath para extraer nombre, precio y enlace
nombre = '//h2[@class="poly-box poly-component__title"]/a'
siguiente = '//li[@class="andes-pagination__button"]/a[@class="andes-pagination__link"]'
precio = '//div[@class="poly-price__current"]/span[@role="img"]'
link = '//h2[@class="poly-box poly-component__title"]/a'
```

## Paso 6: Almacenar los datos en un DataFrame

```python
# Inicializar lista para almacenar datos
productos = []

# Extraer información de productos (nombre, precio, enlace)
# (Aquí iría un código que recorra los elementos, extraiga los datos y los almacene en el DataFrame)
```

## Paso 7: Conexión y almacenamiento en MySQL

```python
# Conectar a MySQL
engine = create_engine('mysql+mysqlconnector://usuario:contraseña@localhost:3306/nombre_db')

# Insertar los datos en MySQL
df.to_sql('tabla_productos', con=engine, if_exists='replace', index=False)
```

## Paso 8: Conexión y almacenamiento en MongoDB

```python
# Conectar a MongoDB
cliente = MongoClient('mongodb://localhost:27017/')
db = cliente['Scrapping']
coleccion = db['Articulo']

# Convertir DataFrame a diccionario e insertar en MongoDB
data_dict = df.to_dict('records')
coleccion.insert_many(data_dict)
```

## Paso 9: Cerrar el WebDriver

```python
driver.quit()
```

