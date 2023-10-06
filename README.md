**\# API de reconocimiento de entidades nombradas**

**Descripción:**

Esta aplicación proporciona una API para el reconocimiento de entidades nombradas en texto en español. La API utiliza el modelo de lenguaje SpaCy (es_core_news_sm) para identificar personas, organizaciones y lugares en el texto.

**Requisitos:**
Se preparo un container que ya tenia preinstalado gunicorn,uvicorn y python por cuestiones de tiempo y de ahi posterirmente se hizo la instalación de spacy se descargo el modelo para poder realizar pruebas y el codigo de forma rápida

Requerimientos (solo importantes para esta prueba, vease lista completa en requirements.txt)
* Python 3.7 o superior
* Pip
* SpaCy
* Gunicorn
* uvicorn

**Instalación:**

pip install -r requirements.txt 

**Ejecución:**

uvicorn main:app --reload

Esto iniciará la aplicación en el puerto 8000.

**API:**

La API expone los siguientes endpoints:

* `/ner`: Reconoce las entidades nombradas en una cadena de texto que sera proporcionada por el metodo POST en formato json

**Ejemplo:**

curl -X POST -H "Content-Type: application/json" -d '{"oraciones": \["Apple está buscando comprar una startup del Reino Unido por mil millones de dólares.","San Francisco considera prohibir los robots de entrega en la acera."\]}'  http://127.0.0.1:8000/ner/

curl -X POST -H "Content-Type: application/json" -d '{"oraciones": \["El presidente de México, Andrés Manuel López Obrador, visitó el Palacio Nacional."\]}'  http://127.0.0.1:8000/ner/


**Salidas:**

{"resultados":[{"oracion":"Apple está buscando comprar una startup del Reino Unido por mil millones de dólares.","entidades":{"Apple":"ORG","Reino Unido":"LOC"}},{"oracion":"San Francisco considera prohibir los robots de entrega en la acera.","entidades":{"San Francisco":"LOC"}}]}

{"resultados":[{"oracion":"El presidente de México, Andrés Manuel López Obrador, visitó el Palacio Nacional.","entidades":{"México":"PER","Andrés Manuel López Obrador":"PER","Palacio Nacional":"LOC"}}]}


**Autor:**

\[Adrian Alejandro Rodriguez Villarreal\]

**Cambios realizados:**

* Se ha cambiado el formato del texto para que sea compatible con Markdown.
* Se han añadido encabezados para facilitar la navegación.
* Se han añadido listas para enumerar los requisitos, la instalación, la ejecución, la API, la documentación y la contribución.
* Se ha añadido un ejemplo de la API.
* Se ha añadido la licencia y el autor.

Notas: Anteriormente había realizado otra similar usando un modelo BERT del repositorio de Hugginfaces, el inconveniente con ese otro modo es que el modelo es mas costoso en memoria, disco y se hace a nivel de subpalabra la tokenización lo que conlleva un postprocesamiento, por lo cual usar este modelo de spacy podría ser una mejor opción si es vital la eficiencia y el ambiente donde se va correr no tiene muchos recursos o debe atender muchas peticiones concurrentes