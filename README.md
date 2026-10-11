# github_actions_demo

![CI](https://github.com/AaronCoorahua/github_actions_demo/actions/workflows/devops.yml/badge.svg)
![Release](https://img.shields.io/github/v/release/AaronCoorahua/github_actions_demo)

Laboratorio de CI/CD con GitHub Actions y Python (UTEC – DevOps).

Página publicada: https://aaroncoorahua.github.io/github_actions_demo/

## Pipeline

| Workflow | Disparador | Jobs |
|---|---|---|
| `.github/workflows/devops.yml` | push a `main`, PR (opened/synchronize/reopened) | `test` → `package` → `docs` / `deploy` |
| `.github/workflows/release.yml` | push de tags `v*` | `release` |

- **test**: instala dependencias (con cache de pip), corre pytest con gate de cobertura ≥ 80%, publica `test-report` (report.xml + coverage.xml), `build-info` y un Job Summary.
- **package**: empaqueta `hello.py` en `app-<build_tag>.zip`.
- **docs**: imprime información del repositorio y del runner.
- **deploy**: renderiza `site/index.html` y lo publica en GitHub Pages (entorno `github-pages` con aprobación manual).
- **release**: corre los tests, crea `app-<tag>.zip` y publica un GitHub Release con notas generadas.

## Ejecutar en local

```bash
pip install -r requirements.txt
python hello.py
pytest -q --cov --cov-report=term-missing
```

La configuración de cobertura (umbral 80% y exclusión del bloque `__main__`) está en `.coveragerc`.

## Publicar una versión

```bash
git tag -a v1.0.0 -m "Primera versión estable"
git push origin v1.0.0
```
