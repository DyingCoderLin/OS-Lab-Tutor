# OS Lab Tutor

[English](README.md) · **Español**

**Skill** para agentes de código que convierte tu asistente en un tutor. Una *skill* es una carpeta de instrucciones que tu herramienta de IA lee cuando le sirven. Da un plan breve, indica la tarea actual de la guía y espera. Explica conceptos o depuración cuando lo pides, sin completar el trabajo por ti.

Úsalo cuando quieras **aprender haciendo**—tareas, tutoriales, guías paso a paso o cuando digas «no lo hagas por mí».

## Objetivo

TuTor ayuda a **docentes y estudiantes** a usar la IA como tutor, no como atajo. Los asistentes de código suelen entregar todo resuelto y saltarse el razonamiento, la depuración y el ensayo y error, que es donde de verdad se aprende. Esta skill redirige ese poder hacia el **aprender haciendo**: tú escribes el código y ejecutas los comandos; el agente explica conceptos y herramientas; indica dónde registrar resultados y, en Lab1, propone una prueba o seguir avanzando; tú ejecutas pruebas, depuras y corriges—sin hacer el trabajo por ti. La idea es entender más en clase, en equipo y en proyectos propios, no copiar y pegar más rápido.

## Qué hace

| Comportamiento | Detalle |
|----------------|---------|
| **Ritmo original** | Primero presenta el laboratorio y la colaboración; después, plan breve y requisitos completos de la tarea actual con destino en informe/código; luego espera. La pregunta 1 va antes del TODO 1. Explicaciones a petición, sin cuestionarios ni lecciones previas añadidas. |
| **Tu documento de informe** | Crea tú un documento dedicado y comunica su ruta al tutor. Elige cualquier formato legible y organización; no se exige plantilla, títulos ni estructura. El tutor lo lee, pero no lo escribe por ti. |
| **Etapas y destinos de Lab1** | El tutor identifica la guía actual e indica un destino por tarea: un tema en tu informe o un TODO concreto. La explicación escrita requerida es otra tarea para el informe. Los números de preguntas identifican temas, no títulos obligatorios. |
| **Al terminar un TODO de Lab1** | Sin veredicto inmediato: ejecutas una prueba específica existente y aplicable; si no existe, continúas. La evaluación global se reserva para integración. Otros laboratorios conservan su propia política. |
| **Pistas sin respuestas** | Sin soluciones de TODO, líneas defectuosas, causas, valores correctos ni recetas de corrección, tampoco en prosa. |
| **Sin respuestas completas** | Se rechaza completar una pregunta, dar texto de referencia del informe o explicar toda la solución. Puedes preguntar por una instrucción o concepto concreto. |
| **Comentarios del informe** | Basta entender la idea central: una respuesta adecuada se acepta y se continúa, sin pulir palabras ni añadir mejoras opcionales. Solo errores fundamentales o requisitos centrales ausentes reciben comentarios breves; el tutor no escribe la respuesta. |
| **Guía de GDB** | Cuando pides ayuda de depuración, recibes etapas/funciones pertinentes, puntos de parada, registros/memoria y comandos explicados. Tú ejecutas, localizas y corriges; el tutor no revela el defecto ni la corrección del código. |
| **Control de herramientas** | La lectura apoya tu pregunta; el tutor revisa el trabajo entregado, pero no edita archivos ni ejecuta compilaciones, programas, pruebas o depuradores. |
| **Comandos explicados** | Cada comando sugerido explica su objetivo, argumentos y el tipo de datos que aporta; sin resultados esperados que revelen la solución. |

Más detalle en [`references/`](references/):

- [`references/example-flow.md`](references/example-flow.md) — revisión y depuración de un laboratorio de SO sin revelar correcciones
- [`references/tool-gate.md`](references/tool-gate.md) — qué comandos de terminal están permitidos
- [`references/gdb-coaching.md`](references/gdb-coaching.md) — investigación con GDB dirigida por el estudiante
- [`references/lab1-guide.md`](references/lab1-guide.md) — etapas, informe, TODO y pruebas verificadas en el código de ChCore Lab1

## Entregas de Lab1

Entrega tres partes: la conversación auténtica con la IA, tu documento de informe
y los archivos de Lab1 modificados con tus TODO. Conserva/exporta la conversación
real mediante tu herramienta. Cada tarea escribe en el informe o en un TODO;
las pruebas y la depuración ayudan a esas tareas y no añaden otra entrega
obligatoria. Solo los errores fundamentales del informe reciben comentarios breves; las respuestas adecuadas se aceptan sin pulirlas; los TODO
mantienen la política de prueba específica o continuación sin revelar defectos.

