# Fecha en JavaScript

Los objetos JavaScript Date representan un momento en el tiempo en un formato independiente de la plataforma. Estos objetos encapsulan un número entero que representa milisegundos desde la medianoche de principios del 1 de enero de 1970, UTC (la época).

## Descripción

### Época, marcas de tiempo y fechas no válidas

Una fecha de JavaScript se especifica como el tiempo en milisegundos que ha transcurrido desde la época, definida como la medianoche del comienzo del 1 de enero de 1970, UTC (equivalente a la época de UNIX). Esta marca de tiempo es independiente de la zona horaria y define de forma única un instante en la historia. El rango de representación de fechas es amplio, pero fuera de este rango, la fecha se considera no válida.

### Componentes de fecha y zonas horarias

Una fecha se representa internamente como un solo número, la marca de tiempo, que puede interpretarse como hora local o como Hora Universal Coordinada (UTC), la hora estándar global definida por el Estándar de Hora Mundial. La interpretación de la marca de tiempo depende de su uso como hora local o UTC. 

### Formato de cadena de fecha y hora

JavaScript especifica un formato de cadena de fecha y hora para la compatibilidad universal. Este formato sigue la estructura `YYYY-MM-DDTHH:mm:ss.sssZ`, donde cada componente es opcional. Hay diversas formas de formatear una fecha, pero este formato garantiza la máxima compatibilidad.

## Notas adicionales

JavaScript proporciona métodos para interactuar con las fechas, permitiendo el acceso y la manipulación de los componentes de la fecha. Es importante tener en cuenta que los objetos Date se comportan de manera diferente dependiendo del contexto de la zona horaria.

---

*Nota*: TC39 está trabajando en Temporal, una nueva API de fecha/hora. Lea más al respecto en el blog de Igalia. ¡Aún no está listo para su uso en producción!

---

# Constructor

## Date()

Cuando se llama como constructor, devuelve un nuevo objeto Date. Cuando se llama como función, devuelve una representación de cadena de la fecha y hora actuales.

# Métodos estáticos

## Date.now()

Devuelve el valor numérico correspondiente a la hora actual en milisegundos desde el 1 de enero de 1970, 00:00:00 UTC.

## Date.parse()

Analiza una representación de cadena de una fecha y devuelve el número de milisegundos desde el 1 de enero de 1970, 00:00:00 UTC.

## Date.UTC()

Devuelve el número de milisegundos desde el 1 de enero de 1970, 00:00:00 UTC, a partir de los parámetros proporcionados.

# Propiedades de instancia

Estas propiedades están definidas en Date.prototype y compartidas por todas las instancias de Date.

## Date.prototype.constructor

La función constructora que creó el objeto de instancia.

# Métodos de instancia

Estos métodos están definidos en Date.prototype y son utilizados por las instancias de Date.

... (se omite el resto del texto para mantener la longitud adecuada)
