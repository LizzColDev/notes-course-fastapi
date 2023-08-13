# Curso de FastAPI: Introducción, Operaciones, Validaciones y Autenticación

Created: August 12, 2023 10:06 PM

- **¿Qué es FastAPI?**
    
    FastAPI es un framework web de Python de alto rendimiento diseñado para crear APIs (Interfaces de Programación de Aplicaciones) de forma rápida y sencilla. Se destaca por su velocidad, eficiencia y facilidad de uso. FastAPI se basa en el estándar de tipo de anotaciones de Python (PEP 484) y hace un uso extenso de la tipificación estática para ayudar a los desarrolladores a crear aplicaciones con menos errores y más legibilidad.
    
    Algunas características destacadas de FastAPI son:
    
    1. **Rendimiento:** FastAPI está diseñado para ser muy rápido y eficiente, gracias a su enfoque en la ejecución asíncrona y su integración con el servidor ASGI (Asynchronous Server Gateway Interface).
    2. **Autodocumentación:** FastAPI genera automáticamente documentación interactiva para tus APIs en formato OpenAPI y Swagger UI, lo que facilita a los desarrolladores y consumidores comprender cómo usar tus endpoints.
    3. **Validación y conversión de datos:** FastAPI realiza la validación automática de datos según las anotaciones de tipos, lo que ayuda a garantizar la integridad de los datos entrantes en tus endpoints. También realiza conversión de tipos de datos de manera automática.
    4. **Tipado estático:** FastAPI aprovecha el sistema de anotación de tipos de Python para realizar una verificación estática de tipos en tiempo de ejecución. Esto ayuda a prevenir errores comunes y proporciona una mejor autodocumentación.
    5. **Creación de APIs RESTful y WebSocket:** FastAPI permite crear APIs RESTful tradicionales, así como también es compatible con WebSocket para aplicaciones en tiempo real.
    6. **Interfaz intuitiva:** Su sintaxis es muy intuitiva y similar a la definición de funciones regulares en Python, lo que facilita a los desarrolladores la creación de APIs sin una curva de aprendizaje empinada.
    7. **Extensible y personalizable:** Aunque FastAPI ofrece muchas funcionalidades por defecto, también es altamente extensible y permite personalizar varios aspectos según las necesidades específicas de tu proyecto.
- **Instalación de FastAPI y creación de tu primera aplicación**
    
    **Instalación de FastAPI:**
    
    Para utilizar FastAPI y crear tu primera aplicación, necesitarás tener primero Python instalado en tu sistema.
    
    Puedes instalar FastAPI utilizando pip, que es el administrador de paquetes de Python. Abre una terminal y ejecuta el siguiente comando:
    
    ```bash
    pip install fastapi
    ```
    
    Además, para aprovechar al máximo la funcionalidad de FastAPI, es recomendable instalar también el servidor ASGI "uvicorn":
    
    ```bash
    pip install uvicorn
    ```
    
    **Creación de tu primera aplicación FastAPI:**
    
    1. Crea un archivo llamado **`main.py`** en tu directorio de trabajo.
    2. Abre **`main.py`** en tu editor de texto favorito y agrega el siguiente código:
    
    ```python
    from fastapi import FastAPI
    
    app = FastAPI()
    
    @app.get("/")
    def read_root():
        return {"Hello": "World"}
    ```
    
    En este ejemplo, hemos importado la clase **`FastAPI`** de la biblioteca FastAPI. Luego, hemos creado una instancia de esta clase llamada **`app`**. Hemos decorado una función llamada **`read_root`** con **`@app.get("/")`**, lo que significa que esta función se ejecutará cuando se realice una solicitud GET a la raíz ("/") de la aplicación. Dentro de la función, simplemente devolvemos un diccionario con un mensaje de saludo.
    
    1. Guarda el archivo **`main.py`**.
    2. Abre una terminal en el directorio donde se encuentra **`main.py`** y ejecuta el siguiente comando para iniciar el servidor:
    
    ```bash
    uvicorn main:app --reload
    ```
    
    Esto iniciará el servidor ASGI de uvicorn y cargará tu aplicación FastAPI. La opción **`--reload`** permite que el servidor se recargue automáticamente cuando realices cambios en el código.
    
    1. Abre tu navegador web y ve a la siguiente dirección: **`http://127.0.0.1:8000/`**. Deberías ver un mensaje JSON que dice **`{"Hello": "World"}`**, que es la respuesta de tu aplicación FastAPI.
    
    ¡Felicidades! Has creado tu primera aplicación FastAPI y la has ejecutado localmente.
    
