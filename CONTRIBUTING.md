# Estándar de trabajo con GitHub en Profact

## 1. Propósito

Este documento define el flujo esperado para los repositorios de Profact.

Asana es la fuente principal para planeación, prioridad, responsables y seguimiento funcional. GitHub es la fuente principal para código, ramas, Pull Requests, revisión e historial técnico.

## 2. Rama principal

La rama principal de los repositorios es `main`.

`main` está protegida y no se utiliza como rama de desarrollo.

Todo cambio destinado a `main` debe ingresar mediante un Pull Request aprobado.

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

No se reutilizan ramas que ya hayan sido integradas.

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

Profact utiliza **Squash merge**, por lo que al integrar el Pull Request a `main` sus commits se consolidan en un único commit lógico. Los commits originales siguen formando parte del contexto e historial del Pull Request, pero no se incorporan individualmente al historial de `main`.

## 5. Publicación de la rama

La rama debe publicarse en el repositorio remoto cuando exista trabajo que deba respaldarse, compartirse o revisarse.

Una vez publicada, el developer continuará realizando sus pushes sobre la misma rama mientras el Pull Request permanezca abierto.

## 6. Pull Request

Todo cambio destinado a `main` requiere Pull Request.

Formato de título:

```text
[ID-ASANA] Descripción breve
```

El Pull Request debe utilizar la plantilla oficial de Profact.

El developer es responsable de:

- vincular la tarea de Asana;
- explicar el alcance del cambio;
- indicar cómo validar;
- declarar riesgos, dependencias o cambios de configuración;
- mantener el Pull Request actualizado;
- atender comentarios y cambios solicitados;
- resolver conflictos antes de integrar.

## 7. Draft Pull Request

Un Pull Request normal significa que el cambio está listo para revisión.

Un **Draft Pull Request** se utiliza cuando el trabajo todavía no está terminado pero se desea:

- dar visibilidad temprana;
- solicitar retroalimentación;
- mostrar avance;
- discutir una solución antes de concluirla.

Un Draft no se considera listo para aprobación ni integración.

Cuando el developer termina el trabajo, debe cambiarlo a **Ready for review**.

## 8. Reviewer

El reviewer debe ser una persona distinta del autor del cambio.

Su responsabilidad es revisar, según corresponda:

- comportamiento esperado;
- impacto funcional;
- legibilidad y mantenibilidad;
- consistencia con la arquitectura;
- posibles efectos secundarios;
- manejo de errores;
- seguridad;
- pruebas o validaciones realizadas;
- alcance declarado en Asana y en el Pull Request.

El reviewer puede:

- comentar;
- sugerir cambios;
- solicitar modificaciones;
- aprobar.

## 9. Aprobación

Los Pull Requests requieren al menos una aprobación válida.

Además, el ruleset exige que el **último push revisable** haya sido aprobado por una persona distinta de quien realizó ese push.

Estas reglas cubren situaciones diferentes:

- **Required approvals** asegura que exista el número mínimo de aprobaciones.
- **Approval of the most recent reviewable push** evita que un cambio aprobado reciba nuevos commits y sea integrado sin que alguien distinto revise esos últimos cambios.

Las aprobaciones anteriores pueden invalidarse cuando se agregan nuevos commits.

## 10. Conversaciones

Los comentarios sobre líneas o secciones del Pull Request generan conversaciones.

Una conversación debe marcarse como resuelta únicamente cuando:

- el cambio solicitado fue atendido;
- la duda fue aclarada; o
- reviewer y developer acordaron que no se requiere modificación.

Todas las conversaciones requeridas deben estar resueltas antes del merge.

## 11. Conflictos con `main`

Si GitHub detecta conflictos entre la rama de trabajo y `main`, el developer es responsable de resolverlos antes del merge.

Los conflictos simples pueden resolverse en GitHub.

Para cambios de código relevantes, se recomienda resolverlos localmente sobre la rama de trabajo, incorporar la versión actual de `main`, validar el resultado y publicar nuevamente la rama.

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

- la rama remota debe eliminarse;
- el developer debe actualizar su `main` local;
- la rama local debe eliminarse cuando ya no sea necesaria;
- la tarea de Asana debe avanzar al estado que corresponda al proceso de QA, despliegue o cierre.

Una rama integrada no se reutiliza para una nueva tarea.

## 14. Hotfix

Una urgencia no elimina el flujo de revisión.

Los hotfix parten de `main`, se desarrollan en una rama `hotfix/...` y deben ingresar mediante Pull Request.

El bypass de protecciones queda reservado para situaciones excepcionales y para los actores expresamente autorizados.

## 15. Autenticación

El método estándar de acceso a los repositorios de Profact es **SSH**.

Cada developer debe:

- utilizar su propia cuenta de GitHub;
- utilizar su propia llave SSH;
- proteger su llave privada;
- registrar únicamente la llave pública en GitHub;
- evitar compartir llaves, tokens o credenciales.

Los repositorios deben clonarse utilizando la URL SSH.

La configuración técnica de SSH se documenta en `SSH_SETUP.md`.

## 16. Información sensible

No se almacenan en Git:

- contraseñas;
- API keys;
- tokens;
- certificados privados;
- llaves privadas;
- connection strings productivas;
- secretos de infraestructura.

Los secretos deben permanecer en los mecanismos de configuración segura definidos para cada solución.

## 17. Automatización

El flujo podrá complementarse con CI/CD.

**CI (Continuous Integration)** valida automáticamente cambios, por ejemplo mediante build, pruebas y análisis.

**CD (Continuous Delivery/Deployment)** automatiza etapas posteriores a la integración, como empaquetado y despliegue a ambientes.

Estas automatizaciones no reemplazan el flujo de ramas, Pull Requests y revisión definido en este documento.

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
