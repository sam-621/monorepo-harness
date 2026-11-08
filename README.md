# monorepo-harness

Template de monorepo para trabajar con Claude Code. No trae código: trae las convenciones (estilo de código, arquitectura, testing y comandos) de cada tipo de app y el flujo de trabajo con features, agentes y QA. Las apps se instalan cuando se necesitan, con las dependencias del momento, siguiendo sus docs.

## Usar

1. En GitHub, **Use this template → Create a new repository** con el nombre del proyecto.
2. En el `CLAUDE.md` raíz, cambiar `<proyecto>` y la línea de descripción.
3. Borrar las apps que el proyecto no usa: su carpeta en `apps/`, sus agentes en `.claude/agents/`, su fila en la tabla del `CLAUDE.md` raíz y su scope en `.claude/skills/commit/SKILL.md`.
4. Instalar cada app dentro de su carpeta siguiendo su `docs/` (stack en `docs/architecture.md`, scripts en `docs/commands.md`). Lo mismo con `e2e/` cuando haya una UI que probar.

## Qué trae

```
.
├── CLAUDE.md                 reglas del repo, tabla de apps, flujo de features y formato de reportes
├── .claude/
│   ├── agents/               <app>-implementer y <app>-reviewer por app, e2e-implementer y e2e-qa
│   └── skills/               /session-start, /commit y /qa
├── features/_templates/      spec/product.md, technical.md, ui.md y log.md
├── apps/
│   ├── api/                  backend: API, servicio o microservicio (Express, GraphQL Yoga, Drizzle)
│   └── admin/                frontend con sesión: back office o portal de clientes (React, Vite, coss ui)
└── e2e/                      entorno aislado de pruebas y QA en el navegador
```

Cada app y `e2e/` tienen solo su `CLAUDE.md` (qué doc leer antes de escribir código) y su `docs/`.

## Flujo

- `/session-start <slug>`: abre el trabajo sobre `features/<slug>/`. Claude delega el código a `<app>-implementer` y revisa el diff con `<app>-reviewer`.
- `/qa <flujo>`: levanta `e2e/`, el agente `e2e-qa` recorre el flujo en el navegador como un humano y reporta los fallos con screenshots.
- `/commit`: commit con el formato del repo.

## Modificar el template

Las mejoras se hacen en este repo. Los proyectos ya creados conservan la versión con la que nacieron, y sus docs evolucionan solos: el `CLAUDE.md` raíz pide proponer cambios a `docs/` cuando aparece una decisión nueva, y el reviewer reporta los "patrones sin documentar".