- **Documentación automática con Swagger**
    
    FastAPI proporciona documentación automática utilizando el estándar OpenAPI (anteriormente conocido como Swagger). Esta documentación automática es generada automáticamente en función de las anotaciones de tipo y las decoraciones que uses en tu código. Aquí te muestro cómo habilitar y acceder a la documentación de Swagger en tu aplicación FastAPI:
    
    1. Asegúrate de que tienes instalado FastAPI y uvicorn como se mencionó anteriormente.
    2. Abre tu archivo **`main.py`** (o el nombre que hayas utilizado) en tu editor de texto.
    3. Asegúrate de que tu archivo **`main.py`** contenga las rutas y funciones que quieres documentar. Por ejemplo, puedes tener algo como esto:
    
    ```python
    from fastapi import FastAPI
    
    app = FastAPI()
    
    @app.get("/")
    def read_root():
        return {"Hello": "World"}
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int, query_param: str = None):
        return {"item_id": item_id, "query_param": query_param}
    ```
    
    1. Para habilitar la documentación automática, importa el módulo **`FastAPI`** y crea una instancia de **`FastAPI`** en un archivo separado, por ejemplo, **`main.py`**:
    
    ```python
    from fastapi import FastAPI
    
    app = FastAPI()
    ```
    
    1. Importa la clase **`SwaggerUI`** de la biblioteca **`fastapi.openapi.models`**:
    
    ```python
    from fastapi.openapi.models import SwaggerUI
    ```
    
    1. Crea una ruta para servir la documentación de Swagger. Agrega el siguiente código a tu archivo **`main.py`**:
    
    ```python
    @app.get("/docs", include_in_schema=False)
    def custom_swagger_ui_html():
        return SwaggerUI(openapi_url="../openapi.json")
    ```
    
    1. Ejecuta tu aplicación utilizando el comando uvicorn:
    
    ```bash
    uvicorn main:app --reload
    ```
    
    1. Abre tu navegador web y visita la siguiente dirección: **`http://127.0.0.1:8000/docs`**. Deberías ver la interfaz de usuario de Swagger, que mostrará automáticamente la documentación de tus rutas y funciones definidas en **`main.py`**.
    
    La interfaz de usuario de Swagger te permitirá explorar, probar y comprender tus rutas y parámetros de una manera interactiva. Puedes expandir cada ruta para ver detalles sobre los parámetros aceptados y las respuestas generadas. Esto proporciona una forma conveniente de documentar y consumir tus APIs de manera efectiva.
    
- **Métodos HTTP en FastAPI**
    
    FastAPI admite varios métodos HTTP estándar que te permiten interactuar con tus rutas y recursos de API de diferentes maneras. Aquí hay una descripción general de los métodos HTTP compatibles en FastAPI:
    
    1. **GET:** Este método se utiliza para recuperar información de un recurso. Puedes definir rutas para manejar solicitudes GET utilizando el decorador **`@app.get()`**.
    2. **POST:** Se utiliza para enviar datos y crear un nuevo recurso. Puedes definir rutas para manejar solicitudes POST utilizando el decorador **`@app.post()`**.
    3. **PUT:** Este método se utiliza para actualizar un recurso existente o crearlo si no existe. Puedes definir rutas para manejar solicitudes PUT utilizando el decorador **`@app.put()`**.
    4. **DELETE:** Se utiliza para eliminar un recurso existente. Puedes definir rutas para manejar solicitudes DELETE utilizando el decorador **`@app.delete()`**.
    5. **PATCH:** Este método se utiliza para realizar modificaciones parciales en un recurso. Puedes definir rutas para manejar solicitudes PATCH utilizando el decorador **`@app.patch()`**.
    6. **OPTIONS:** Se utiliza para obtener información sobre las opciones disponibles para una ruta determinada. Puedes definir rutas para manejar solicitudes OPTIONS utilizando el decorador **`@app.options()`**.
    7. **HEAD:** Similar a GET, pero se utiliza para solicitar solo las cabeceras de respuesta sin el cuerpo de la respuesta real. Puedes definir rutas para manejar solicitudes HEAD utilizando el decorador **`@app.head()`**.
    
    Aquí hay un ejemplo de cómo definir una ruta para cada uno de estos métodos HTTP en FastAPI:
    
    ```python
    from fastapi import FastAPI
    
    app = FastAPI()
    
    @app.get("/")
    def read_root():
        return {"message": "GET request"}
    
    @app.post("/")
    def create_item(item: dict):
        return {"message": "POST request", "data": item}
    
    @app.put("/{item_id}")
    def update_item(item_id: int, updated_item: dict):
        return {"message": f"PUT request for item {item_id}", "data": updated_item}
    
    @app.delete("/{item_id}")
    def delete_item(item_id: int):
        return {"message": f"DELETE request for item {item_id}"}
    
    @app.patch("/{item_id}")
    def partial_update(item_id: int, updates: dict):
        return {"message": f"PATCH request for item {item_id}", "updates": updates}
    
    @app.options("/")
    def options_info():
        return {"message": "OPTIONS request"}
    
    @app.head("/")
    def head_info():
        return
    ```
    
    Recuerda que los nombres de los parámetros en las funciones de ruta deben coincidir con los nombres de las variables en la URL o en el cuerpo de la solicitud, según corresponda. FastAPI manejará automáticamente la validación y la conversión de tipos para ti, según las anotaciones de tipo que uses en tus funciones.
    
