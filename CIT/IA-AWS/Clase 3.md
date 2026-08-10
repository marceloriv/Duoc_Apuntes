# Clase 3

## Party Rock

https://partyrock.aws/


>[!quote]
>Prompt
>Crea una aplicación que basado en un documento de word que tiene ejercicios de un lenguaje de programación, construya mas ejercicio

>[!note]
>Funciona con Amazon Q,  todo esta plataforma esta hostiada en Amazon
>**Amazon Q: **  Es un modelo prentrenado.
>


- Se puede vincular Amazon Q con vscode
- Se pueden hacer escaneos a nivel si trabajamos en la nube , para identificar múltiples cosas.


## Amazon Bedrock

Una plataforma de Amazon para poder levantar el modelo que nosotros queramos del mercado.

>[!abstract]
>Amazon ya tiene modelos para llegar y usar.
>- Tiene distintos proveedores para nosotros llegar y usar el modelo que queramos para poder configurar ciertos parámetros
>	- Temperatura: Que tan precisa es la respuesta 
>	- Top b: Es para ajustar la precisión.
>	- Length: Es para ayustar que tantos token queremos que gaste


Usamos esta plataforma para hacer test de prompt ya que por lo visto podemos ver 2 modelos funcionales ejecutando el mismo prompt y ver sus diferencias.

>[!warning]
>hay que tener en cuenta:
>- Precisión
>- costos
>- objetivo | Casos de uso
>- Calidad de Respuesta
>- Latencia


Nosotros podemos agregarle conocimientos a los modelos de IA

>[!example]
>Se puede crear una base de datos , en donde se pueden  cargas todos los archivos que uno desee para que este disponible para todos los modelos que estén disponibles en el servicio.
>- Amazon con registro de informacion


### Amazon GuardRails

Le damos permiso a Bedrock a ciertas parte de la plataforma para que trabaje, son filtros que se manejan según la entrada y la salida.

Siempre que se cree un modelo necesitamos tener una base de filtro para evitar el mal uso del modelo que se este levantando en Amazon  bedrock.

- Los modelos en su minoría tienden a insultar a lo que se esta usando en los chatbot.
- Cuando se activa, no se gastan los token para evitar que realmente se de un mal uso.

>[!info]
>- Se configurar que no tenga permitido hablar de algunos topicos.
> - Como por ejemplo que no hable de ciberseguridad.
> - Por naturaleza `Profanity filter` se puede usar para prevenir **Prompt injection**



>[!info]
>**Profanity filter**  
> - Agrega filtros por palabras para evitar que evite hablar de las contraseñas, en caso de que se quiera evitar.
> -  Las palabras filtradas quedan como * , es decir **
> - Se pueden agregar hasta 10 expresiones regulares para filtrar.
> - **Grounding:** Es para  que la IA pueda alucinar o no, para que responda de manera mas segura sin que se invente la información. El promedio es `0.7`.
> - **Relevance:** Es para que me de información relevante , ejemplo que no me de informacion antigua.

## Amazon Audit Manager 

Nos permite registrar todos los logs  de la infraestructura completa , para ver la trazabilidad del mismo. Tiene un framework especifico para las IA.
Nos sirve para auditar un sistema que esta en la nube ya que nos centraliza todos los logs de los diferentes servicios que presenta el mismo.

>[!danger]
>Este servicio no arregla los problemas que va encontrando, ya que solo los esta auditando para que nosotros tengamos toda la información de los servicios que nosotros hemos levantado.

**Token** Es una palabra en ingles.














