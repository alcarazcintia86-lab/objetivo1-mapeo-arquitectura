# Objetivo 1: Mapeo de Arquitectura Lógica

## Caso elegido: solicitud de turno en un hospital privado

### Objetivo

Representar cómo viajan los datos cuando un paciente solicita un turno
desde la página web de un hospital privado e identificar el tramo
protegido por HTTPS.

### Diagrama de flujo

``` mermaid
flowchart TD
    A["Paciente interactúa con el Frontend<br/>Completa el formulario de turno"]
    B["Navegador web"]
    C["HTTPS / TLS<br/>Cifra los datos durante el tránsito"]
    D["Servidor web / Backend<br/>Recibe y valida los datos"]
    E["Backend consulta la Base de Datos"]
    F[("Base de Datos<br/>Guarda la solicitud del turno")]
    G["La Base de Datos devuelve el resultado"]
    H["Backend prepara la respuesta"]
    I["Respuesta al navegador mediante HTTPS"]
    J["Frontend muestra la confirmación al paciente"]

    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
    F --> G
    G --> H
    H --> I
    I --> J

    style C fill:#d9ecff,stroke:#1769aa,stroke-width:2px
    style I fill:#d9ecff,stroke:#1769aa,stroke-width:2px
```

**Nota:** Los bloques resaltados indican la comunicación protegida por
HTTPS entre el navegador y el servidor. HTTPS protege los datos en
tránsito en ese tramo; no representa por sí mismo la seguridad de la
conexión interna entre el Backend y la Base de Datos.

### Paso a paso

1.  **Interacción con el Frontend:** el paciente abre la página del
    hospital y completa un formulario con datos necesarios para
    solicitar un turno, por ejemplo, nombre, especialidad y fecha
    preferida.
2.  **Envío mediante HTTPS:** el navegador envía la solicitud al
    servidor usando HTTPS. TLS cifra la comunicación entre el navegador
    y el servidor para ayudar a evitar que terceros lean o modifiquen
    los datos durante el tránsito.
3.  **Procesamiento en el Backend:** el servidor recibe la solicitud y
    valida los campos. También debe comprobar que los datos sean válidos
    y que la operación esté permitida.
4.  **Consulta a la Base de Datos:** el Backend realiza una consulta
    para registrar la solicitud del turno. La comunicación entre el
    Backend y la Base de Datos debe protegerse con controles apropiados,
    como permisos restringidos y, cuando corresponda, cifrado de
    conexión.
5.  **Respuesta de la Base de Datos:** la Base de Datos confirma si la
    solicitud se guardó correctamente y devuelve el resultado al
    Backend.
6.  **Respuesta al paciente:** el Backend prepara una respuesta y la
    envía al navegador mediante HTTPS. El Frontend muestra un mensaje de
    confirmación o informa si ocurrió un error.

### ¿En qué tramo ocurre la protección HTTPS?

HTTPS protege el canal de comunicación **entre el navegador del paciente
y el servidor web**, tanto cuando se envía la solicitud como cuando
vuelve la respuesta. No cifra automáticamente los datos almacenados en
la Base de Datos ni garantiza por sí solo la seguridad de la
comunicación interna entre el Backend y la Base de Datos.

### Conclusión

El recorrido lógico de los datos es: **Frontend → navegador →
servidor/Backend → Base de Datos**, y la respuesta regresa hacia el
paciente. HTTPS es esencial para proteger los datos mientras circulan
entre el navegador y el servidor. Además, el sistema debe validar los
datos, controlar los permisos de acceso y proteger adecuadamente la Base
de Datos.

### Herramienta utilizada

El diagrama está escrito en Mermaid dentro de Markdown. Puede
visualizarse en un visor compatible con Mermaid o utilizarse como
referencia para recrearlo en draw.io o Excalidraw.
