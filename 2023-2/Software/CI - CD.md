# 4 Team Performance metrics

Medir performance:
- Delivery lead time
- Deployment frequency
- Mean time to restore
- Change failure rate

## Delivery lead time
Cuanto tiempo toma desde subir un commit hasta llegar a producción. Cuanto tiempo una branch, llega main.

## Deployment frequency
Cuantas vece uno llega a producción (solo se cuenta, no se toma en cuenta el tiempo)

## Mean time to restore (MTTR)
Tiempo que toma solucionar un bug

## Change failure rate
Que porcentaje de lo que se sube (nivel commit, lineas) crean un bug



# Flujo Git

Mantener convención de mensaje de commits. 

1. git pull
2. git add .
3. git hook: (pre-commit) -> husky
	1. prettier: `formatter`
	2. lint: `eslint`
	3. manejador de dependencias: `knip`
4. git commit "mensaje"
5. (pre-push)
	1. test: `npm run test`
6. git push

## Formatter vs Linter

- Formatter: Solo ve cosas visuales, estética del código. `js: prettier; python: black`
- Linter: Análisis estático (AST) del árbol sintético. Cambia aspectos funcionales. No ven dependencias.
Pueden entrar en conflicto. Ciertos linter realizan ambas tareas, en ese caso solo utilizar linter.

## Git flow / Trunk Based Development

Git flow:
Tiene varias ramas (forks), para distintos tipos de tareas.

TBD:
- 1 forma: todos los commits a una rama (develop) y luego pr a main
- ramas short lived: develop (qa) - main (producción)
	- ramas short: una feature, nace de develop. Vive poco, y se hace pr a dev
