# Fecha en JavaScript

Los objetos JavaScript Date representan un momento en el tiempo en un formato independiente de la plataforma. Estos objetos encapsulan un número entero que representa milisegundos desde la medianoche de principios del 1 de enero de 1970, UTC (la época).

## Descripción

### Época, marcas de tiempo y fechas no válidas

Existen varios métodos que le permiten interactuar con la marca de tiempo almacenada en la fecha:

- Puede interactuar con el valor de la marca de tiempo directamente usando los métodos [`getTime()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/getTime)y [`setTime()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/setTime).
- Los métodos [`valueOf()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/valueOf)y [`[@@toPrimitive]()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/@@toPrimitive)(cuando se pasan `"number"`), que se llaman automáticamente en [coerción numérica](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number#number_coercion) , devuelven la marca de tiempo, lo que hace que `Date`los objetos se comporten como sus marcas de tiempo cuando se usan en contextos numéricos.
- Todos los métodos estáticos ( [`Date.now()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/now), [`Date.parse()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/parse)y [`Date.UTC()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/UTC)) devuelven marcas de tiempo en lugar de `Date`objetos.
- Se puede llamar al [`Date()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/Date)constructor con una marca de tiempo como único argumento.

## Componentes de fecha y zonas horarias 

la hora estándar global definida por el Estándar de Hora Mundial. La zona horaria local no se almacena en el objeto de fecha, sino que está determinada por el entorno del host (dispositivo del usuario).Por ejemplo, la marca de tiempo 0 representa un instante único en la historia, pero se puede interpretar de dos maneras:

- Como hora UTC, es la medianoche de principios del 1 de enero de 1970, UTC,
- Como hora local en Nueva York (UTC-5), son las 19:00:00 del 31 de diciembre de 1969.

| Componente        | Local             |                   | UTC                  |                      |
| ----------------- | ----------------- | ----------------- | -------------------- | -------------------- |
| Año               | getFullYear()     | setFullYear()     | getUTCFullYear()     | setUTCFullYear()     |
| Mes               | getMonth()        | setMonth()        | getUTCMonth()        | setUTCMonth()        |
| Fecha (del mes)   | getDate()         | setDate()         | getUTCDate()         | setUTCDate()         |
| Horas             | getHours()        | setHours()        | getUTCHours()        | setUTCHours()        |
| Minutos           | getMinutes()      | setMinutes()      | getUTCMinutes()      | setUTCMinutes()      |
| Segundos          | getSeconds()      | setSeconds()      | getUTCSeconds()      | setUTCSeconds()      |
| Milisegundos      | getMilliseconds() | setMilliseconds() | getUTCMilliseconds() | setUTCMilliseconds() |
| Día de la semana) | getDay()          | N / A             | getUTCDay()          | N / A                |



## Formato de cadena de fecha y hora

Hay muchas formas de formatear una fecha como una cadena. La especificación de JavaScript solo especifica un formato que será compatible universalmente: el formato de cadena de fecha y hora, una simplificación del formato extendido de fecha del calendario ISO 8601. El formato es el siguiente:

- `YYYY-MM-DDTHH:mm:ss.sssZ`
  - `YYYY`: El año, con cuatro dígitos (0000 a 9999), o como un año ampliado o +seguido -de seis dígitos. El letrero es obligatorio para años ampliados. -000000 está explícitamente rechazado como año válido.
  - `MM`: El mes, con dos dígitos (01 a 12). El valor predeterminado es 01.
  - `DD`: El día del mes, con dos dígitos (01 a 31). El valor predeterminado es 01.
  - `T`: Es un carácter literal, que indica el comienzo de la parte temporal de la cadena. Se requiere al especificar la parte de tiempo.
  - `HH`: La hora, con dos dígitos (00 a 23). Como caso especial, 24:00:00 se permite, y se interpreta como medianoche del inicio del día siguiente. El valor predeterminado es 00.
  - `mm`: El minuto, con dos dígitos (00 a 59). El valor predeterminado es 00.
  - `ss`: El segundo, con dos dígitos (00 a 59). El valor predeterminado es 00.
  - `sss`: El milisegundo, con tres dígitos (000 a 999). El valor predeterminado es 000.
  - `Z`: El desplazamiento de la zona horaria, que puede ser el carácter literal Z (que indica UTC) o +seguido -de HH:mm, el desplazamiento en horas y minutos desde UTC.

Se pueden omitir varios componentes, por lo que son válidos los siguientes:

- Formulario solo para fecha: `YYYY`, `YYYY-MM`, `YYYY-MM-DD`
- Formulario de fecha y hora: uno de los formularios anteriores de solo fecha, seguido de `T`, seguido de `HH:mm`, `HH:mm:ss` o `HH:mm:ss.sss`. Cada combinación puede ir seguida de un desplazamiento de zona horaria.

## Otras formas de formatear una fecha

Existen varias formas adicionales de formatear una fecha en JavaScript:

- `toISOString()`: Devuelve una cadena en el formato `1970-01-01T00:00:00.000Z` (el formato de cadena de fecha y hora simplificado según ISO 8601). `toJSON()` llama a `toISOString()` y devuelve el resultado.
  - Ejemplo:
    ```javascript
    const d = new Date(0);
    console.log(d.toISOString()); // "1970-01-01T00:00:00.000Z"
    ```

- `toString()`: Devuelve una cadena en el formato `Thu Jan 01 1970 00:00:00 GMT+0000 (Coordinated Universal Time)`, mientras que `toDateString()` y `toTimeString()` devuelven las partes de fecha y hora de la cadena, respectivamente. `@@toPrimitive` (cuando se pasa `"string"` o `"default"`) llama a `toString()` y devuelve el resultado.
  - Ejemplo:
    ```javascript
    const d = new Date(0);
    console.log(d.toString()); // "Thu Jan 01 1970 00:00:00 GMT+0000 (Coordinated Universal Time)"
    ```

- `toUTCString()`: Devuelve una cadena en el formato `(RFC 7231) Thu, 01 Jan 1970 00:00:00 GMT`.
  - Ejemplo:
    ```javascript
    const d = new Date(0);
    console.log(d.toUTCString()); // "Thu, 01 Jan 1970 00:00:00 GMT"
    ```

- `toLocaleDateString()`, `toLocaleTimeString()` y `toLocaleString()`: Utilizan formatos de fecha y hora específicos de la configuración regional, generalmente proporcionados por la API Intl.
  
  - Ejemplo:
  
    ````javascript
    const date = new Date(Date.UTC(2012, 11, 20, 3, 0, 0));
    
    // formats below assume the local time zone of the locale;
    // America/Los_Angeles for the US
    
    // US English uses month-day-year order
    console.log(date.toLocaleDateString("en-US"));
    // "12/20/2012"
    ````
  
    

## Constructor y Métodos Estáticos

### Constructor

- `Date()`: Cuando se llama como constructor, devuelve un nuevo objeto Date. Cuando se llama como función, devuelve una representación de cadena de la fecha y hora actuales.

  ``````javascript
  new Date()
  new Date(value)
  new Date(dateString)
  new Date(dateObject)
  
  new Date(year, monthIndex, day, hours, minutes, seconds, milliseconds)
  ``````

  

### Métodos Estáticos

- `Date.now()`: Devuelve el valor numérico correspondiente a la hora actual: el número de milisegundos transcurridos desde las 00:00:00 UTC del 1 de enero de 1970, ignorando los segundos intercalares.

  ````javascript
  Date.now();
  // 1519211809934
  ````

  

- `Date.parse()`: Analiza una representación de cadena de una fecha y devuelve el número de milisegundos desde el 1 de enero de 1970, 00:00:00 UTC, ignorando los segundos intercalares.

  ````javascript
  Date.parse("04 December 1995"); // 818031600000 in all implementations
  ````

- `Date.UTC()`: Acepta los mismos parámetros que la forma más larga del constructor (es decir, de 2 a 7) y devuelve el número de milisegundos desde el 1 de enero de 1970 a las 00:00:00 UTC, ignorando los segundos intercalares.

  ````javascript
  Date.UTC(year, monthIndex, day, hour, minute, second, millisecond)
  ````

## Métodos de instancia

- `Date.prototype.getDate()`: Devuelve el día del mes (1-31) para la fecha especificada según la hora local.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getDate()); // Ejemplo de salida: 13
    ```

- `Date.prototype.getDay()`: Devuelve el día de la semana (0-6) para la fecha especificada según la hora local.
  
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getDay()); // Ejemplo de salida: 5
    ```
  