- **Parámetros de ruta**
    
    En FastAPI, los parámetros de ruta te permiten capturar valores directamente de la URL de la solicitud. Esto es útil cuando necesitas acceder a valores específicos proporcionados en la ruta de la URL, como identificadores únicos o nombres de recursos. Los parámetros de ruta se definen dentro de las llaves **`{}`** en la definición de la ruta y se pasan automáticamente como argumentos a la función de ruta correspondiente.
    
    Aquí te muestro cómo puedes utilizar los parámetros de ruta en FastAPI:
    
    ```python
    from fastapi import FastAPI
    
    app = FastAPI()
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int):
        return {"item_id": item_id}
    ```
    
    En este ejemplo, hemos definido una ruta **`/items/{item_id}`** que captura el valor de **`item_id`** de la URL. Cuando se realiza una solicitud a esta ruta, el valor de **`item_id`** se pasa automáticamente como argumento a la función **`read_item()`**. Puedes acceder a este valor y utilizarlo en la función.
    
    Ejemplo de solicitud y respuesta:
    
    - Solicitud: **`GET /items/42`**
    - Respuesta:
    
    ```json
    {"item_id": 42}
    ```
    
    También puedes definir múltiples parámetros de ruta en una sola ruta:
    
    ```python
    @app.get("/users/{user_id}/items/{item_id}")
    def read_user_item(user_id: int, item_id: int):
        return {"user_id": user_id, "item_id": item_id}
    ```
    
    En este ejemplo, hemos definido dos parámetros de ruta, **`user_id`** y **`item_id`**, y hemos capturado ambos valores de la URL. La función **`read_user_item()`** recibe estos valores como argumentos y los utiliza en la respuesta.
    
    Ejemplo de solicitud y respuesta:
    
    - Solicitud: **`GET /users/123/items/456`**
    - Respuesta:
    
    ```json
    {"user_id": 123, "item_id": 456}
    ```
    
    FastAPI también realiza automáticamente la validación de tipos para los parámetros de ruta, asegurando que los valores proporcionados en la URL sean del tipo esperado (en este caso, **`int`**). Si se proporciona un valor no válido, FastAPI generará una respuesta de error con los detalles correspondientes.
    
- **Parámetros Query**
    
    En FastAPI, los parámetros de consulta (query parameters) te permiten pasar información adicional a través de la URL en forma de pares clave-valor. Estos parámetros son opcionales y se especifican después del signo de interrogación (**`?`**) en la URL. Los parámetros de consulta son muy útiles cuando deseas proporcionar filtros, opciones de paginación u otra información adicional a tu API.
    
    Aquí tienes un ejemplo de cómo usar parámetros de consulta en FastAPI:
    
    ```python
    from fastapi import FastAPI
    
    app = FastAPI()
    
    @app.get("/items/")
    def read_items(skip: int = 0, limit: int = 10):
        return {"skip": skip, "limit": limit}
    ```
    
    En este ejemplo, hemos definido una ruta **`/items/`** que acepta dos parámetros de consulta opcionales: **`skip`** y **`limit`**. Estos parámetros se definen directamente como argumentos en la función de ruta **`read_items()`**. Si no se proporcionan en la URL, los valores predeterminados (**`0`** y **`10`** en este caso) se usarán.
    
    Ejemplo de solicitud y respuesta:
    
    - Solicitud: **`GET /items/?skip=20&limit=5`**
    - Respuesta:
    
    ```json
    {"skip": 20, "limit": 5}
    ```
    
    Si no se proporcionan los parámetros de consulta en la URL, los valores predeterminados se usarán:
    
    - Solicitud: **`GET /items/`**
    - Respuesta:
    
    ```json
    {"skip": 0, "limit": 10}
    ```
    
    FastAPI realiza automáticamente la validación y la conversión de tipos para los parámetros de consulta. Si un valor no válido es proporcionado (por ejemplo, una cadena en lugar de un número entero), FastAPI generará una respuesta de error con los detalles correspondientes.
    
    Recuerda que los nombres de los parámetros de consulta en la función deben coincidir con los nombres utilizados en la URL. Además, los parámetros de consulta en FastAPI son tratados como parámetros opcionales, lo que significa que no es necesario proporcionarlos en cada solicitud.
    
