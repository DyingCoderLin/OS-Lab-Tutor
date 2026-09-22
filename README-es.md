# TuTor

[English](README.md) · **Español**

**Skill** para agentes de código que convierte tu asistente en un tutor. Una *skill* es una carpeta de instrucciones que tu herramienta de IA lee cuando le sirven. Planifica en pasos cortos, explica cada comando, revisa tu avance con comandos de solo lectura y no termina la tarea por ti.

Úsalo cuando quieras **aprender haciendo**—tareas, tutoriales, guías paso a paso o cuando digas «no lo hagas por mí».

## Objetivo

TuTor ayuda a **docentes y estudiantes** a usar la IA como tutor, no como atajo. Los asistentes de código suelen entregar todo resuelto y saltarse el razonamiento, la depuración y el ensayo y error, que es donde de verdad se aprende. Esta skill redirige ese poder hacia el **aprender haciendo**: tú escribes el código y ejecutas los comandos; el agente planifica, explica y verifica—sin hacer el trabajo por ti. La idea es entender más en clase, en equipo y en proyectos propios, no copiar y pegar más rápido.

## Qué hace

| Comportamiento | Detalle |
|----------------|---------|
| **Paso a paso** | Muestra un plan numerado al inicio y da **una** acción por turno (sin la solución completa). |
| **Verificación** | Cuando dices que terminaste, la herramienta revisa con comandos de solo lectura (`Read`, `ls`, `cat`, `git status`, `git diff`, las pruebas que corriste). |
| **Control de herramientas** | Puede ver tu trabajo, pero **no** debe crear, editar ni ejecutar comandos que armen tu entregable por ti. |
| **Comandos explicados** | Cada comando de terminal incluye desglose: para qué sirve, qué hace cada parte y cómo saber si salió bien. |

Más detalle en [`references/`](references/):

- [`references/example-flow.md`](references/example-flow.md) — ejemplo de app desde cero
- [`references/tool-gate.md`](references/tool-gate.md) — qué comandos de terminal están permitidos

## Instalación

