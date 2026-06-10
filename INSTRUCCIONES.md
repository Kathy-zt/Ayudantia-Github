# Instrucciones de la Actividad

Ayudantía Git & GitHub — Simulación GitHub Flow

---

## Antes de empezar

Asegúrate de tener instalado:
- Git (`git --version`)
- Una cuenta en [github.com](https://github.com)

---

## Grupos y roles

Los grupos son de **1 a 4 integrantes**.

Cada grupo debe tener al menos un **Administrador del repositorio**, que es quien:

- Hace el fork del repositorio.
- Agrega a los demás integrantes como colaboradores.
- Revisa, comenta y acepta o rechaza los Issues y Pull Requests del grupo.
- Realiza el merge de los PRs aprobados y cierra los Issues resueltos.

El resto de los integrantes actúan como **colaboradores** y se encargan de las tareas asignadas.

---

## Paso 1 — Fork del repositorio

Solo el **Administrador del grupo** hace esto.

1. Ir a [github.com/mittods/Ayudantia-Github](https://github.com/mittods/Ayudantia-Github).
2. Hacer clic en **Fork** (arriba a la derecha).
3. Confirmar el fork a tu cuenta personal.

El fork es tu copia del repositorio. Desde ahí trabajará todo el grupo.

---

## Paso 2 — Configurar variables del repositorio (Administrador)

El repositorio incluye un workflow en `.github/workflows/ci.yml` que se ejecuta en cada push y pull request a `main`. Este workflow **fallará** hasta que el Administrador configure las variables requeridas.

Las variables se agregan en:  
**Settings → Secrets and variables → Actions → Variables → New repository variable**

| Variable | Descripción | Ejemplo |
|----------|-------------|---------|
| `APP_NAME` | Nombre del proyecto | `github-lab-grupo3` |
| `DEPLOY_ENV` | Entorno de despliegue | `staging` |
| `TEAM_NAME` | Nombre del grupo | `Grupo 3` |

Una vez configuradas, el workflow pasará a verde en el próximo push.

---

## Paso 3 — Agregar colaboradores

La persona que hizo el fork:

1. Ir a **Settings → Collaborators → Add people**.
2. Agregar el usuario de GitHub de cada integrante del grupo.
3. Los compañeros aceptan la invitación que les llega por email.

---

## Paso 4 — Clonar el repositorio

**Todos** los integrantes del grupo clonan el fork (no [github.com/mittods/Ayudantia-Github](https://github.com/mittods/Ayudantia-Github)):

```bash
git clone https://github.com/<usuario-quien-forkeo>/Ayudantia-Github
cd Ayudantia-Github
```

Verificar el remote:

```bash
git remote -v
```

---

## Paso 5 — Elegir una tarea y crear el Issue

Cada persona elige **una tarea distinta** de la lista y la registra abriendo un Issue en el fork del grupo:

1. Ir a la pestaña **Issues** del fork.
2. Clic en **New Issue**.
3. Escribir un título descriptivo (ej. `Corregir typo en calculo-promedio.txt`).
4. Asignarse el Issue a uno mismo en **Assignees**.
5. Hacer clic en **Submit new issue** — GitHub le asignará un número (`#1`, `#2`, etc.).

| Tarea | Archivo |
|-------|---------|
| Agregar los nombres del grupo | `practica/git-practica.txt` |
| Completar la ficha de markdown | `practica/markdown.md` |
| Corregir el typo | `practica/calculo-promedio.txt` |
| Agregar contactos al portfolio | `portfolio.html` |
| Agregar tu fila en la tabla de participantes del README (nombre, juego favorito, película/serie favorita, animal favorito) | `README.md` |
| Corregir el `.env` subido por error añadiéndolo al `.gitignore` | `.gitignore` |

---

## Paso 6 — Crear una rama para el Issue

**Cada persona** crea su propia rama desde `main`, asociada al Issue que abrió:

```bash
git checkout main
git pull origin main
git checkout -b issue-<número>-<descripción-breve>
```

Ejemplo (si tu Issue es el #3):

```bash
git checkout -b issue-3-corregir-typo
```

Verificar en qué rama estás:

```bash
git branch
```

---

## Paso 7 — Hacer el cambio

Editar el archivo que corresponde a tu Issue.

Ver qué cambiaste:

```bash
git status
git diff
```

---

## Paso 8 — Commit

```bash
git add <nombre-del-archivo>
git commit -m "Descripción breve de lo que hiciste"
```

Una buena práctica es usar **Conventional Commits**: prefijos que indican el tipo de cambio.

| Prefijo | Cuándo usarlo |
|---------|---------------|
| `feat:` | Se agrega algo nuevo |
| `fix:` | Se corrige un error |
| `docs:` | Cambios solo en documentación |
| `chore:` | Mantenimiento (configuración, archivos ignorados) |
| `refactor:` | Cambio de código sin agregar ni corregir nada |
| `style:` | Formato o espaciado sin cambio lógico |

Ejemplos de buenos mensajes de commit:

```
feat: agrega integrantes del Grupo 3 al listado
docs: completa ficha de markdown de Ana García
fix: corrige typo en broken-file.txt
feat: agrega Python y JavaScript al portfolio
chore: agrega .env al .gitignore
```

---

## Paso 9 — Push

```bash
git push origin issue-3-corregir-typo
```

---

## Paso 10 — Pull Request

1. Ir al fork del grupo en GitHub.
2. GitHub muestra el banner **"Compare & pull request"**. Hacer clic.
3. Verificar:
   - **base:** `main` (de [github.com/mittods/Ayudantia-Github](https://github.com/mittods/Ayudantia-Github))
   - **compare:** `issue-<número>-<descripción>` (tu rama)
4. Completar el template:
   - Describir qué cambiaste.
   - Escribir `Closes #<número>` para enlazar el Issue.
5. Crear el PR.

---

## Paso 11 — Review y merge (Administrador)

El **Administrador del grupo** es quien revisa y cierra el ciclo:

1. Ir al PR abierto en el fork.
2. Revisar la pestaña **Files Changed**.
3. Dejar al menos un comentario de revisión.
4. Si todo está bien, **aprobar** el PR y hacer **Merge**.
5. Una vez mergeado, **cerrar el Issue** correspondiente (o verificar que `Closes #N` lo haya cerrado automáticamente).

---

## Paso 12 — Actividad final: resolución de conflicto local

Esta actividad la hace **cada integrante por separado**, en su propia rama. **No se pushea nada.**

### Parte A — Modificar el archivo

Editar `practica/conflicto.txt` cambiando **solo las partes indicadas dentro de cada línea** (no la línea completa):

| Línea | Cambiar esto | Por esto |
|-------|-------------|----------|
| `nombre    = AppLab-v1.0` | `v1.0` | `v2.0` |
| `estado    = borrador, sin_revision` | `borrador` | `revisado` |
| `entorno   = desarrollo` | `desarrollo` | `produccion` |
| `integrantes = sin_registrar` | `sin_registrar` | tu nombre |
| `modulos     = ninguno` | `ninguno` | módulos a elección (ej: `auth, api`) |
| `ultima_revision = 2024-01-01` | la fecha | la fecha de hoy |

Commitear el cambio localmente:

```bash
git add practica/conflicto.txt
git commit -m "feat: actualiza configuración local del equipo"
```

### Parte B — Mergear con la rama de conflicto

```bash
git merge merge-challenge
```

Git **no podrá resolver el merge solo** porque la rama `merge-challenge` también modificó las mismas partes del archivo. Verás algo así:

```
<<<<<<< HEAD
nombre    = AppLab-v2.0
=======
nombre    = AppLab-v1.5-beta
>>>>>>> merge-challenge
```

### Parte C — Resolver el conflicto

1. Abrir `practica/conflicto.txt` en el editor.
2. Buscar todos los bloques `<<<<<<< / ======= / >>>>>>>`.
3. Para cada uno: decidir con qué versión quedarse (o combinar ambas) y eliminar los marcadores.
4. Guardar el archivo.

Confirmar que no quedan marcadores:

```bash
grep -c "<<<<<<" practica/conflicto.txt
```

Debe devolver `0`. Luego finalizar el merge:

```bash
git add practica/conflicto.txt
git commit -m "fix: resuelve conflicto de merge con merge-challenge"
```

> **No hacer push.** Esta actividad queda solo en tu rama local.

---


## Comandos de emergencia (si algo sale mal)

| Situación | Comando |
|-----------|---------|
| Ver qué cambié | `git status` |
| Ver los cambios en detalle | `git diff` |
| Descartar cambios sin commitear | `git restore <archivo>` |
| Ver el historial | `git log --oneline` |
| Volver a ver un commit anterior | `git checkout <HASH>` |
| Volver a tu rama | `git checkout issue-<número>-<descripción>` |
| Deshacer un commit ya pusheado | `git revert <HASH>` |

---

## Flujo completo resumido

```
Fork → Clone → Branch → Cambio → Commit → Push → Pull Request → Review
```