- **Creación de esquemas**
    
    En FastAPI, puedes usar esquemas (schemas) para definir cómo se deben validar y convertir los datos de entrada y salida en tus rutas. Los esquemas te permiten especificar la estructura y los tipos de datos esperados para las solicitudes y respuestas de tu API. Puedes utilizar la biblioteca Pydantic para crear esquemas en FastAPI, ya que FastAPI está estrechamente integrado con Pydantic para el manejo de datos.
    
    Aquí te muestro cómo crear esquemas en FastAPI utilizando Pydantic:
    
    1. Primero, asegúrate de tener instalados FastAPI y Pydantic. Si no lo has hecho, puedes instalarlos con los siguientes comandos:
    
    ```bash
    pip install fastapi
    pip install pydantic
    ```
    
    1. Crea un archivo **`main.py`** en tu directorio de trabajo.
    2. Abre **`main.py`** en tu editor de texto y agrega el siguiente código:
    
    ```python
    from fastapi import FastAPI
    from pydantic import BaseModel
    
    app = FastAPI()
    
    class Item(BaseModel):
        name: str
        description: str = None
        price: float
        tax: float = None
    
    @app.post("/items/")
    def create_item(item: Item):
        return item
    ```
    
    En este ejemplo, hemos definido una clase **`Item`** que hereda de **`BaseModel`** de Pydantic. Dentro de la clase, hemos definido los campos **`name`**, **`description`**, **`price`** y **`tax`**, junto con sus tipos de datos esperados. Los campos con valores predeterminados se especifican usando el operador de asignación (**`=`**). Luego, hemos creado una ruta **`/items/`** que acepta una solicitud POST y espera un objeto **`Item`** en el cuerpo de la solicitud.
    
    1. Guarda el archivo **`main.py`**.
    2. Abre una terminal en el directorio donde se encuentra **`main.py`** y ejecuta el siguiente comando para iniciar el servidor:
    
    ```bash
    uvicorn main:app --reload
    ```
    
    1. Abre un cliente API (por ejemplo, Postman o cURL) y realiza una solicitud POST a **`http://127.0.0.1:8000/items/`** con un cuerpo JSON como este:
    
    ```json
    {
        "name": "Product A",
        "price": 29.99
    }
    ```
    
    Deberías recibir una respuesta que contiene el objeto **`Item`** con los datos proporcionados en la solicitud.
    
    Los esquemas definidos con Pydantic te permiten realizar validaciones automáticas de datos, conversión de tipos y generación de documentación precisa en tu API. Puedes expandir y personalizar estos esquemas según las necesidades de tu aplicación, y FastAPI se encargará de manejar la validación y conversión de manera eficiente.
    
- **Validaciones de tipos de datos**
    
    En FastAPI, las validaciones de tipos de datos se realizan automáticamente utilizando las anotaciones de tipo proporcionadas por Python y Pydantic. FastAPI aprovecha el sistema de anotación de tipos para realizar una verificación estática de tipos en tiempo de ejecución. Esto asegura que los datos proporcionados en las solicitudes cumplan con los tipos de datos esperados.
    
    Aquí tienes un ejemplo de cómo se realizan las validaciones de tipos de datos en FastAPI:
    
    ```python
    from fastapi import FastAPI
    from pydantic import BaseModel
    
    app = FastAPI()
    
    class Item(BaseModel):
        name: str
        price: float
    
    @app.post("/items/")
    def create_item(item: Item):
        return item
    ```
    
    En este ejemplo, hemos definido una clase **`Item`** que hereda de **`BaseModel`** de Pydantic. Hemos especificado que **`name`** debe ser una cadena (**`str`**) y **`price`** debe ser un número de punto flotante (**`float`**). Cuando realizamos una solicitud POST a **`/items/`** y proporcionamos un objeto JSON que no cumple con estas validaciones, FastAPI generará automáticamente una respuesta de error con los detalles correspondientes.
    
    Por ejemplo, si enviamos el siguiente objeto JSON:
    
    ```json
    {
        "name": "Product A",
        "price": "29.99"
    }
    ```
    
    FastAPI generará una respuesta de error indicando que se esperaba un número de punto flotante para el campo **`price`**.
    
    Además de las validaciones de tipos de datos, Pydantic también realiza automáticamente otras validaciones, como verificar que los campos requeridos estén presentes, aplicar valores predeterminados y permitir la validación de valores nulos (null) o vacíos según las anotaciones de tipo y las configuraciones de Pydantic.
    
    FastAPI también proporciona validaciones adicionales que puedes aplicar a los campos utilizando las declaraciones **`Field`** y las funciones auxiliares de Pydantic, como **`MinLength`**, **`MaxLength`**, **`Email`**, **`Url`**, entre otras.
    
    Las validaciones de tipos de datos en FastAPI son una característica poderosa que te ayuda a garantizar la integridad de los datos en tu API y a prevenir errores antes de que lleguen a la lógica de tu aplicación.
    
