# Actividad dirigida 2
## ¿En qué consiste?
Utilizamos el código en bruto de un ejercicio sobre Web Scraping, que ya trabajamos en la anterior asignatura de Programación, para convertilo en un cuaderno en Jupyer. En este documento, empleamos el lenguaje markdown con el objetivo de ir explicando en qué consitía el juego y qué significaban las diferentes líneas de código.

## ¿Cómo lo hemos realizado?
Lo que hicimos fue analizar ese código en bruto y organizarlo. De esta forma, cualquier usuario podrá enteneder facilmente cuáles son los pasos que se han seguido y el por qué. Posteriormente, pasamos a explicar detenenidamente cada uno de los apartados:

#### LIBRERÍAS
Como el objetivo de este juego es extraer información de una página web, lo que haremos es importar la librería `requests`, que nos facilita el trabajo con las peticiones HTTP, y la librería `BeautifulSoup` que sirve para extraer datos desde sitios HTML.

#### VARIABLES
Es uno de los aspectos más importantes ya que dependiendo de esto los datos que aparecerán serán unos o otros.  

#### SOLICITUD
Introduciremos la [URL](https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/) y a ella le haremos la petición `request.get`.

 Es importante darle la instrucción de que si el estatus code no nos permite hacer scrapping, que nos diga mediante el código `req.status_code != 200`

#### DATOS
Locarizaremos las variables `paises`, `oros`, `platas`, `bronces` y  `totales` en la web de El País y las identificaremos con la función `find_all ()`para que haga la búsqueda y las muestre posteriormente.

#### PREGUNTA
Se le formulará al usuario la pregunta `¿Quieres conocer los 20 países que han obtenido más medallas en 2020?`

#### BUCLE CON RESULTADOS
Si la respuesta es `s` se mostraran los datos, en el caso de que se introduzca otra letra, aparecerá el mensaje:`Qué lástima, y...`

## Código en bruto:
```
from bs4 import BeautifulSoup
import requests
#Datos sobre los Juegos Olímpicos en 2020

respuesta=input('¿QUIERES CONOCER LOS 20 PAÍSES QUE HAN OBTENIDO MÁS MEDALLAS EN 2020?\n \n Si tu respuesta es Sí, presiona "s" \n')
if(respuesta == 's'):
  print('\nRESULTADOS DE LOS DATOS DE LOS JUEGOS OLÍMPICOS 2020\n')
  print ('PAÍSES')
  URL = "https://resultados.elpais.com/deportivos/juegos-olimpicos/medallero/"
  # Realizamos la petición a la web
  req = requests.get(URL)
  # Si el estatus code no es 200 no se puede leer la página
  if (req.status_code != 200):
    raise Exception("No se puede hacer Web Scraping en"+ URL)
  # Pasamos el contenido HTML de la web a un objeto BeautifulSoup()
  html = BeautifulSoup(req.text, "html.parser")
  # Obtenemos todos los divs donde están las entradas
  paises = html.find_all("th",{"class":"pais"})
  oros = html.find_all("td",{"class":"m_oro"})
  platas = html.find_all("td",{"class":"m_plata"})
  bronces = html.find_all("td",{"class":"m_bronce"})
  totales = html.find_all("td",{"class":"m_total"})
  for i in range (20):
    # Con el método "getText()" no nos devuelve el HTML
    print("%d. %s \nOro: %s Plata: %s Bronce: %s \n Total: %s \n " % (i+1, paises[i+1].text.strip(),oros[i].text.strip(),platas[i].text.strip(),bronces[i].text.strip(), totales[i].text.strip()))

else:
  print('Qué lástima, y...')

```
[Enlace Scraping](https://github.com/nebrijas/periodismodedatos-marialucia11/blob/main/AD2/scraping%201.ipynb)