**Repositorio:** [github.com/kevinnio/tutor](https://github.com/kevinnio/tutor)

TuTor es una carpeta con `SKILL.md` (las instrucciones) y `references/` (lecturas extra). Deja la carpeta con el nombre `tutor`. Algunas herramientas no cargan una skill si el nombre de la carpeta no coincide con el nombre dentro de `SKILL.md`.

### Con Skills CLI (recomendado)

La [Skills CLI](https://github.com/vercel-labs/skills) ([skills.sh](https://skills.sh)) es un instalador pequeño: busca las herramientas de IA que tienes y copia la skill en la carpeta correcta de cada una, así no necesitas saber las rutas.

**Global (todos tus proyectos)** — lo más práctico la primera vez:

```bash
npx skills add kevinnio/tutor -g -y
```

**Solo este repositorio** (para compartir con tu clase o equipo vía git):

```bash
npx skills add kevinnio/tutor -y
```

**Elegir herramientas** (sin el menú):

```bash
npx skills add kevinnio/tutor -g -a opencode -a github-copilot -a gemini-cli -y
```

| Opción | Qué hace |
|--------|----------|
| `-g`, `--global` | Instalación global en tu usuario (`~/…/skills/`) |
| (sin `-g`) | Solo en el proyecto donde estás |
| `-a`, `--agent` | Para qué herramientas instalar: `opencode`, `github-copilot`, `gemini-cli`, `cursor`, `claude-code`, `codex`, etc. |
| `-y`, `--yes` | Sin pedir confirmación |

Antes de instalar: `npx skills add kevinnio/tutor --list`. Todas las herramientas compatibles: [vercel-labs/skills](https://github.com/vercel-labs/skills#supported-agents).

Al terminar, abre un **chat nuevo** (o vuelve a abrir la herramienta) para que vea la skill.

### Con qué herramienta empezar

Cualquiera de la lista sirve. Si es tu primera vez, **OpenCode** es libre y de código abierto, y puedes conectarlo a un modelo gratuito, incluso uno que corra en tu propia computadora. **GitHub Copilot** y **Gemini CLI** son gratis para estudiantes verificados ([Student Developer Pack](https://education.github.com/pack), [Google AI para estudiantes](https://gemini.google/students/)). Cursor y Claude Code requieren un plan de pago, salvo que tu escuela te lo dé.

### Cómo usar TuTor en cada herramienta

- **OpenCode** — Cuéntale qué quieres aprender; OpenCode carga la skill cuando le sirve. [OpenCode skills](https://opencode.ai/docs/skills/).
- **GitHub Copilot** — En VS Code, escribe `/tutor` en el chat o cuéntale qué quieres aprender. [Copilot skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills).
- **Gemini CLI** — Cuéntale qué quieres aprender; Gemini CLI carga la skill cuando le sirve. [Gemini CLI skills](https://geminicli.com/docs/cli/skills/).
- **Cursor** — Pide aprender algo (p. ej. «Enséñame a hacer una app de tareas, pero no la escribas tú») o usa `/tutor` si lo tienes. [Cursor skills](https://cursor.com/docs/context/skills).
- **Claude Code** — Ejecuta `/tutor` o cuéntale qué quieres aprender. [Claude Code skills](https://code.claude.com/docs/en/skills).

### Opcional: TuTor como modo al que puedes cambiar

Normalmente la skill se carga sola cuando le sirve. Si prefieres elegir TuTor desde un menú, como eliges Plan o Build en OpenCode, añade un archivo extra. También impide que la herramienta edite tus archivos: TuTor solo puede leer.

| Herramienta | Archivo | Dónde ponerlo | Cómo cambiar |
|-------------|---------|---------------|--------------|
| [OpenCode](https://opencode.ai) | `agents/opencode/tutor.md` | `~/.config/opencode/agents/` | pulsa `Tab` y elige **tutor** |
| [Claude Code](https://code.claude.com) | `agents/claude/tutor.md` | `~/.claude/agents/` | `claude --agent tutor`, o `@tutor` en un chat |
| [GitHub Copilot](https://code.visualstudio.com/docs/agent-customization/custom-agents) (VS Code) | `agents/claude/tutor.md` | `~/.claude/agents/` | elige **tutor** en el menú de agentes |

```bash
SKILL_DIR=~/.claude/skills/tutor   # donde esté instalada la skill tutor

mkdir -p ~/.config/opencode/agents ~/.claude/agents
ln -sf "$SKILL_DIR/agents/opencode/tutor.md" ~/.config/opencode/agents/tutor.md
ln -sf "$SKILL_DIR/agents/claude/tutor.md"   ~/.claude/agents/tutor.md
```

En macOS y Linux son atajos (enlaces simbólicos), así que actualizar TuTor (`npx skills update`) también actualiza el modo. En Windows, Git Bash puede copiar el archivo en lugar de enlazarlo, así que repite los comandos tras actualizar.

VS Code Copilot también lee la carpeta de Claude, así que un archivo sirve para Copilot y Claude Code.

Instala la skill primero. Los dos archivos le dicen a la herramienta que la siga. Una skill solo puede pedirle que no edite tus archivos; estos archivos hacen que la herramienta se niegue.

Cada herramienta espera su propio formato, por eso hay un archivo por herramienta. Cursor eliminó sus modos personalizados en 2.1, así que allí usas solo la skill.

### Instalación manual (git clone)

Si prefieres no usar el instalador, clona este proyecto en la carpeta que lee tu herramienta. La carpeta depende de la herramienta:

| Herramienta | Para todos tus proyectos | Solo este proyecto |
|-------------|-------------------------|--------------------|
| [Cursor](https://cursor.com) | `~/.cursor/skills/tutor` | `.cursor/skills/tutor` o `.agents/skills/tutor` |
| [Claude Code](https://code.claude.com) | `~/.claude/skills/tutor` | `.claude/skills/tutor` |
| [OpenCode](https://opencode.ai) | `~/.config/opencode/skills/tutor` | `.opencode/skills/tutor` |
| [GitHub Copilot](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills) | `~/.copilot/skills/tutor` | `.github/skills/tutor` |
| [Gemini CLI](https://geminicli.com/docs/cli/skills/) | `~/.gemini/skills/tutor` | `.gemini/skills/tutor` |

```bash
REPO=https://github.com/kevinnio/tutor.git
TARGET=~/.cursor/skills/tutor   # ejemplo global

mkdir -p "$(dirname "$TARGET")"
git clone "$REPO" "$TARGET"
```

No instales dentro de `~/.cursor/skills-cursor/`. Cursor guarda ahí sus propias skills. Si `TARGET` ya existe, bórralo o ve a [Actualizar](#actualizar).

### Enlace simbólico (desarrollo local)

```bash
SKILL_ROOT="$HOME/code/tutor"
TARGET="$HOME/.cursor/skills/tutor"

mkdir -p "$TARGET"
ln -sf "$SKILL_ROOT/SKILL.md" "$TARGET/SKILL.md"
ln -sf "$SKILL_ROOT/references" "$TARGET/references"
```

### Instalar TuTor con TuTor

Como ejercicio, deja que TuTor te guíe para instalarlo: tú ejecutas cada comando y la herramienta te orienta y revisa. Así ves cómo quedan las skills en disco y, cuando termine, ya puedes usarlo en tareas reales.

Pega esto en una herramienta de IA que pueda abrir enlaces (mejor en un chat nuevo):

**Nota de confianza:** este prompt le pide a tu herramienta de IA obtener instrucciones de internet (`raw.githubusercontent.com`), fijadas a la etiqueta de versión `v0.6` (inmutable). Solo hazlo si confías en la fuente: una skill que instalas puede influir en lo que tu herramienta de IA haga en futuras sesiones. Si prefieres no descargar instrucciones remotas, sigue los pasos de instalación manual de arriba.

```text
TuTor, instálate conmigo: yo ejecuto cada comando y tú actúas como tutor.

Lee y aplica durante toda la sesión:
- SKILL.md: https://raw.githubusercontent.com/kevinnio/tutor/v0.6/SKILL.md
- README, sección Instalación: https://raw.githubusercontent.com/kevinnio/tutor/v0.6/README.md

Reglas de TuTor: un paso a la vez, desglosa los comandos, verifica cuando diga "listo".
No instales por mí (no escribas archivos, no hagas git clone ni npx)—si pido "hazlo tú", rechaza.

Primero pregúntame qué herramienta de IA uso (OpenCode, GitHub Copilot, Gemini CLI, Cursor, Claude Code, etc.)
y si quiero instalación global o solo en este proyecto. Usa la ruta de skills correcta.

Objetivo: tener la skill `tutor` en mi máquina.
Enséñame `npx skills add kevinnio/tutor -g -y` salvo que prefiera git clone manual.

Cuando responda, dame un plan corto numerado y el Paso 1; ahí te detienes.
```

## Actualizar

### Con Skills CLI (recomendado)

```bash
npx skills update tutor -g -y    # global
npx skills update tutor -y         # solo este proyecto
```

Para ver dónde está instalada: `npx skills list | grep tutor`

### Con git (instalación manual)

```bash
cd ~/.cursor/skills/tutor   # tu ruta
git pull origin master
```

Si es **submódulo**: `git submodule update --remote ruta/al/tutor`

### Fijar a una etiqueta de versión (instalación reproducible)

Las etiquetas de versión son inmutables. Instala una versión auditada exacta en vez de `master`:

```bash
# clon nuevo
git clone --branch v0.6 https://github.com/kevinnio/tutor.git "$TARGET"
# o dentro de un clone ya existente
git fetch --tags && git checkout v0.6
```

Verifica la versión fijada: `git describe --tags`

### Revisar la versión instalada

```bash
grep '^  version:' ~/.cursor/skills/tutor/SKILL.md
# la ruta puede variar; usa npx skills list
```

Compárala con `metadata.version` en [SKILL.md](SKILL.md) en GitHub.

### Después de actualizar

1. **Vuelve a abrir tu herramienta de IA** (o abre un chat nuevo) para que recargue la skill.
2. **Confirma la versión** con el `grep` de arriba.
3. Si no notas cambios, ejecuta `npx skills list` y actualiza en cada sitio (global y proyecto) donde aparezca `tutor`.

## Cómo usarlo

1. **Instala** la skill (arriba) y abre tu proyecto en la herramienta.
2. **Di qué quieres aprender** y que te acompañe, no que lo haga por ti.

Ejemplos de mensajes:

```text
I want to learn how to add tests to this repo. Walk me through it step by step; don't edit files for me.

Enséñame a crear un API REST con Express. No hagas el código por mí.

Help me fix this failing test, but only give hints and commands—I run everything myself.
```

3. **Sigue cada paso** que te indique y avisa cuando termines (p. ej. «listo», «done»).
4. El tutor **revisa** antes de seguir. Si algo falla, te dice qué falta; no pasa al siguiente paso.
5. Si la herramienta intenta hacerlo por ti, recuérdale: *«Sigue la skill tutor: solo verifica, yo ejecuto los comandos.»*

## Estructura del repositorio

```text
tutor/
├── SKILL.md              # La skill (obligatorio)
├── references/           # Lecturas extra que la herramienta carga cuando le sirven
│   ├── example-flow.md
│   └── tool-gate.md
├── agents/               # Modos opcionales (solo lectura)
│   ├── opencode/tutor.md
│   └── claude/tutor.md
├── README.md
├── README-es.md
├── AGENTS.md             # Guía para agentes que editan este repo
├── AUTHORS.md            # Contribuidores
└── LICENSE               # MIT
```

La versión va en `SKILL.md`, en la línea `metadata.version` cerca del inicio (hoy **0.6**). Cada release se etiqueta como `v<versión>` (p. ej. `v0.6`); fija la instalación a una etiqueta para que sea reproducible.

## Contribuir

Nos encanta recibir ideas, reportes y código.

- **Errores y nuevas funciones** — [abre un issue](https://github.com/kevinnio/tutor/issues/new). Cuéntanos qué esperabas, qué pasó y qué agente usas.
- **Código y documentación** — manda un [pull request](https://github.com/kevinnio/tutor/compare). Por ejemplo: mejores formas de enseñar, casos raros del control de herramientas, traducciones del README o notas de instalación para otros agentes.

### Cómo enviar un pull request

1. Haz **fork** del repo y crea una rama (`git checkout -b fix/tool-gate-example`).
2. Edita `SKILL.md` y/o `references/`. Mantén la skill concisa; los ejemplos largos van en `references/`.
3. **Pruébalo** instalando tu rama en un agente (Cursor, Claude Code u OpenCode) con una tarea corta de aprendizaje.
4. Abre el **pull request** indicando:
   - Qué cambió y por qué
   - En qué agente(s) lo probaste
   - Si rompe rutas de instalación o el nombre `tutor` (en OpenCode debe coincidir con la carpeta)

No subas secretos, rutas personales ni `node_modules` ni archivos del playground.

## Contribuidores

<a href="https://github.com/kevinnio/tutor/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=kevinnio/tutor&columns=3" alt="Contribuidores" />
</a>

Las fotos salen de los [contribuidores en GitHub](https://github.com/kevinnio/tutor/graphs/contributors), generadas con [contrib.rocks](https://contrib.rocks) (contributors-img). Nombres y perfiles: [AUTHORS.md](AUTHORS.md).

## Donaciones

Si TuTor te sirve para aprender, puedes invitarme un café por PayPal:

**[paypal.me/kevindperezm](https://paypal.me/kevindperezm?locale.x=es_XC&country.x=MX)**

Donar es opcional; no hace falta para usar el proyecto ni para contribuir.

## Licencia

[MIT](LICENSE) — Copyright (c) 2026 Kevin Perez