- **Validaciones de parámetros**
    
    En FastAPI, puedes aplicar validaciones a los parámetros de ruta, parámetros de consulta y cuerpos de solicitud utilizando las anotaciones de tipo y las funciones auxiliares proporcionadas por Pydantic. Esto te permite garantizar que los datos ingresados cumplan con ciertos criterios antes de que se procesen en tu aplicación.
    
    Aquí tienes ejemplos de cómo aplicar validaciones a diferentes tipos de parámetros:
    
    **Validaciones en parámetros de ruta:**
    
    ```python
    from fastapi import FastAPI, Path
    
    app = FastAPI()
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int = Path(..., title="ID del artículo", gt=0)):
        return {"item_id": item_id}
    ```
    
    En este ejemplo, hemos aplicado las siguientes validaciones al parámetro **`item_id`** de la ruta:
    
    - **`...`** indica que el parámetro es requerido.
    - **`title`** especifica una descripción más legible para la documentación.
    - **`gt=0`** asegura que el valor del parámetro sea mayor que cero.
    
    **Validaciones en parámetros de consulta:**
    
    ```python
    from fastapi import FastAPI, Query
    
    app = FastAPI()
    
    @app.get("/items/")
    def read_items(skip: int = Query(0, title="Saltar elementos", description="Número de elementos a saltar", ge=0),
                   limit: int = Query(10, title="Límite de elementos", description="Número máximo de elementos a devolver", le=100)):
        return {"skip": skip, "limit": limit}
    ```
    
    En este ejemplo, hemos aplicado las siguientes validaciones a los parámetros de consulta **`skip`** y **`limit`**:
    
    - **`ge=0`** asegura que el valor sea mayor o igual a cero.
    - **`le=100`** asegura que el valor sea menor o igual a 100.
    
    **Validaciones en cuerpos de solicitud:**
    
    ```python
    from fastapi import FastAPI, Body
    
    app = FastAPI()
    
    class ItemCreate(BaseModel):
        name: str
        price: float
    
    @app.post("/items/")
    def create_item(item: ItemCreate = Body(..., title="Item a crear")):
        return item
    ```
    
    En este ejemplo, hemos aplicado la validación del esquema **`ItemCreate`** al cuerpo de la solicitud. La anotación **`...`** indica que el campo es requerido.
    
    Recuerda que las validaciones de parámetros en FastAPI se combinan con la validación de tipos inherente a las anotaciones de tipo de Python y Pydantic. Esto te permite garantizar la coherencia y la calidad de los datos en tu aplicación API, reduciendo la probabilidad de errores y problemas relacionados con datos incorrectos.
    
- **Tipos de respuestas**
    
    En FastAPI, puedes controlar los tipos de respuestas que tu API devuelve utilizando las anotaciones de tipo y las funciones auxiliares proporcionadas por FastAPI. Esto te permite definir el formato y la estructura de las respuestas generadas por tus rutas.
    
    Aquí tienes ejemplos de cómo especificar los tipos de respuestas en FastAPI:
    
    **Respuestas con tipos de datos simples:**
    
    ```python
    
    from fastapi import FastAPI
    
    app = FastAPI()
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int):
        return {"item_id": item_id, "name": "Product A"}
    ```
    
    En este ejemplo, la función de ruta **`read_item()`** devuelve un diccionario. FastAPI infiere automáticamente el tipo de respuesta basado en el valor de retorno. En este caso, la respuesta generada tendrá el formato JSON.
    
    **Respuestas con tipos de Pydantic:**
    
    ```python
    
    from fastapi import FastAPI
    from pydantic import BaseModel
    
    app = FastAPI()
    
    class Item(BaseModel):
        item_id: int
        name: str
    
    @app.get("/items/{item_id}", response_model=Item)
    def read_item(item_id: int):
        return {"item_id": item_id, "name": "Product A"}
    ```
    
    En este ejemplo, hemos especificado el tipo de respuesta utilizando el parámetro **`response_model`**. La función de ruta **`read_item()`** devuelve un diccionario, pero FastAPI lo convertirá automáticamente al esquema **`Item`** definido en Pydantic antes de enviar la respuesta. Esto garantiza que la respuesta cumpla con la estructura y los tipos de datos esperados.
    
    **Respuestas con código de estado personalizado:**
    
    ```python
    
    from fastapi import FastAPI, HTTPException
    
    app = FastAPI()
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int):
        if item_id != 42:
            raise HTTPException(status_code=404, detail="Item not found")
        return {"item_id": item_id, "name": "Product A"}
    ```
    
    En este ejemplo, hemos lanzado una excepción **`HTTPException`** con un código de estado personalizado y un mensaje de detalle cuando el **`item_id`** no es igual a 42. FastAPI convertirá automáticamente esta excepción en una respuesta JSON con el código de estado y el mensaje especificados.
    
    Estos son solo ejemplos básicos de cómo controlar los tipos de respuestas en FastAPI. Puedes utilizar tipos de datos simples, esquemas Pydantic, excepciones personalizadas y otras funciones auxiliares para definir el formato y la estructura exactos de las respuestas de tus rutas. FastAPI se encargará de realizar las conversiones y generar respuestas adecuadas según las especificaciones que proporciones.
    