- `Date.prototype.getFullYear()`: Devuelve el año (4 dígitos para años de 4 dígitos) de la fecha especificada según la hora local.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getFullYear()); // Ejemplo de salida: 2024
    ```

- `Date.prototype.getHours()`: Devuelve la hora (0-23) de la fecha especificada según la hora local.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getHours()); // Ejemplo de salida: 14
    ```

- `Date.prototype.getMilliseconds()`: Devuelve los milisegundos (0-999) de la fecha especificada según la hora local.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getMilliseconds()); // Ejemplo de salida: 123
    ```

- `Date.prototype.getMinutes()`: Devuelve los minutos (0-59) de la fecha especificada según la hora local.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getMinutes()); // Ejemplo de salida: 30
    ```

- `Date.prototype.getMonth()`: Devuelve el mes (0-11) en la fecha especificada según la hora local.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getMonth()); // Ejemplo de salida: 1 (febrero)
    ```

- `Date.prototype.getSeconds()`: Devuelve los segundos (0-59) de la fecha especificada según la hora local.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getSeconds()); // Ejemplo de salida: 45
    ```

- `Date.prototype.getTime()`: Devuelve el valor numérico de la fecha especificada como el número de milisegundos desde el 1 de enero de 1970 a las 00:00:00 UTC. (Se devuelven valores negativos para momentos anteriores).
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getTime()); // Ejemplo de salida: 1644743925123
    ```

- `Date.prototype.getTimezoneOffset()`: Devuelve el desplazamiento de la zona horaria en minutos para la ubicación actual.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getTimezoneOffset()); // Ejemplo de salida: -480 (UTC+08:00)
    ```

