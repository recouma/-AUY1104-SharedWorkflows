# AUY1104 — SharedWorkflows (Repositorio Central)

Repositorio proveedor de workflows reutilizables para la asignatura AUY1104 — Ciclo de Vida del Software II.

## Rol

Este repositorio centraliza la lógica de CI/CD mediante GitHub Actions Reusable Workflows. Los proyectos consumidores lo invocan con `uses:` sin necesidad de duplicar código.

## Contenido
## deploy-api.yaml — Jobs

| Job | Descripción |
|---|---|
| `deps-and-test` | Instala dependencias y ejecuta `npm test`. Si falla, el pipeline se detiene. |
| `build-and-push` | Solo corre si el job anterior fue exitoso. Construye y publica la imagen en Docker Hub. |

## Inputs requeridos

| Input | Descripción | Ejemplo |
|---|---|---|
| `image-name` | Nombre de la imagen en Docker Hub | `demo-api` |
| `image-tag` | Etiqueta de versión | `v1.0.0` |

## Secretos requeridos

| Secreto | Descripción |
|---|---|
| `DOCKER_USERNAME` | Usuario de Docker Hub del repositorio consumidor |
| `DOCKER_PASSWORD` | Access Token de Docker Hub (no la contraseña real) |

## Cómo consumir este workflow

```yaml
jobs:
  usar-receta-compartida:
    uses: recouma/-AUY1104-SharedWorkflows/.github/workflows/deploy-api.yaml@main
    with:
      image-name: demo-api
      image-tag: ${{ github.ref_name }}
    secrets:
      DOCKER_USERNAME: ${{ secrets.DOCKER_USERNAME }}
      DOCKER_PASSWORD: ${{ secrets.DOCKER_PASSWORD }}
```

## Asignatura

AUY1104 — Ciclo de Vida del Software II · Duoc UC · 2026