- **Códigos de estado**
    
    En FastAPI, puedes controlar los códigos de estado de las respuestas HTTP utilizando la biblioteca estándar **`starlette.status`** o simplemente proporcionando los códigos de estado directamente en tus respuestas. Aquí tienes ejemplos de cómo trabajar con códigos de estado en FastAPI:
    
    **Usando la biblioteca `starlette.status`:**
    
    ```python
    
    from fastapi import FastAPI
    from starlette import status
    
    app = FastAPI()
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int):
        if item_id == 42:
            return {"item_id": item_id, "name": "Product A"}
        else:
            return {"error": "Item not found"}, status.HTTP_404_NOT_FOUND
    ```
    
    En este ejemplo, hemos importado **`status`** de **`starlette`** y utilizado **`status.HTTP_404_NOT_FOUND`** para especificar el código de estado 404 en caso de que el ítem no sea encontrado.
    
    **Proporcionando códigos de estado directamente:**
    
    ```python
    
    from fastapi import FastAPI
    
    app = FastAPI()
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int):
        if item_id == 42:
            return {"item_id": item_id, "name": "Product A"}
        else:
            return {"error": "Item not found"}, 404
    ```
    
    En este ejemplo, hemos proporcionado directamente el código de estado 404 en la respuesta.
    
    Recuerda que FastAPI también admite el uso de excepciones para manejar códigos de estado personalizados. Puedes utilizar la clase **`HTTPException`** para lanzar una excepción con un código de estado y un mensaje de detalle personalizados:
    
    ```python
    
    from fastapi import FastAPI, HTTPException
    
    app = FastAPI()
    
    @app.get("/items/{item_id}")
    def read_item(item_id: int):
        if item_id == 42:
            return {"item_id": item_id, "name": "Product A"}
        else:
            raise HTTPException(status_code=404, detail="Item not found")
    ```
    
    En este caso, FastAPI automáticamente generará una respuesta con el código de estado 404 y el mensaje de detalle especificados en la excepción.
    
    En resumen, puedes controlar los códigos de estado en FastAPI utilizando la biblioteca **`starlette.status`**, proporcionando códigos directamente en tus respuestas o lanzando excepciones **`HTTPException`** con códigos de estado personalizados. Esto te permite enviar respuestas con los códigos de estado adecuados según la lógica de tu aplicación.
    
- **Flujo de autenticación**
    
    El flujo de autenticación en una aplicación FastAPI generalmente sigue un patrón en el que los usuarios deben autenticarse antes de acceder a ciertas rutas o recursos protegidos. FastAPI ofrece flexibilidad para implementar varios métodos de autenticación, como el uso de tokens JWT (JSON Web Tokens), esquemas OAuth2, autenticación básica, entre otros. A continuación, te proporcionaré un ejemplo básico de cómo implementar la autenticación JWT en FastAPI:
    
    1. Instala los paquetes necesarios:
    
    Asegúrate de tener instalados los paquetes necesarios para implementar la autenticación JWT. Puedes instalarlos con los siguientes comandos:
    
    ```bash
    
    pip install fastapi
    pip install uvicorn
    pip install pyjwt
    ```
    
    1. Crea un archivo **`main.py`** en tu directorio de trabajo.
    2. Abre **`main.py`** en tu editor de texto y agrega el siguiente código:
    
    ```python
    
    from fastapi import FastAPI, Depends, HTTPException
    from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm
    import jwt
    from jwt import PyJWTError
    from datetime import datetime, timedelta
    
    app = FastAPI()
    
    # Configura el secreto y el algoritmo para JWT
    SECRET_KEY = "mikeysecreta"
    ALGORITHM = "HS256"
    ACCESS_TOKEN_EXPIRE_MINUTES = 30
    
    # Simulación de una base de datos de usuarios
    fake_users_db = {
        "johndoe": {
            "username": "johndoe",
            "password": "password123"
        }
    }
    
    class TokenData:
        username: str
    
    class User:
        def __init__(self, username: str):
            self.username = username
    
    # Función para generar un token JWT
    def create_access_token(data: dict, expires_delta: timedelta):
        to_encode = data.copy()
        expire = datetime.utcnow() + expires_delta
        to_encode.update({"exp": expire})
        encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
        return encoded_jwt
    
    # Dependencia para obtener el token de acceso desde la solicitud
    oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")
    
    # Ruta para autenticar y generar un token JWT
    @app.post("/token")
    async def login_for_access_token(form_data: OAuth2PasswordRequestForm = Depends()):
        user = fake_users_db.get(form_data.username)
        if user is None or user["password"] != form_data.password:
            raise HTTPException(status_code=401, detail="Credenciales inválidas")
        access_token_expires = timedelta(minutes=ACCESS_TOKEN_EXPIRE_MINUTES)
        access_token = create_access_token(
            data={"sub": user["username"]}, expires_delta=access_token_expires
        )
        return {"access_token": access_token, "token_type": "bearer"}
    
    # Ruta protegida que requiere autenticación
    @app.get("/protected")
    async def protected_route(token: str = Depends(oauth2_scheme)):
        try:
            payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
            username: str = payload.get("sub")
            if username not in fake_users_db:
                raise HTTPException(status_code=401, detail="No autorizado")
            return {"message": "¡Ruta protegida accesible!", "username": username}
        except PyJWTError:
            raise HTTPException(status_code=401, detail="No autorizado")
    ```
    
    1. Guarda el archivo **`main.py`**.
    2. Abre una terminal en el directorio donde se encuentra **`main.py`** y ejecuta el siguiente comando para iniciar el servidor:
    
    ```bash
    
    uvicorn main:app --reload
    ```
    
    Ahora has implementado un flujo de autenticación básico usando tokens JWT en FastAPI. Puedes probarlo utilizando una herramienta como Postman o cURL:
    
    1. Obtén un token de acceso haciendo una solicitud POST a **`http://127.0.0.1:8000/token`** con las credenciales en el formulario (**`username`** y **`password`**).
    2. Luego, realiza una solicitud GET a **`http://127.0.0.1:8000/protected`**, incluyendo el token de acceso en el encabezado de autorización (**`Bearer <token>`**). Deberías recibir una respuesta exitosa si la autenticación es exitosa.
