# AgentHub: especificacion del prototipo

## 1. Producto y usuario

AgentHub es un panel web para que un administrador gestione agentes de IA, sus habilidades y las integraciones que utilizan. El prototipo permite recorrer las tareas administrativas habituales y consultar actividad reciente mediante datos de demostracion; no se conecta a servicios reales.

El usuario principal es el administrador del espacio de trabajo. Necesita entender de un vistazo el estado de sus agentes, encontrar configuraciones con rapidez y realizar cambios sencillos con confirmacion visible.

## 2. Alcance y restricciones tecnicas

- La interfaz se construye con HTML semantico, Tailwind CSS cargado desde CDN y JavaScript vanilla.
- No se usan frameworks, bibliotecas de componentes, compiladores ni backend. `server.py` puede servir los archivos estaticos durante el desarrollo, pero la aplicacion no depende de el para su logica.
- Las entidades y metricas son datos locales de demostracion. Las modificaciones pueden persistirse en `localStorage`; no se presentan como cambios enviados a un servidor.
- Las seis vistas de la aplicacion son Dashboard, Agents, Skills, Integrations, Activity y Settings.
- La interfaz debe funcionar con teclado y en pantallas estrechas, ademas de escritorio. Los controles interactivos tendran etiquetas accesibles y estados visibles de foco.

## 3. Estructura global y lenguaje visual

- La aplicacion usa una barra lateral persistente con la marca AgentHub, las seis entradas de navegacion, un indicador de vista activa y el control de modo oscuro. En movil, la barra lateral se convierte en un menu plegable que se puede abrir y cerrar.
- El area principal muestra el titulo de la vista, una descripcion corta cuando aporte contexto y las acciones propias de esa vista. Cambiar de seccion actualiza la vista activa sin recargar la pagina.
- El estilo es el de una herramienta operativa: jerarquia tipografica compacta, tablas faciles de escanear, divisores sutiles y color reservado para estados o acciones. Los estados se distinguen por texto e icono, no solo por color.
- Se mantiene un espaciado consistente y un contraste legible. Las tarjetas usan esquinas discretas; los dialogos y menus no se recortan en los bordes de pantalla.

## 4. Especificaciones por seccion

### 4.1 Dashboard

1. **Cuadricula de metricas:** mostrar cuatro tarjetas en una cuadricula 2x2 en escritorio y una columna en movil. Cada tarjeta contiene icono, etiqueta y valor de demostracion: `Total agents` (12), `Active agents` (8), `Runs this week` (1,284) y `Success rate` (98.6%).
2. **Acentos por metrica:** cada tarjeta usa un color de acento distinto para el icono y el indicador de tendencia. Incluye una comparacion breve con el periodo anterior; un valor positivo o negativo se expresa con texto y no unicamente con color.
3. **Actividad semanal:** debajo de las metricas, mostrar un grafico de barras de siete dias con el total de ejecuciones por dia. El encabezado incluye el titulo `Weekly activity` y el total del periodo; las etiquetas de dia y los valores se pueden consultar sin depender de pasar el puntero.
4. **Agentes recientes:** una lista compacta de los tres agentes usados mas recientemente muestra nombre, estado, ultima ejecucion y enlace a `Agents`.

### 4.2 Agents

1. **Listado de agentes:** mostrar una tabla con nombre, descripcion corta, estado, habilidades asignadas, ultima ejecucion y menu de acciones. Incluir al menos cuatro filas de demostracion y un encabezado por columna.
2. **Busqueda y filtros:** un campo de busqueda filtra por nombre; un selector filtra por estado (`All`, `Active`, `Paused`). Los filtros se pueden combinar y un mensaje de estado indica cuando no hay coincidencias.
3. **Alta y edicion:** el boton `New agent` abre un modal con campos de nombre, descripcion y estado. Guardar agrega o actualiza la fila local; cancelar o cerrar descarta los cambios. Los campos requeridos muestran validacion junto al campo.
4. **Acciones por fila:** el menu desplegable permite editar, activar/pausar y eliminar. Eliminar solicita confirmacion en un modal; activar/pausar actualiza inmediatamente el badge de estado y la lista.

### 4.3 Skills

1. **Catalogo agrupado:** listar habilidades de demostracion agrupadas por categoria, con nombre, descripcion, cantidad de agentes que la usan y badge de disponibilidad.
2. **Lista plegable:** cada categoria tiene un encabezado accionable que expande o contrae su lista. El estado expandido se comunica con icono y `aria-expanded`; inicialmente la primera categoria esta abierta.
3. **Detalle de habilidad:** seleccionar una habilidad abre un panel o modal con su descripcion completa, agentes que la tienen asignada y boton para volver al catalogo.
4. **Asignacion local:** un control permite asignar o quitar la habilidad de un agente seleccionado. La cantidad de usos y la lista relacionada se actualizan en la interfaz.

### 4.4 Integrations

