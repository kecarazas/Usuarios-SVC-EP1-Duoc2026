# Usuarios — Microservicio de riesgo usuarios

Microservicio correspondiente al **caso caso10 — CargoClick** (Logística / courier) de la Evaluación Parcial N°1.

| | |
|---|---|
| Stack | Spring Boot 3.3 · Java 21 · Maven · Spring Data JPA · H2 · springdoc-openapi |
| Calidad | JaCoCo cobertura LINE 100% · Cucumber (BDD) alineado a endpoints REST |
| Entrega | Docker / Docker Compose |

## Responsabilidad (SRP)

administra los datos y la lógica del dominio de Usuarios del caso caso10 (CargoClick). Su base de datos es una **H2 en memoria** (un solo microservicio por base), cumpliendo aislamiento de datos por dominio.

## Página de presentación

Al ejecutar el servicio, `http://localhost:8080/` muestra la página de presentación del microservicio con documentación y enlaces a:

- **Swagger UI**: `/swagger-ui/index.html`
- **OpenAPI (yaml)**: `/v3/api-docs.yaml`
- **ReDoc**: `/redoc.html`
- **H2 Console**: `/h2-console`

## Endpoints

| Método | Ruta | Descripción |
|--------|------|-------------|
| GET | `/api/usuarios` | Lista todos los recursos |
| GET | `/api/usuarios/{id}` | Obtiene un recurso por id |
| POST | `/api/usuarios` | Crea un recurso |
| PUT | `/api/usuarios/{id}` | Actualiza un recurso |
| DELETE | `/api/usuarios/{id}` | Elimina un recurso |

## Documentación del proyecto

La documentación completa está en la carpeta [`docs/`](docs/):

- [`docs/00_Resumen.md`](docs/00_Resumen.md) — propósito, responsabilidad y tecnologías
- [`docs/01_Arquitectura.md`](docs/01_Arquitectura.md) — componentes, arquitectura y patrones
- [`docs/02_API.md`](docs/02_API.md) — contrato REST y ejemplos curl
- [`docs/03_Pruebas.md`](docs/03_Pruebas.md) — tests unitarios, cobertura y Cucumber
- [`docs/04_Despliegue.md`](docs/04_Despliegue.md)
- [`docs/05_Justificacion.md`](docs/05_Justificacion.md) — justificación del servicio: RF/RNF/seguridad cubiertos, stack y por qué cada tecnología AWS
- [`docs/diagramas/`](docs/diagramas/) — C4 (contexto, contenedores, componentes), secuencia e infraestructura AWS — Docker, Docker Compose e integración

## Cómo ejecutar locamente

```bash
mvn spring-boot:run
```

## Cómo ejecutar con Docker

```bash
docker compose up --build
# http://localhost:8080
```

## Cómo ejecutar las pruebas

```bash
mvn test      # unit tests + Cucumber
mvn verify    # + verificación de cobertura JaCoCo (100% LINE, falla si baja)
```

## Modelo de ramificación

Elegimos GitFlow porque el proyecto se va desarrollando durante todo el semestre y cada entrega (EP01, EP02 y EP03) funciona como un punto importante y estable del proyecto. La rama **develop** nos permite juntar el trabajo de ambos integrantes sin modificar directamente **main**, por otro lado, si aparece algún error en producción, podemos usar una rama **hotfix/** para solucionarlo sin tener que detener el trabajo que estamos haciendo en desarrollo. 

También nos sirve para tener más orden, ya que **main** queda para las versiones estables y **develop** para el código que todavía estamos integrando y probando, así podemos llevar un mejor control de los cambios y tener más claro qué se ha hecho en cada etapa del proyecto, especialmente en relación con lo que se pide en las rúbricas del curso.

## Convención de commits
|Tipo |Para qué |Ejemplo
|--------|------|-------------|
feat |Nueva funcionalidad feat(ui):| agregar pie de pagina
fix |Corrección de bug fix(home):| corregir titulo
docs |Documentación docs: |agregar changelog
chore |Tareas / CI chore(ci):| agregar workflow hola mundo

Formato: **tipo(alcance):** descripcion-corta. Escrito en minúsculas y sin tildes.

## Naming de ramas
 * feature/<feature-name> y hotfix/<feature-name>, en minúsculas y con guiones.
 * Ejemplos: feature/pagina-presentacion, hotfix/titulo-pagina.

## Flujo de merge
* Features y hotfix siempre entran por pull request, nunca push directo a main o develop.

* Se necesita al menos 1 aprobación del compañero antes de fusionar.

*  Usar merge commit o squash, y borrar la rama después de fusionar.

## Estrategia de revisión
* El autor abre el PR y asigna un revisor.
* El revisor comenta, aprueba o pide cambios; nunca se fusiona un PR sin revisar.
* Antes de cada PR: confirmar que mvn test pasa y revisar la diff.

**Opcional:** crea PULL_REQUEST_TEMPLATE.md para automatizar la plantilla de revisión desde
GitHub.