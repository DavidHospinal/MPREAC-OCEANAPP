
   # MPREAC-OCEANAPP
## Sistema para el reconocimiento de las especies en la pesca acompañante de cerco, utilizando redes neuronales convolucionales para una empresa del sector pesquero en los puertos de Callao y Paracas.

Se espera que este trabajo sea beneficioso para el campo industrial y artesanal de la pesca y los científicos marinos, así como un punto de partida útil donde la motivación principal de los autores es generar la concientización respecto a la identificación de los principales depredadores relacionado al rescate y liberación de las especies marinas que interactúan con la pesca objetivo como es la anchoveta, jurel y caballa.[Link al artículo científico-Paper](https://drive.google.com/file/d/1WY2wJVpQvEA8-5xLBjGibL4HIeXe-E-A/view?usp=share_link)

A continuación presentamos la ![DemoOceanApp]!

![gIF gIThUBv0 2](https://user-images.githubusercontent.com/73408508/204155702-4b328740-b964-4b9e-baed-e90080914f3f.gif)

# Desarrollo y evaluación del modelo

El desarrollo del modelo está conformado por dos grandes fases: la fase del entrenamiento del modelo y la fase de despliegue de este.

# 1.Pre-Entrenamiento

En este punto, se detalla el total de las imágenes estructuradas (data real y sintética), la cual se obtuvo mediante las principales fuentes de datos de las principales Empresas Pesqueras, páginas web (Exalmar, SNP y repositorios indexados), y mediante un trabajo previo de limpieza y conversión de fotogramas. Pos!
teriormente, se procedió a realizar el etiquetado de las respectivas imágenes mediante la herramienta “makesense.ai”.
Aparte de ello se generó información de las coordenadas del cuadro dentro de la imagen que contiene cada categoría. A la información de las coordenadas del objeto dentro de la imagen es a lo que se le puede llamar la etiqueta, para nuestro caso la primera especie lobo marino es a (“0”) y la segunda especie pelícano es a (“1”), en un sistema de coordenadas binario.
![media io_UNjqeAe1](https://user-images.githubusercontent.com/73408508/204156043-42da9768-083d-4e4d-8123-d649adae1c68.gif)



# 2.Entrenamiento

Para el entrenamiento del modelo, se obtuvo un conjunto de datos conformado por 1240 imágenes estructuradas, obtenidas de las principales fuentes de las empresas peruanas pesqueras, y 4960 imágenes de fondo generadas por la clase DataGenerator de Python a fin de reducir los falsos positivos del modelo, dando un total de 6200 imágenes en conjunto, utilizando el 80% de imágenes estructuradas para el entrenamiento y el 20% restante para su validación.

## 2.1 Base de datos:
Se encuentra en Google Drive, se recomienda que ustedes hagan una copia en su perfil, el formato de las imágnes están en jpg y los label en txt.  ya que asi se espera en el google colab para poder trabajar, prestar mucha atención al orden de los archivos en las carpetas, la base de datos se ira actualizando [clik aquí para descargar BD estructurada ](https://drive.google.com/drive/folders/1RIaeYJsEKEyp6wgIBoR8rONC5i2qCo1R?usp=share_link).

Por otro lado referente a la clase DataGenerator nos sirvió  para la alimentación de datos en tiempo real empleado en la biblioteca Keras. Este artificio nos ayudó a mejorar el desempeño de la métrica de precisión de nuestro modelo en la que se pudo llegar a cumplir el indicador de éxito. Hay que destacar que se llegó a generar 4960 imágenes adicionales llamado “imágenes de fondo”, en la cual estos son archivos sin objetos que se agregan a un conjunto de datos para reducir los falsos positivos (FP), para este caso no se requieren etiquetas para las imágenes de fondo. También, merece la pena subrayar que para aumentar el desempeño de esta técnica se realizó mediante un rango del [1%-10%], para nuestro caso se empleó un 5% del total.[clik aquí para descargar BD DataGenerator ](https://drive.google.com/drive/folders/12KPpOShxC82Bpca4Wxe67qjqXoLcvjKH?usp=share_link).

[![00.png](https://i.postimg.cc/BQTDWYWJ/00.png)](https://postimg.cc/VdN5nFLh)


## 2.2 Entrenamiento en la nube:

Se decidió usar google colab, debido a que porrpociona una maquina virtual gratuita por unas horas, subimos el archivo II_Deploy_OceanApp.ipynb o pueden ingresar directamente a nuestro colab . Prestar Atención!!! tienen que desacargar el archivo de la base de datos y subirlo a su cuenta del Google Drive [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1j0T8gdLIa0X8fzkIgFpXDoU27BF49RUz?usp=sharing). Luego tiene que subir el archivo lobpeldrivetraintrain.yaml [clik aquí para descargar el archivo .yaml](https://drive.google.com/file/d/1bT8P3K8NCGKhc7T3EmeHbJdHoOzovCb0/view?usp=share_link)
al google drive dentro de la carpeta yolov5/data, lo que hace este coordinar la información del etiquetado con el entrenamiento de Yolov5 .
Luego la red entrenada genera una archivo best.pt que se encuentra aqui runs/train/exp/weights/best.pt, hay que descargar el mismo , 
[clik aquí para descargar el archivo .best](https://drive.google.com/file/d/1UkN8bOm88l_eTj2Icb7hTgCw0LdN1NSs/view?usp=share_link)

# 3 Resultados - Porcentaje de precisión del modelo

En este punto se desarrolló la métrica de precisión que es el número de resultados correctos dividido por el número de todos los resultados devueltos. La precisión tiene en cuenta todos los archivos recuperados, pero también se puede evaluar en un rango de corte dado, considerando solo los resultados más altos devueltos por el sistema. 

Para todos aquellos resultados de precisión se realizó 07 entrenamientos hasta obtener un indicador óptimo mayor e igual al 90%, en la cual se utilizaron dos tipos de modelos Yolov5x y Yolov5s.

![image](https://user-images.githubusercontent.com/73408508/204157759-eab7c01e-2edf-4533-b150-b3cd71177f48.png)


![Mosaico](https://user-images.githubusercontent.com/73408508/204157722-bd8b1cdb-b79e-47a0-9e9c-8c87738d293a.png)

# 4 Deploy

## 4.1 Google Colab:
Para hacer un puesta en producción rápido ofrecemos un[![Open In Colab](https://colab.research.google.com/drive/1sJb12gs07k22lVD_eXBXpp5tY8RBUUuZ?usp=share_link)](https://colab.research.google.com/drive/1j0T8gdLIa0X8fzkIgFpXDoU27BF49RUz?usp=sharing), previamente hay que subir la red entrenada, que obtuvimos en el paso anterior que se llama best.pt .
Nota; este producto solo durará unas horas ya que esta limitado por el uso de google colab.

## 4.2 HugginFace:
Si se desea tener un modelo en la nube de manera permanente y gratuita le ofrecemos una versión en HuggingFace, el código se encuentra libre en la misma plataforma [Link Deploy](https://huggingface.co/spaces/hexenbiest/OceanApp)

![I-01](https://user-images.githubusercontent.com/73408508/204157894-fe085dda-ad51-4128-9384-5e03b009dbd2.gif)



# Citación
Por favor si usas la base de datos o el código, realizar la citación respectiva de los autores. 
```
@article{Aplicativo móvil para el reconocimiento de las especies del mar peruano en la pesca acompañante de cerco utilizando redes neuronales convolucionales,
  Title = {OceanApp: Detección y monitoreo a tiempo real de especies acompañantes incidentales en el Mar del Perú},
  Authors = {Hospinal Roman, Oscar David  and Geraldine Indira, Jayo Escalante },
  
  Year = {2022}
  University={Universidad Peruana de Ciencias Aplicadas-UPC}
}
```
# Contacto 
Para mas información por favor contactarse a:

u202021214@upc.edu.pe(David Hospinal) and
u202020275@upc.edu.pe(Geraldine Jayo).