- **Generando tokens con PyJWT**
    
    **`PyJWT`** es una biblioteca de Python que te permite generar y verificar tokens JSON Web (JWT), como los tokens de autenticación JWT utilizados en sistemas de autenticación y autorización. A continuación, te mostraré cómo generar tokens con **`pyjwt`**:
    
    1. Instala la biblioteca **`pyjwt`** si aún no lo has hecho:
    
    ```bash
    
    pip install pyjwt
    ```
    
    1. Aquí tienes un ejemplo de cómo generar un token JWT con **`pyjwt`**:
    
    ```python
    
    import jwt
    import datetime
    
    # Definir una clave secreta (secreto compartido entre el servidor y el cliente)
    SECRET_KEY = "mikeysecreta"
    
    # Definir la información que deseas incluir en el token (carga útil)
    payload = {
        "sub": "usuario123",         # Sujeto del token (identificador único)
        "iat": datetime.datetime.utcnow(),  # Tiempo de emisión del token
        "exp": datetime.datetime.utcnow() + datetime.timedelta(minutes=30)  # Tiempo de expiración del token
    }
    
    # Generar el token usando la función encode de jwt
    token = jwt.encode(payload, SECRET_KEY, algorithm="HS256")
    
    print("Token generado:")
    print(token)
    ```
    
    En este ejemplo, hemos utilizado la función **`jwt.encode()`** para generar un token JWT. Le proporcionamos la carga útil (payload) que deseamos incluir en el token, la clave secreta (**`SECRET_KEY`**) y el algoritmo de cifrado (**`HS256`**). El token generado es una cadena de caracteres que representa el token JWT.
    
    Recuerda que la clave secreta (**`SECRET_KEY`**) debe ser mantenida segura y no compartida públicamente. Es crucial para la seguridad del token y para garantizar que solo el servidor pueda firmar y verificar los tokens.
    
    1. Puedes decodificar y verificar el token JWT en otro momento utilizando **`jwt.decode()`**:
    
    ```python
    
    try:
        decoded_payload = jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
        print("Token decodificado:")
        print(decoded_payload)
    except jwt.ExpiredSignatureError:
        print("El token ha expirado")
    except jwt.InvalidTokenError:
        print("El token no es válido")
    ```
    
    En este ejemplo, utilizamos **`jwt.decode()`** para verificar y decodificar el token JWT. Si el token es válido y no ha expirado, la función retornará la carga útil decodificada.
    
    Este es solo un ejemplo básico de cómo generar y verificar tokens JWT utilizando la biblioteca **`pyjwt`**. Los tokens JWT son ampliamente utilizados en sistemas de autenticación y autorización para transmitir información segura entre el cliente y el servidor de manera segura y eficiente. Recuerda seguir las mejores prácticas de seguridad al trabajar con tokens JWT y otras medidas de seguridad en tus aplicaciones.
    