- `Date.prototype.getUTCDate()`: Devuelve el día (fecha) del mes (1-31) en la fecha especificada según la hora universal.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getUTCDate()); // Ejemplo de salida: 13
    ```

- `Date.prototype.getUTCDay()`: Devuelve el día de la semana (0-6) en la fecha especificada según la hora universal.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getUTCDay()); // Ejemplo de salida: 5
    ```

- `Date.prototype.getUTCFullYear()`: Devuelve el año (4 dígitos para años de 4 dígitos) en la fecha especificada según la hora universal.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getUTCFullYear()); // Ejemplo de salida: 2024
    ```

- `Date.prototype.getUTCHours()`: Devuelve las horas (0-23) de la fecha especificada según la hora universal.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getUTCHours()); // Ejemplo de salida: 6
    ```

- `Date.prototype.getUTCMilliseconds()`: Devuelve los milisegundos (0-999) de la fecha especificada según la hora universal.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getUTCMilliseconds()); // Ejemplo de salida: 123
    ```

- `Date.prototype.getUTCMinutes()`: Devuelve los minutos (0-59) de la fecha especificada según la hora universal.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getUTCMinutes()); // Ejemplo de salida: 30
    ```

- `Date.prototype.getUTCMonth()`: Devuelve el mes (0-11) en la fecha especificada según la hora universal.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getUTCMonth()); // Ejemplo de salida: 1 (febrero)
    ```

- `Date.prototype.getUTCSeconds()`: Devuelve los segundos (0-59) de la fecha especificada según la hora universal.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.getUTCSeconds()); // Ejemplo de salida: 45
    ```

- `Date.prototype.toDateString()`: Devuelve la parte de "fecha" de Date como una cadena legible por humanos como 'Thu Apr 12 2018'.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toDateString()); // Ejemplo de salida: Sat Feb 13 2024
    ```

- `Date.prototype.toISOString()`: Convierte una fecha en una cadena siguiendo el formato extendido ISO 8601.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toISOString()); // Ejemplo de salida: 2024-02-13T06:30:45.123Z
    ```

