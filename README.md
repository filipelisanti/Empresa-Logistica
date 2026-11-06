# MandáTodo Logística

Sistema web para una empresa de logística de última milla que recibe pedidos por WhatsApp, Instagram, correo y otros canales. Su objetivo principal es **normalizar y geolocalizar las direcciones de envío** para evitar viajes fallidos, y acompañar el pedido desde la carga hasta la entrega y el cobro.

Proyecto académico PPP1 · Grupo 9 · Caso 7.

## Qué hace

### Usuarios y acceso
- Inicio de sesión con cuentas individuales y token JWT.
- Tres roles con permisos diferenciados: **Administrador**, **Operador** y **Chofer**. Los permisos se validan en el servidor.
- ABM de usuarios (solo administrador).

### Clientes
- ABM de clientes con búsqueda por nombre, DNI, teléfono o email.
- Normalización del DNI y rechazo de DNI duplicados; aviso (sin fusión automática) ante teléfono o email repetidos.
- Libreta de direcciones por cliente para reutilizar direcciones de envíos anteriores.

### Pedidos y direcciones
- Carga manual de pedidos con dirección estructurada (calle, altura, piso/depto, entre calles, localidad, provincia, código postal) y canal de origen.
- Normalización de provincias y localidades argentinas (24 jurisdicciones, catálogo de localidades).
- Geocodificación de la dirección y previsualización de la ubicación en un mapa durante la carga.
- **Confirmación humana obligatoria** de la ubicación: un empleado revisa el punto en el mapa y la confirma o la rechaza. Si la dirección cambia, la confirmación se invalida.
- Bandeja de revisión de direcciones pendientes.
- Alerta de pedidos potencialmente duplicados (mismo cliente y misma dirección en una ventana de tiempo).
- Listado general de pedidos con filtros por estado, estado de validación, cliente y fechas.

### Tarifas e importes
- Configuración del precio por kilómetro y de la sucursal de origen (administrador).
- Importe sugerido según la distancia entre la sucursal y el punto de entrega, también durante la carga.

### Asignación y entrega
- Asignación manual de pedidos a choferes (solo con dirección confirmada y chofer activo).
- Cambios de estado de preparación y despacho con historial de estados.
- Vista del chofer con sus pedidos asignados, registro de entrega y de pago.
- Carga de comprobantes de pago por parte del chofer y acreditación del pago por el administrador.

### Exportación e importación
- Exportación de la información de un pedido y de su mapa a PDF.
- Importación del histórico de pedidos desde Excel, con saneamiento de datos.

## Tecnologías

| Capa | Tecnologías |
| --- | --- |
| Frontend | React 19, Vite 8, React Router 7, Axios, Leaflet + React Leaflet (mapas), jsPDF y pdf.js (PDF), ESLint, Vitest |
| Backend | Node.js 24, Express 5 (CommonJS), JSON Web Token, bcryptjs (hash de contraseñas), Zod (validación), mysql2, xlsx (importación de Excel), dotenv |
| Base de datos | MySQL 8.4 con migraciones versionadas |
| Geolocalización | API Georef (datos geográficos oficiales de Argentina) y mapas Leaflet; adaptadores alternativos preparados para Nominatim y Google |
| Infraestructura | Docker y Docker Compose (servicios MySQL, backend y frontend) |

## Estructura

| Carpeta | Contenido |
| --- | --- |
| `frontend/` | Aplicación web React (páginas, componentes, cliente de API, sesión y guardas por rol) |
| `backend/` | API REST Express organizada en rutas, controladores, servicios y repositorios |
| `database/` | Esquema y migraciones SQL |
| `docs/` | Documentación del proyecto: contexto, arquitectura, decisiones y tareas |

## Arranque

Instalación, Docker, migraciones y ejecución local en [docs/arranque.md](docs/arranque.md).
