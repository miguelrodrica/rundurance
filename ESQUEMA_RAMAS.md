# Organización de Ramas Rundurance — Agosto 2026

## Contexto
A partir de la nueva fase de desarrollo de la plataforma Rundurance, se establecen las siguientes ramas para orden, trazabilidad histórica y prácticas estándar de trabajo en equipo. Este flujo asegura que la rama principal/main sólo contenga código aprobado y listo para producción, al tiempo que se conserva la historia del MVP inicial y se permite desarrollo estructurado hacia adelante.

---

## Estructura de Ramas

| Rama         | Propósito                                                      |
|--------------|----------------------------------------------------------------|
| main         | Rama "release". Sólo código listo/deployable a producción.     |
| dev          | Integración/QA de nuevas features y fixes antes de pasar a main |
| legacy-mvp   | Respaldo inmutable de la versión MVP original. No se modifica.  |
| v1-inicio    | Nuevo inicio del proyecto, base de desarrollo 2026+.            |


### Flujo de trabajo recomendado
1. **legacy-mvp**: Rama congelada a partir de main antes de la reestructuración actual; nunca se modifica. Sirve de historial técnico.
2. **v1-inicio**: Marca el comienzo de la nueva fase; cuidado a partir de aquí en ramas de features/fixes.
3. **dev**: Se usa para consolidar desarrollo de features, pruebas QA/código, integración continua. Sólo se mergea a main cuando el código está estable.
4. **main**: Únicamente recibe merges de dev para releases o despliegue.
5. **feature/**, **fix/**, **hotfix/**: Crea ramas hijas así para features o correcciones específicas y merges sólo hacia dev (luego a main tras pruebas).


---

## Procedimiento de reestructuración aplicado

1. Congelamiento del MVP anterior en la rama `legacy-mvp`.
2. Creación de la rama base para la nueva etapa (`v1-inicio`).
3. Creación de la rama de integración y QA (`dev`) a partir de `v1-inicio`.
4. Documentación de este esquema y commit único de reestructuración.

---

## Convenciones
- Los merges a main sólo desde dev y bajo control. Nunca se codea directo a main.
- El MVP histórico está siempre disponible en legacy-mvp: ninguna nueva funcionalidad ni bugfix aplica sobre esa rama.
- Se recomienda documentar los PRs y feature branches creados en cada etapa temporal, así como mantener limpio el árbol de ramas borrando feature/* una vez integrados.


---

_Última actualización: Agosto 2026. Cambios futuros deben agregarse/consolidarse en este documento._