1. **Directorio de integraciones:** mostrar al menos cuatro integraciones ficticias en una lista o tabla con nombre, proposito, estado (`Connected` o `Not connected`) y accion disponible.
2. **Conectar y desconectar:** el boton de cada fila alterna su estado localmente y actualiza el texto del boton y el badge. Ningun control solicita credenciales reales ni afirma que se conecto a un servicio externo.
3. **Configuracion simulada:** `Configure` abre un modal con opciones de demostracion propias de la integracion. Guardar conserva los valores localmente; cancelar los descarta.
4. **Estado vacio y filtro:** un filtro por estado reduce el directorio. Cuando no haya coincidencias, se muestra un mensaje claro y una accion para limpiar el filtro.

### 4.5 Activity

1. **Registro de eventos:** mostrar una tabla cronologica con fecha y hora, actor, accion, recurso y resultado. Los eventos iniciales son ficticios y cubren ejecuciones, cambios de estado y ediciones.
2. **Filtros del registro:** incluir filtros por tipo de evento y resultado, mas busqueda por agente o actor. Cambiar filtros actualiza las filas sin recargar la pagina.
3. **Detalle de evento:** seleccionar una fila abre un modal de solo lectura con los campos completos del evento y un boton para cerrarlo.
4. **Orden y ausencia de resultados:** la actividad mas reciente aparece primero. Si los filtros no encuentran eventos, se muestra un estado vacio que permite restablecerlos.

### 4.6 Settings

1. **Perfil del espacio de trabajo:** mostrar y permitir editar el nombre del espacio de trabajo y el nombre del administrador en un formulario local. Guardar presenta confirmacion visible y mantiene los valores durante la sesion.
2. **Preferencias de notificacion:** usar controles tipo checkbox o toggle para notificaciones de ejecuciones fallidas y resumen semanal. Cada control refleja su estado y actualiza la preferencia local.
3. **Modo oscuro:** un toggle accesible alterna entre tema claro y oscuro en toda la aplicacion; la seleccion persiste en `localStorage` y se aplica al volver a cargar.
4. **Zona de acciones:** incluir `Reset demo data`, que abre un modal de confirmacion. Confirmar restaura los datos iniciales; cancelar cierra el modal sin cambios.

## 5. Inventario de componentes reutilizables

- **Sidebar y navegacion:** enlaces a las seis vistas, indicador de seleccion y variante plegable para movil.
- **Encabezado de vista:** titulo, texto de contexto opcional y espacio para acciones principales.
- **Tarjeta de metrica:** icono, etiqueta, valor, comparacion del periodo y color de acento; se reutiliza en Dashboard.
- **Badge de estado:** texto e indicador visual para estados de agentes, integraciones y resultados.
- **Campo de busqueda y filtros:** controles etiquetados que pueden combinarse y exponer su estado.
- **Tabla/lista de registros:** encabezados, filas, estado vacio y acciones por elemento.
- **Dropdown de acciones:** menu asociado a un boton, navegable con teclado y cerrado al seleccionar una accion o hacer clic fuera.
- **Modal/dialogo:** titulo, contenido, acciones primarias/secundarias, cierre con boton y tecla Escape; al abrir, el foco entra al dialogo y al cerrar vuelve al control que lo abrio.
- **Lista de skills plegable:** encabezado con indicador de expansion y region asociada.
- **Toggle de modo oscuro:** control con nombre accesible, estado actual visible y persistencia local.
- **Toast de confirmacion:** mensaje breve para indicar que una accion local se completo o fallo por validacion.
- **Estado vacio:** mensaje y accion contextual para recuperar una lista filtrada sin resultados.

## 6. Criterios de aceptacion

1. La aplicacion presenta exactamente las seis secciones especificadas y cada entrada de navegacion muestra su vista correspondiente y estado activo.
2. El Dashboard muestra cuatro tarjetas de metricas en cuadricula 2x2 en escritorio y distribucion de una columna en movil, con icono, etiqueta, valor y acento diferenciable en cada una.
3. El grafico de actividad semanal muestra siete dias, valores legibles y el total semanal; la informacion no depende exclusivamente de color o hover.
4. En Agents, buscar y filtrar por estado actualiza la tabla; crear, editar, pausar/activar y eliminar realizan la accion local prevista, y eliminar siempre pide confirmacion.
5. En Skills, cada categoria se puede expandir y contraer con teclado o puntero y comunica el estado con `aria-expanded`.
6. En Integrations, conectar/desconectar cambia el estado visible sin llamadas de red ni solicitud de secretos reales.
7. En Activity, busqueda y filtros se pueden combinar, los eventos se ordenan del mas reciente al mas antiguo y una consulta sin resultados ofrece limpiar filtros.
8. En Settings, guardar el perfil muestra confirmacion; las preferencias responden al cambio; el tema oscuro se aplica a todas las vistas y persiste tras recargar.
9. Dropdowns y modales se pueden abrir y cerrar con controles accesibles; los modales cierran con Escape, gestionan el foco y las acciones destructivas requieren confirmacion.
10. Todas las vistas mantienen texto y controles dentro del viewport en movil y escritorio, sin solapamientos ni desplazamiento horizontal de la pagina a un ancho de 320 px.
11. Todas las acciones interactivas tienen etiqueta accesible, foco visible y resultado perceptible. Estados como activo, pausado, conectado o fallido incluyen texto, no solo una variacion de color.
12. La aplicacion funciona con HTML, Tailwind CSS por CDN y JavaScript vanilla; no importa frameworks, no requiere backend y no hace peticiones de red para sus datos de demostracion.