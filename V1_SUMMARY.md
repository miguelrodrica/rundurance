# Rundurance — Versión 1.0 Especificación y Reglas de Negocio

---

## 1. Contexto y Propósito
Rundurance es una plataforma interna—no SaaS—diseñada exclusivamente para facilitar la administración y operación de la empresa Rundurance, cuyo dueño y único administrador es Mauricio. La plataforma busca centralizar la información financiera y operativa en torno a la gestión de clientes (“atletas”) pagadores. Este documento es la fuente única de requerimientos, reglas de negocio y arquitectura para la versión 1.0.

## 2. Alcance de la Versión 1
- Acceso y gestión solo por Mauricio (Owner).
- No hay roles activos de entrenador ni atleta; sólo prevista su existencia en el modelo/diseño futuro.
- No incluye portal de atleta ni feedback IA.
- Funcionalidad: gestión básica administrativa/financiera (clientes, pagos, alertas de cobro, dashboard de control).

## 3. Roles
| Rol       | Descripción                                           | V1 permitido |
|-----------|-------------------------------------------------------|--------------|
| Owner     | Mauricio, acceso a toda la plataforma y administración| Sí           |
| Entrenador| Preparado para futuro, sin acceso/UI                  | No           |
| Atleta    | Solo registro administrativo en BD, sin portal propio | No           |

## 4. Procesos de Negocio — Flujos Principales
- **Landing page** informativa y con medios de contacto para prospectos.
- **Login:** ingreso seguro, sólo para owner (email + clave). 
- **Alta de cliente:** agregar nuevo cliente pagador (nombre, contacto, monto, ciclo, fecha corte).
- **Dashboard financiero:** visualización global de todos los clientes, sus pagos, vencimientos y estados.
- **Registro de pago:** entrada de pago manual (fecha, monto, método, comentario).
- **Alertas de cobro/estado automático:** actualización de estado del cliente según fechas clave (ver reglas).
- **Listado de clientes en alerta/vencido:** soporte para gestión manual de cobro/contacto.

## 5. Reglas de Negocio
- Un "cliente" es toda persona que paga mensualidad, asociada a sus datos y registro histórico de pagos.
- Estados financieros del cliente respecto a la mensualidad:
    - `Pagó`: pago mensual asentado.
    - `Alerta`: 3 días antes de la fecha límite si no ha pagado.
    - `Vencido`: día después de la fecha límite si sigue sin pago.
- Fechas límite y periodo de alerta calculadas individualmente por cliente.
- Al registrar pago, el estado vuelve a `Pagó` y se recalcula próxima fecha límite.

## 6. Arquitectura del Sistema
- **Cliente:** Navegador web (dashboard privado + landing estática informativa).
- **Servidor:** Node.js + Express. Monolítico, dividido por capas (MVC extendido: rutas, middlewares, controladores, modelos, servicios).
- **Base de datos:** PostgreSQL 16+ (tabla usuarios, clientes, pagos, etc).
- **Despliegue:** Monolito en VPS Cloud; arquitectura pensada para desplegarse en contenedor o ambiente autoalojado.
- **Comunicación:** Métodos HTTP REST puro (sin GraphQL, RPC ni sockets).
- **Almacenamiento de archivos:** Local en VPS (no S3 en v1).
- **Seguridad:** Auth-JWT + bcryptjs para credenciales; .env excluido de git.
- **Backups:** Cron job (pg_dump + rsync). Se sugiere investigar soporte de snapshots automáticos de la VPS.

## 7. Tech Stack
| Capa           | Tecnología                                     |
|----------------|------------------------------------------------|
| Frontend       | Vanilla JS, HTML5, Tailwind CSS (con build), Bootstrap Icons |
| Backend        | Node.js + Express                              |
| Base de datos  | PostgreSQL (v16+)                              |
| Almacenamiento | Local VPS                                      |
| Automatización | n8n (Reservado/futuro, no activo en v1)        |
| Backup         | Cron + pg_dump/rsync + (snapshots si VPS los da)|
| Auth           | JWT + bcryptjs                                 |
| Archivos       | multer + fit-file-parser                       |

## 8. Modelo de Datos Inicial (Entidades principales)
| Entidad | Campos clave                                                         |
|---------|----------------------------------------------------------------------|
| Usuario | id, nombre, email, rol, password_hash                                |
| Cliente | id, nombre, contacto, monto_mensual, ciclo, prox_fecha_corte, estado_pago       |
| Pago    | id, cliente_id, fecha_pago, monto, método, comentario                |

## 9. Ejemplo de Flujo: Ciclo de Estados Pago

```
1. Mauricio registra manualmente un nuevo cliente (alta).
2. El sistema calcula su primera fecha de corte, estado='Alerta' o 'Por pagar'.
3. Cuando faltan 3 días para fecha de corte, cliente pasa a estado=“Alerta”.
4. Si vence la fecha de corte y no hay pago registrado, cambia a “Vencido”.
5. Cuando se registra pago, retorna a “Pagó” y se reinicia ciclo para el mes siguiente.
```

## 10. Reglas de Seguridad y Buenas Prácticas
- Solo el owner accede al dashboard/admin.
- Nunca exponer credenciales o datos sensibles.
- Proteger todas las rutas de backend con middleware auth.
- Plan de backups y restauración con cron/documentación.

## 11. Consideraciones / Roadmap
- La arquitectura permitirá en próximos releases crecer hacia portal de atletas, nuevos roles (entrenador), integración con automatizaciones (n8n/notificaciones), feedback avanzado, y almacenamiento externo (S3, etc).
- Este archivo sirve de contrato inicial y debe actualizarse con cada pivot o cambio mayor.

---

Documentación creada y validada — Agosto 2026. Consultar ramas `legacy-mvp` para el MVP original y `MAPEO_CASOS_USO.md` para detalles de reglas y casos históricos.