- **Validando tokens**
    
    La validación de tokens JWT es una parte esencial del flujo de autenticación en una aplicación. Para validar tokens JWT generados previamente, necesitas asegurarte de que el token sea auténtico (no ha sido alterado) y que no haya expirado. Aquí tienes un ejemplo de cómo puedes realizar la validación de tokens JWT en Python utilizando la biblioteca **`pyjwt`**:
    
    1. Instala la biblioteca **`pyjwt`** si aún no lo has hecho:
    
    ```bash
    
    pip install pyjwt
    ```
    
    1. Supongamos que ya tienes un token JWT que has recibido en una solicitud de autenticación:
    
    ```python
    
    received_token = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJ1c3VhcmlvMTIzIiwiaWF0IjoxNjMwNTI1MzA2LCJleHAiOjE2MzA1MjgxMDZ9.XX2cPuvuA0RG_k-bdCzrBfEeLqr1J_bAsgAqtNtPWQw"
    ```
    
    1. Aquí tienes un ejemplo de cómo puedes validar y decodificar el token JWT:
    
    ```python
    
    import jwt
    import datetime
    
    # Definir la clave secreta (debe coincidir con la clave utilizada para firmar el token)
    SECRET_KEY = "mikeysecreta"
    
    try:
        # Validar y decodificar el token
        decoded_payload = jwt.decode(received_token, SECRET_KEY, algorithms=["HS256"])
    
        # Verificar la fecha de expiración
        current_time = datetime.datetime.utcnow()
        token_exp = datetime.datetime.utcfromtimestamp(decoded_payload["exp"])
        if token_exp < current_time:
            print("El token ha expirado")
        else:
            print("Token válido:")
            print(decoded_payload)
    except jwt.ExpiredSignatureError:
        print("El token ha expirado")
    except jwt.InvalidTokenError:
        print("El token no es válido")
    ```
    
    En este ejemplo, estamos utilizando **`jwt.decode()`** para validar y decodificar el token JWT. Luego, comparamos la fecha de expiración (**`exp`**) en el token con la hora actual para verificar si el token ha expirado. Si el token es válido y no ha expirado, el contenido decodificado del token se mostrará en la consola.
    
    Ten en cuenta que esta es una validación básica de tokens JWT. En aplicaciones reales, es recomendable implementar una estrategia de manejo de tokens más sólida, como la verificación de firmas con claves públicas y privadas, así como la validación de otros campos específicos según tus necesidades de seguridad.
    
    Recuerda mantener la clave secreta (**`SECRET_KEY`**) segura y no compartirla públicamente, ya que es fundamental para la seguridad de tus tokens JWT.
    
- **Middlewares de autenticación**
    
    Los middlewares de autenticación son componentes que se utilizan en un framework web para interceptar y procesar las solicitudes antes de que lleguen a las rutas de la aplicación. En FastAPI, los middlewares de autenticación te permiten implementar la lógica de autenticación y autorización de manera centralizada, lo que facilita la protección de rutas o recursos específicos de tu API.
    
    A continuación, te proporciono un ejemplo básico de cómo implementar un middleware de autenticación en FastAPI utilizando tokens JWT:
    
    ```python
    
    from fastapi import FastAPI, Depends, HTTPException, status
    from fastapi.security import OAuth2PasswordBearer
    import jwt
    from jwt import PyJWTError
    from datetime import datetime, timedelta
    
    app = FastAPI()
    
    # Configura el secreto y el algoritmo para JWT
    SECRET_KEY = "mikeysecreta"
    ALGORITHM = "HS256"
    ACCESS_TOKEN_EXPIRE_MINUTES = 30
    
    # Simulación de una base de datos de usuarios
    fake_users_db = {
        "johndoe": {
            "username": "johndoe",
            "password": "password123"
        }
    }
    
    class TokenData:
        username: str
    
    class User:
        def __init__(self, username: str):
            self.username = username
    
    # Función para generar un token JWT
    def create_access_token(data: dict, expires_delta: timedelta):
        to_encode = data.copy()
        expire = datetime.utcnow() + expires_delta
        to_encode.update({"exp": expire})
        encoded_jwt = jwt.encode(to_encode, SECRET_KEY, algorithm=ALGORITHM)
        return encoded_jwt
    
    # Dependencia para obtener el token de acceso desde la solicitud
    oauth2_scheme = OAuth2PasswordBearer(tokenUrl="token")
    
    # Middleware de autenticación
    def authenticate_token(token: str = Depends(oauth2_scheme)):
        try:
            payload = jwt.decode(token, SECRET_KEY, algorithms=[ALGORITHM])
            username: str = payload.get("sub")
            if username not in fake_users_db:
                raise HTTPException(status_code=status.HTTP_401_UNAUTHORIZED, detail="No autorizado")
            return User(username=username)
        except PyJWTError:
            raise HTTPException(status_code=status.HTTP_401_UNAUTHORIZED, detail="No autorizado")
    
    # Ruta protegida que requiere autenticación
    @app.get("/protected")
    async def protected_route(user: User = Depends(authenticate_token)):
        return {"message": "¡Ruta protegida accesible!", "username": user.username}
    ```
    
    En este ejemplo, hemos creado un middleware de autenticación llamado **`authenticate_token`** que intercepta las solicitudes y verifica la autenticidad del token JWT. Si el token es válido, la función **`authenticate_token`** devuelve un objeto **`User`** que contiene el nombre de usuario. Luego, este objeto **`User`** se pasa como argumento a la función de ruta **`protected_route`**, permitiendo el acceso a la ruta protegida solo a usuarios autenticados.
    
    El uso de middlewares de autenticación centraliza la lógica de autenticación y simplifica la protección de rutas en tu API. Puedes aplicar este enfoque a otras estrategias de autenticación, como autenticación basada en tokens de sesión, OAuth2 u otras formas de autenticación personalizada según tus necesidades específicas.