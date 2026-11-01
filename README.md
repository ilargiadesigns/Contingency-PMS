# Panel de Contingencia para OPERA

Una página web de un solo fichero para seguir trabajando en recepción **cuando OPERA PMS no está disponible**. Sin instalación, sin servidor, sin conexión a internet.

> **ES** · Instrucciones en español · **EN** · [English summary below](#english-summary)

## Para qué sirve

Cargas los informes que hayas exportado de OPERA y trabajas con ellos como en un mini-PMS:

- **Habitaciones**: tablero por plantas con estado de housekeeping y huésped alojado, varios días.
- **Llegadas**: asigna habitación a una llegada (solo entre las libres durante toda la estancia y listas) y da check-in de contingencia.
- **Salidas**: da de out; la habitación pasa a vacía y sucia.
- **Housekeeping**: cambia el estado de una habitación cuando housekeeping te avisa por teléfono.
- **Avisos (traces)** por departamento, enlazados con las llegadas.
- **Resumen de turno** imprimible: lo que hay que pasar a OPERA cuando el sistema vuelva.
- Copia de seguridad en `.json`.

## Cómo se usa (3 pasos)

1. **Abre `index.html`** con Chrome, Edge, Firefox o Safari (doble clic).
2. **Arrastra los informes `.txt`** a la página (o «Cargar informes»). La app reconoce cada informe por sus columnas, no por el nombre del fichero. ¿Primera vez? Pulsa **«Probar con datos de ejemplo»**.
3. **Trabaja.** Toca una habitación, una llegada o una salida.

> 💡 **Prepárate antes de la caída.** Los informes hay que exportarlos *antes*, mientras OPERA funciona. Exporta el plano de habitaciones **empezando hoy y con una semana por delante**. También puedes guardar `index.html` en un USB o en el escritorio de recepción.

## Qué informes necesita

Todos se exportan desde OPERA con salida **Delimited Data** (datos delimitados, separados por tabulador) y se guardan como `.txt`. Un PDF o un Excel no sirven.

| Informe | Necesario | Columnas que usa |
|---|---|---|
| Plano de habitaciones (Room Plan, p. ej. `RESROOMPLAN`) | **Sí** | `ROOM, ROOM_TYPE, ROOM_STATUS, ORA_DATE, CHAR_D, DAY, GUEST` |
| Llegadas (p. ej. B104 / Reservation Detail) | No | `CONFIRMATION_NO, FULL_NAME_NO_SHR_IND, ROOM_NO, ARRIVAL, DEPARTURE, ROOM_CATEGORY_LABEL, RESV_NAME_ID` |
| Salidas | No | `GUEST_NAME, ROOM, NIGHTS, ARRIVAL, BALANCE, RESV_STATUS` |
| Estado real de habitaciones (Room Status / T120) | No | `ROOM, ROOM_TYPE, ROOM_STATUS, ROOM_RESV_STATUS_DESC` |
| Avisos (Traces) | No | `ROOM, GUEST_NAME, TRACE_TEXT, DEPT_ID, RESV_NAME_ID` |

Los códigos y menús exactos pueden variar según la versión de OPERA y la configuración de cada hotel. Cualquier informe equivalente que incluya esas columnas vale.

## Ajustes

En **«Datos y ajustes»**:

- **Cuándo se puede asignar/dar check-in**: solo *Inspeccionada* (por defecto), *Limpia o Inspeccionada*, o cualquiera salvo fuera de servicio/bloqueada.
- Copia de seguridad (descargar / importar).
- **Borrar todos los datos.**

## Privacidad y seguridad

- La página **no hace ninguna petición de red**: no usa servidores, librerías externas, cookies ni analítica. Puedes comprobarlo: es un único fichero HTML legible.
- Los datos viven **solo en la memoria de la pestaña**. Al cerrarla se pierden (la app avisa si hay cambios hechos a mano sin guardar).
- Lo único que se guarda en el navegador es el ajuste del criterio «lista para asignar».
- Los informes y las copias `.json` contienen **datos personales de huéspedes**. Antes de usar datos reales, consulta con el equipo de TI / protección de datos de tu hotel. Usa equipos de confianza y pulsa «Borrar todos los datos» al terminar.

## Limitaciones (importante)

- **No escribe en OPERA** ni se conecta a él. Es un apoyo temporal: al volver el sistema, hay que registrar en OPERA lo hecho (el «Resumen de turno» lo lista).
- Solo ve lo que haya en los informes cargados. No gestiona facturación, pagos ni historiales.
- La disponibilidad solo se comprueba dentro de los días del plano cargado (la app avisa de las noches no verificables).
- Se asume que el primer día del plano de habitaciones es **hoy**.
- Formatos de fecha reconocidos: `DD-MM-AA`, `MM/DD/AA`, `AAAA-MM-DD` y `DD-MMM-AA`.
- Interfaz solo en español por ahora.
- En hoteles con habitaciones numéricas se ignoran los códigos no numéricos del plano (piscina, spa…).

## Para desarrolladores

Todo está en `index.html`: HTML + CSS + JavaScript sin dependencias. Los *parsers* leen las cabeceras de columna, así que el orden de las columnas no importa. Cualquier mejora es bienvenida.

## Aviso legal

Herramienta independiente, no afiliada, patrocinada ni respaldada por Oracle. *OPERA* es marca registrada de Oracle y se menciona solo para indicar compatibilidad. Software libre bajo licencia MIT (ver `LICENSE`), **sin garantía de ningún tipo**: úsalo bajo tu responsabilidad y verifica siempre los datos críticos.

---

## English summary

**Contingency Panel for OPERA** is a single-file offline web page for front desks to keep working while OPERA PMS is down. Open `index.html` in any modern browser, drag your exported OPERA *Delimited Data* `.txt` reports onto the page (reports are auto-detected from their column headers), and work from a room board, arrivals (assign room + contingency check-in), departures (check-out), housekeeping status updates, traces, and a printable shift summary to re-enter into OPERA afterwards.

- Only the Room Plan report is required; arrivals, departures, room status and traces are optional.
- **Export your reports before the outage** – you cannot run them once OPERA is down. Request the room plan starting today with about a week ahead.
- No network calls, no dependencies; data lives in browser memory only (use *Delete all data* when done). Reports contain guest personal data: check with your IT/data-protection team first.
- It **does not write to OPERA**. Currently the interface is Spanish only.
- Independent tool, not affiliated with or endorsed by Oracle. OPERA is a trademark of Oracle. MIT licensed, provided "as is" without warranty.
