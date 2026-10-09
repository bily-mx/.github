# Estándar de trabajo con GitHub en Profact

## 1. Propósito

Este documento define el flujo esperado para los repositorios de Profact.

Asana es la fuente principal para planeación, prioridad, responsables y seguimiento funcional. GitHub es la fuente principal para código, ramas, Pull Requests, revisión e historial técnico.

Antes de trabajar en cualquier repositorio de Profact, cada colaborador debe completar el proceso descrito en [`ONBOARDING.md`](./ONBOARDING.md).

## 2. Rama principal

La rama principal es `main`.

`main` está protegida por política y no se utiliza como rama de desarrollo. Todo cambio destinado a `main` debe ingresar mediante un Pull Request aprobado.

## 3. Inicio de trabajo

Antes de iniciar una tarea, el developer debe:

1. Confirmar que existe una tarea identificable en Asana.
2. Partir de la versión actual de `main`.
3. Crear una rama exclusiva para esa unidad de trabajo.

Convención:

```text
tipo/ID-ASANA-descripcion-corta
```

Tipos:

```text
feature/
fix/
refactor/
hotfix/
```

Ejemplos:

```text
feature/ABC-123-nueva-funcionalidad
fix/ABC-456-correccion-calculo
refactor/ABC-789-mejora-servicio
hotfix/ABC-999-error-produccion
```

No se reutilizan ramas integradas. Evitar espacios, acentos, `ñ` y caracteres especiales.

## 4. Commits

Durante el desarrollo pueden existir tantos commits como sean necesarios.

Cada commit debe representar un avance entendible y utilizar un mensaje descriptivo.

Preferir:

```text
Corrige selección de pagos por fecha real
Agrega validación para comprobantes cancelados
Evita duplicidad en cálculo mensual
```

Evitar:

```text
cambios
update
fix
prueba
ahora si
```

Los commits de la rama son visibles durante la revisión del Pull Request.

Profact utiliza **Squash merge**, por lo que al integrar el Pull Request a `main` sus commits se consolidan en un único commit lógico. Los commits originales permanecen como contexto del Pull Request, pero no se incorporan individualmente al historial de `main`.

## 5. Publicación de la rama

La rama debe publicarse cuando exista trabajo que deba respaldarse, compartirse o revisarse.

Mientras el Pull Request permanezca abierto, cualquier corrección o ajuste solicitado debe realizarse sobre la misma rama y publicarse nuevamente.

## 6. Pull Request

Todo cambio destinado a `main` requiere Pull Request.

Formato de título:

```text
[ID-ASANA] Descripción breve
```

El Pull Request debe utilizar la plantilla oficial de Profact configurada.

El developer es responsable de:

- vincular la tarea de Asana;
- explicar el alcance del cambio;
- indicar cómo validar;
- declarar riesgos, dependencias o cambios de configuración;
- mantener el Pull Request actualizado;
- atender comentarios y cambios solicitados;
- resolver conflictos antes de integrar.

## 7. Draft Pull Request

Un Pull Request normal indica que el cambio está listo para revisión formal.

Un **Draft Pull Request** se utiliza cuando el trabajo todavía no está terminado pero se desea dar visibilidad temprana, solicitar retroalimentación o discutir una solución antes de concluirla.

Un Draft no se considera listo para aprobación ni integración. Cuando el developer termina el trabajo, debe cambiarlo a **Ready for review**.

## 8. Reviewer

El reviewer será una persona distinta del autor por política.

Debe revisar, según corresponda:

- comportamiento esperado;
- impacto funcional;
- legibilidad y mantenibilidad;
- consistencia con la arquitectura;
- posibles efectos secundarios;
- manejo de errores;
- seguridad;
- pruebas o validaciones realizadas;
- alcance declarado en Asana y en el Pull Request.

Puede comentar, sugerir cambios, solicitar modificaciones o aprobar.

## 9. Aprobación

Los Pull Requests requieren al menos una aprobación válida.

Además, el ruleset exige que el **último push revisable** haya sido aprobado por una persona distinta de quien realizó ese push.

- **Required approvals** asegura el número mínimo de aprobaciones.
- **Approval of the most recent reviewable push** evita que un PR aprobado reciba nuevos commits y sea integrado sin revisar esos últimos cambios.

Las aprobaciones anteriores pueden invalidarse cuando se agregan nuevos commits.

## 10. Conversaciones

Los comentarios sobre líneas o secciones del Pull Request generan conversaciones.

Una conversación debe marcarse como resuelta únicamente cuando el cambio solicitado fue atendido, la duda fue aclarada o reviewer y developer acordaron que no se requiere modificación.

Todas las conversaciones requeridas deben estar resueltas antes del merge.

## 11. Conflictos con `main`

Si GitHub detecta conflictos entre la rama de trabajo y `main`, el developer debe resolverlos antes del merge.

Los conflictos simples pueden resolverse en GitHub. Para cambios de código relevantes, se recomienda resolverlos localmente sobre la rama de trabajo, incorporar la versión actual de `main`, validar el resultado y publicar nuevamente la rama.

Nunca se resuelven conflictos modificando directamente `main`.

## 12. Integración

El método estándar es **Squash merge**.

Antes del merge deben cumplirse:

- Pull Request fuera de Draft;
- aprobación requerida;
- último push revisado;
- conversaciones resueltas;
- ausencia de conflictos;
- validaciones requeridas por el repositorio.

El mensaje final del squash debe conservar el identificador de Asana y describir el cambio integrado.

## 13. Después del merge

Después de integrar:

- la rama remota debe eliminarse (configurado por política);
- el developer debe actualizar su `main` local;
- la rama local debe eliminarse cuando ya no sea necesaria;
- la tarea de Asana debe avanzar al estado que corresponda.

Una rama integrada no se reutiliza.

## 14. Hotfix

Una urgencia no elimina el flujo de revisión.

Los hotfix parten de `main`, se desarrollan en una rama `hotfix/...` y deben ingresar mediante Pull Request.

El bypass queda reservado para situaciones excepcionales y actores autorizados.

## 15. Autenticación y acceso

El método estándar de acceso a repositorios Profact es **SSH**.

Cada developer debe completar el proceso de alta, identidad Git y configuración SSH descrito en [`ONBOARDING.md`](./ONBOARDING.md).

No se comparten llaves privadas, tokens ni credenciales.

## 16. Información sensible

No se almacenan en Git contraseñas, API keys, tokens, certificados privados, llaves privadas, connection strings productivas ni secretos de infraestructura.

## 17. Automatización

El flujo podrá complementarse con CI/CD.

**CI** valida automáticamente cambios mediante build, pruebas y análisis.

**CD** automatiza etapas posteriores a la integración, como empaquetado y despliegue.

## 18. Flujo resumido

```text
Asana
  ↓
Crear rama desde main actualizado
  ↓
Desarrollar y hacer commits
  ↓
Publicar rama
  ↓
Pull Request / Draft
  ↓
Ready for review
  ↓
Revisión
  ↓
Correcciones / conversaciones / conflictos
  ↓
Aprobación
  ↓
Squash merge
  ↓
Eliminar rama
  ↓
Continuar flujo en Asana
```