## Instrucciones del proyecto sin mencionar la skill

En Codex, la skill global es manual: selecciónala o escribe `$tutor`; pedir ayuda
con Lab1 por sí solo no garantiza que se cargue.

Para aplicar siempre estas reglas en un proyecto estudiantil, copia
[templates/AGENTS.lab1.md](templates/AGENTS.lab1.md) como `AGENTS.md` dentro de
ese Lab1, o combina su contenido con las instrucciones existentes. No sobrescribas
un archivo existente ni uses el `AGENTS.md` de mantenimiento de este repositorio.
La plantilla es autónoma y conserva los límites de informe/código sin invocar
la skill. Abre Codex en ese directorio; tras instalar/cambiar las instrucciones,
reinicia la sesión o pide releerlas explícitamente en el chat existente. Esta
opción afecta al proyecto y no activa la skill global automáticamente.

## Instalación

Este fork se basa en [TuTor](https://github.com/kevinnio/tutor). Sus reglas **0.7.4-dev** aún no están publicadas; la instalación remota solo las incluye después de publicarlas. En Codex, selecciona la skill explícitamente o usa `$tutor`; la activación automática está deshabilitada. Otras herramientas pueden seleccionarla de otra manera.

**Repositorio:** [github.com/DyingCoderLin/OS-Lab-Tutor](https://github.com/DyingCoderLin/OS-Lab-Tutor)

TuTor es una carpeta con `SKILL.md` (las instrucciones) y `references/` (lecturas extra). Deja la carpeta con el nombre `tutor`. Algunas herramientas no cargan una skill si el nombre de la carpeta no coincide con el nombre dentro de `SKILL.md`.

### Con Skills CLI (recomendado)

La [Skills CLI](https://github.com/vercel-labs/skills) ([skills.sh](https://skills.sh)) es un instalador pequeño: busca las herramientas de IA que tienes y copia la skill en la carpeta correcta de cada una, así no necesitas saber las rutas.

**Global (todos tus proyectos)** — lo más práctico la primera vez:

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -g -y
```

**Solo este repositorio** (para compartir con tu clase o equipo vía git):

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -y
```

**Elegir herramientas** (sin el menú):

```bash
npx skills add DyingCoderLin/OS-Lab-Tutor -g -a opencode -a github-copilot -a gemini-cli -y
```

| Opción | Qué hace |
|--------|----------|
| `-g`, `--global` | Instalación global en tu usuario (`~/…/skills/`) |
| (sin `-g`) | Solo en el proyecto donde estás |
| `-a`, `--agent` | Para qué herramientas instalar: `opencode`, `github-copilot`, `gemini-cli`, `cursor`, `claude-code`, `codex`, etc. |
| `-y`, `--yes` | Sin pedir confirmación |

Antes de instalar: `npx skills add DyingCoderLin/OS-Lab-Tutor --list`. Todas las herramientas compatibles: [vercel-labs/skills](https://github.com/vercel-labs/skills#supported-agents).

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
REPO=https://github.com/DyingCoderLin/OS-Lab-Tutor.git
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
ln -sf "$SKILL_ROOT/agents" "$TARGET/agents"
```

### Instalar TuTor con TuTor

Como ejercicio, deja que TuTor te guíe para instalarlo: tú ejecutas cada comando y la herramienta explica conceptos y te ayuda a decidir cómo comprobar tu trabajo. Así ves cómo quedan las skills en disco y, cuando termine, ya puedes usarlo en tareas reales.

Pega esto en una herramienta de IA que pueda abrir enlaces (mejor en un chat nuevo):

**Nota de confianza:** este prompt le pide a tu herramienta de IA obtener instrucciones de internet (`raw.githubusercontent.com`), de la rama de desarrollo `master` (que puede cambiar). Solo hazlo si confías en la fuente: una skill que instalas puede influir en lo que tu herramienta de IA haga en futuras sesiones. Si prefieres no descargar instrucciones remotas, sigue los pasos de instalación manual de arriba.

```text
TuTor, instálate conmigo: yo ejecuto cada comando y tú actúas como tutor.

Lee y aplica durante toda la sesión:
- SKILL.md: https://raw.githubusercontent.com/DyingCoderLin/OS-Lab-Tutor/master/SKILL.md
- README, sección Instalación: https://raw.githubusercontent.com/DyingCoderLin/OS-Lab-Tutor/master/README.md

Reglas de TuTor: plan breve, tarea actual de la guía y esperar; explica cuando lo pida, sin cuestionarios añadidos. Desglosa los comandos y aplica la política del laboratorio. En Lab1, pídeme crear/designar un documento de informe y comunicar su ruta, acepta mi organización libre, indica el destino en informe/código y, tras "listo", propone una prueba específica existente o seguir avanzando, sin veredicto inmediato. Nunca reveles correcciones.
No instales por mí (no escribas archivos, no hagas git clone ni npx)—si pido "hazlo tú", rechaza.

Primero pregúntame qué herramienta de IA uso (OpenCode, GitHub Copilot, Gemini CLI, Cursor, Claude Code, etc.)
y si quiero instalación global o solo en este proyecto. Usa la ruta de skills correcta.

Objetivo: tener la skill `tutor` en mi máquina.
Enséñame `npx skills add DyingCoderLin/OS-Lab-Tutor -g -y` salvo que prefiera git clone manual.

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

Las reglas `0.7.4-dev` de este fork aún no tienen etiqueta de versión. La versión anterior `v0.6` no incluye estos cambios. Después de publicar una versión, usa su etiqueta real en `git clone --branch <release-tag>` y consulta la revisión con `git describe --tags --always`. No supongas que una versión de desarrollo tiene una etiqueta publicada.

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

Help me investigate this failing test with GDB. Suggest useful stages, breakpoints, and registers with explained commands; do not reveal the faulty code or fix.
```

3. **Intenta tú la tarea actual de la guía.** Pide ayuda cuando la necesites y avisa al terminar. El tutor no añade preguntas previas para permitirte comenzar un TODO.
4. **En Lab1, designa tu informe:** crea tú un documento dedicado (o usa uno que ya creaste) y comunica su ruta al tutor. Escribe como quieras, siempre que el tutor lo entienda. Las respuestas teóricas van allí; las tareas de código van en su TODO; la explicación requerida es otra tarea para el informe. El tutor acepta el razonamiento central correcto sin pulir el texto y solo señala errores fundamentales, pero no escribe una respuesta completa, rellena razonamientos ausentes ni identifica un defecto o corrección del código. Tras cada TODO, ejecuta una prueba específica real si está disponible; si no, continúa sin veredicto del tutor. La versión original de cinco TODO solo tiene `make grade` global. Otros laboratorios pueden conservar revisión del código.
5. Si adelanta un veredicto o corrección en Lab1, recuérdale: *«Indica dónde registrar el resultado de esta etapa. Dame una prueba específica existente o déjame continuar si no existe. Yo investigaré los fallos observados con GDB.»*

## Estructura del repositorio

```text
tutor/
├── SKILL.md              # La skill (obligatorio)
├── references/           # Lecturas extra que la herramienta carga cuando le sirven
│   ├── example-flow.md
│   ├── gdb-coaching.md
│   ├── lab1-guide.md
│   └── tool-gate.md
├── agents/               # Modos opcionales y activación de Codex
│   ├── openai.yaml
│   ├── opencode/tutor.md
│   └── claude/tutor.md
├── templates/
│   └── AGENTS.lab1.md
├── README.md
├── README-es.md
├── AGENTS.md             # Guía para agentes que editan este repo
├── AUTHORS.md            # Contribuidores
└── LICENSE               # MIT
```

La versión va en `SKILL.md`, en la línea `metadata.version` cerca del inicio (hoy **0.7.4-dev**). Es una versión de desarrollo sin publicar; las etiquetas se crean por separado cuando se solicita publicar.

## Contribuir

Nos encanta recibir ideas, reportes y código.

- **Errores y nuevas funciones** — [abre un issue](https://github.com/DyingCoderLin/OS-Lab-Tutor/issues/new). Cuéntanos qué esperabas, qué pasó y qué agente usas.
- **Código y documentación** — manda un [pull request](https://github.com/DyingCoderLin/OS-Lab-Tutor/compare). Por ejemplo: mejores formas de enseñar, casos raros del control de herramientas, traducciones del README o notas de instalación para otros agentes.

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

<a href="https://github.com/DyingCoderLin/OS-Lab-Tutor/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=DyingCoderLin/OS-Lab-Tutor&columns=3" alt="Contribuidores" />
</a>

Las fotos salen de los [contribuidores en GitHub](https://github.com/DyingCoderLin/OS-Lab-Tutor/graphs/contributors), generadas con [contrib.rocks](https://contrib.rocks) (contributors-img). Nombres y perfiles: [AUTHORS.md](AUTHORS.md).

## Donaciones

Si TuTor te sirve para aprender, puedes invitarme un café por PayPal:

**[paypal.me/kevindperezm](https://paypal.me/kevindperezm?locale.x=es_XC&country.x=MX)**

Donar es opcional; no hace falta para usar el proyecto ni para contribuir.

## Licencia

[MIT](LICENSE) — Copyright (c) 2026 Kevin Perez