- `Date.prototype.toJSON()`: Devuelve una cadena que representa el Date uso toISOString(). Diseñado para ser utilizado por JSON.stringify().
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toJSON()); // Ejemplo de salida: 2024-02-13T06:30:45.123Z
    ```

- `Date.prototype.toLocaleDateString()`: Devuelve una cadena con una representación sensible a la localidad de la parte de fecha de esta fecha según la configuración del sistema.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toLocaleDateString()); // Ejemplo de salida: 13/02/2024
    ```

- `Date.prototype.toLocaleString()`: Devuelve una cadena con una representación de esta fecha que depende de la localidad. Anula el Object.prototype.toLocaleString() método.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toLocaleString()); // Ejemplo de salida: 13/02/2024, 06:30:45
    ```

- `Date.prototype.toLocaleTimeString()`: Devuelve una cadena con una representación sensible a la localidad de la parte horaria de esta fecha, según la configuración del sistema.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toLocaleTimeString()); // Ejemplo de salida: 06:30:45
    ```

- `Date.prototype.toString()`: Devuelve una cadena que representa el Date objeto especificado. Anula el Object.prototype.toString() método.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toString()); // Ejemplo de salida: Sat Feb 13 2024 06:30:45 GMT+0800 (Hora de Malasia)
    ```

- `Date.prototype.toTimeString()`: Devuelve la parte de "tiempo" de Date como una cadena legible por humanos.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toTimeString()); // Ejemplo de salida: 06:30:45 GMT+0800 (Hora de Malasia)
    ```

- `Date.prototype.toUTCString()`: Convierte una fecha en una cadena utilizando la zona horaria UTC.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.toUTCString()); // Ejemplo de salida: Sat, 13 Feb 2024 06:30:45 GMT
    ```

- `Date.prototype.valueOf()`: Devuelve el valor primitivo de un Date objeto. Anula el Object.prototype.valueOf() método.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date.valueOf()); // Ejemplo de salida: 1644743925123
    ```

- `Date.prototype[@@toPrimitive]()`: Convierte este Date objeto en un valor primitivo.
  - Ejemplo:
    ```javascript
    const date = new Date();
    console.log(date[@@toPrimitive]()); // Ejemplo de salida: Sat Feb 13 2024 06:30:45 GMT+0800 (Hora de Malasia)
    ```

# Ejemplos

## Distintas maneras de crear un objeto Date

Los siguientes ejemplos muestran distintas maneras de crear fechas en JavaScript:

- **Ejemplo 1:** Utilizando la fecha actual del sistema:
  ```javascript
  const fechaActual = new Date();
  console.log(fechaActual);
  ```

- **Ejemplo 2:** Creando una fecha específica con año, mes y día:
  ```javascript
  const fechaEspecifica = new Date(2024, 1, 13); // El mes es 0-indexado, por lo que 1 representa febrero
  console.log(fechaEspecifica);
  ```

- **Ejemplo 3:** Creando una fecha a partir de una cadena de texto:
  ```javascript
  const fechaDesdeString = new Date("2024-02-13T07:55:40");
  console.log(fechaDesdeString);
  ```

- **Ejemplo 4:** Creando una fecha utilizando milisegundos desde el Epoch (1 de enero de 1970):
  ```javascript
  const fechaDesdeEpoch = new Date(1707828940355);
  console.log(fechaDesdeEpoch);
  ```

- **Ejemplo 5:** Obtener la hora actual en UTC y ajustarla a la zona horaria de Colombia (GMT-5):
  ```javascript
  const nowUTC = new Date();
  const horaColombia = new Date(nowUTC.toLocaleString("en-US", {timeZone: "America/Bogota"}));
  const hora = horaColombia.getHours();
  const minutos = horaColombia.getMinutes();
  const segundos = horaColombia.getSeconds();
  console.log(`${hora}:${minutos}:${segundos}`);
  ```

Estos ejemplos proporcionan diferentes formas de crear objetos `Date` en JavaScript para adaptarse a diversas necesidades de tu aplicación.
