# Bitácora de Cambios Técnicos - Cuidado Seguro

Este documento detalla todas las modificaciones realizadas en los servicios del ecosistema **Cuidado Seguro** 

---

## 1. Estandarización de Base de Datos (MySQL)

Se unificaron las credenciales de conexión en todos los microservicios para evitar inconsistencias locales o credenciales conflictivas procedentes del control de versiones.

* **Estado Anterior:**
  - `CuidadoSeguroPaciente`: credenciales variables o erróneas en `application.properties`.
  - `CuidadoSeguro_Auth`: conflictos de marcadores Git (`<<<<<<< Updated upstream`) y configuraciones de contraseña incorrectas en `application.yml`.
  - `datos-medicos-service`: credenciales arbitrarias en `application.properties`.
* **Estado Actual (Estándar General):**
  - **Servidor:** `localhost:3306`
  - **Usuario:** `root`
  - **Contraseña:** *(Vacía / Sin contraseña)*
* **Archivos Modificados:**
  - [CuidadoSeguroPaciente: application.properties](file:///C:/Users/Marcelo-HP/Desktop/Kari/CuidadoSeguroPaciente/src/main/resources/application.properties)
  - [CuidadoSeguro_Auth: application.yml](file:///C:/Users/Marcelo-HP/Desktop/Kari/CuidadoSeguro_Auth/src/main/resources/application.yml)
  - [datos-medicos-service: application.properties](file:///C:/Users/Marcelo-HP/Desktop/Kari/datos-medicos-service/src/main/resources/application.properties)

---

## 2. Resolución del Error `HttpMediaTypeNotSupportedException` (Causa Raíz)

### Problema Técnico
Al guardar registros de *Antropometría* o *Signos Vitales*, la API respondía con un error `500` e indicaba que el content-type `application/json;charset=UTF-8` no estaba soportado. 

La causa real no residía en las cabeceras HTTP, sino en un **conflicto de referencias de Jackson** durante la deserialización de la entidad `FichaClinica`:
- `FichaClinica` poseía tres relaciones `@OneToMany` marcadas con `@JsonManagedReference` sin un nombre específico (lo que asigna automáticamente el nombre `"defaultReference"`).
- Una de estas listas correspondía a `List<Medicamento> medicamentos`. Sin embargo, la clase `Medicamento.java` definía el campo `ficha` como un simple `String` en lugar de una relación `@ManyToOne` con `@JsonBackReference`.
- Al recibir una solicitud para deserializar `Antropometria` o `ExamenClinico`, Jackson intentaba enlazar la relación `@JsonBackReference` genérica con la lista de medicamentos en `FichaClinica`, lanzando un error de definición de mapeo (`InvalidDefinitionException`) que Spring Boot convertía erróneamente en un fallo de soporte de Content-Type.

### Soluciones Implementadas:

#### A. Ajuste de Mapeo y Referencias en Modelos (`datos-medicos-service`)
- **Modificación en [FichaClinica.java](file:///C:/Users/Marcelo-HP/Desktop/Kari/datos-medicos-service/src/main/java/datosmedicos_service/model/FichaClinica.java):**
  - Se eliminó el decorador `@JsonManagedReference` del campo `medicamentos` (línea 35-37), ya que no es una relación bidireccional de objetos (es un mapeo simple de base de datos a string).
  - Se nombraron explícitamente las referencias manejadas restantes para evitar colisiones:
    - `antropometrias` se marcó con `@JsonManagedReference("ficha-antropometrias")` (línea 40).
    - `examenes` se marcó con `@JsonManagedReference("ficha-examenes")` (línea 44).
- **Modificación en [Antropometria.java](file:///C:/Users/Marcelo-HP/Desktop/Kari/datos-medicos-service/src/main/java/datosmedicos_service/model/Antropometria.java):**
  - Se actualizó el decorador en el campo `ficha` a `@JsonBackReference("ficha-antropometrias")` (línea 33).
- **Modificación en [ExamenClinico.java](file:///C:/Users/Marcelo-HP/Desktop/Kari/datos-medicos-service/src/main/java/datosmedicos_service/model/ExamenClinico.java):**
  - Se actualizó el decorador en el campo `ficha` a `@JsonBackReference("ficha-examenes")` (línea 38).

#### B. Eliminación de Filtros de Entrada Consumes/Produces Restrictivos
- **Modificación en [AntropometriaController.java](file:///C:/Users/Marcelo-HP/Desktop/Kari/datos-medicos-service/src/main/java/datosmedicos_service/controller/AntropometriaController.java):**
  - Se removió `consumes = MediaType.APPLICATION_JSON_VALUE` y `produces = MediaType.APPLICATION_JSON_VALUE` del `@PostMapping("/{fichaId}")` (línea 24) para dar soporte nativo a las variantes extendidas de JSON enviadas por `RestTemplate`.
- **Modificación en [ExamenClinicoController.java](file:///C:/Users/Marcelo-HP/Desktop/Kari/datos-medicos-service/src/main/java/datosmedicos_service/controller/ExamenClinicoController.java):**
  - Se removieron los atributos restrictivos de consumes y produces tanto en el `@PostMapping` de guardar (línea 27) como en el `@PutMapping` de actualizar (línea 39).
- **Modificación en [AntropometriaController.java (BFF)](file:///C:/Users/Marcelo-HP/Desktop/Kari/bff-cuidadoseguro/src/main/java/com/cuidadoseguro/bff_cuidadoseguro/controller/AntropometriaController.java):**
  - Se retiró el filtro `consumes = "application/json"` en el `@PostMapping` de la pasarela BFF (línea 20) para permitir transferir solicitudes del frontend que contengan el juego de caracteres explícito.

---

## 3. Mejoras y Correcciones en Frontend (`cuidado-seguro-react`)

### A. Corrección en el Historial de Signos Vitales
* **Problema:** En el panel del profesional, la columna de **Fecha** y **Hora** dentro de la tabla de registros históricos de signos vitales no renderizaba valores (mostraba `--`).
* **Causa:** El código de frontend intentaba separar una propiedad llamada `registro.fecha` (la cual venía vacía/indefinida desde el backend). El modelo oficial de base de datos guarda este valor en la columna `fecha_registro`, mapeada en el JSON como `fechaRegistro`.
* **Modificación en [HistorialSignosVitales.jsx](file:///C:/Users/Marcelo-HP/Desktop/Kari/cuidado-seguro-react/src/components/profesional/HistorialSignosVitales.jsx):**
  - Se reemplazó el split de `registro.fecha` por la instanciación de un objeto `Date` leyendo directamente `registro.fechaRegistro`.
  - Se aplicaron formateadores de localización local para renderizar de manera limpia la fecha y hora:
    ```javascript
    const fechaCompleta = registro.fechaRegistro ? new Date(registro.fechaRegistro) : null;
    const fecha = fechaCompleta ? fechaCompleta.toLocaleDateString("es-CL") : "--";
    const hora = fechaCompleta ? fechaCompleta.toLocaleTimeString("es-CL", {
      hour: "2-digit",
      minute: "2-digit",
    }) : "--";
    ```

### B. Vinculación de Profesional en el Registro de Antropometría
* **Problema:** Al enviar un registro antropométrico al backend, la propiedad `profesional` no se almacenaba en la base de datos, dejando la columna como nula.
* **Modificación en [FormularioAntropometria.jsx](file:///C:/Users/Marcelo-HP/Desktop/Kari/cuidado-seguro-react/src/components/profesional/FormularioAntropometria.jsx):**
  - Se añadió la propiedad `profesional` al payload JSON enviado dentro de la llamada `request()` (línea 42-45) para vincular correctamente al médico/enfermero que realiza la medición.
