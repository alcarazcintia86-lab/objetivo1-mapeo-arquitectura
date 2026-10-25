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

