# Post-Contenido 2 - Pruebas E2E con Selenium, Postman y Newman

Proyecto Spring Boot basado en la aplicacion ToDo del Post-Contenido 1. Incluye pruebas E2E con Selenium usando Page Object Model, coleccion Postman con 5 requests y workflow de GitHub Actions con Newman.

## Requisitos

- Java 17 o superior.
- Maven 3.9.x o wrapper incluido (`mvnw.cmd`).
- Google Chrome estable instalado.
- Node.js 18+ con npm para ejecutar Newman localmente.
- Postman Desktop v10+ o Postman Web para importar la coleccion.

## Ejecutar la aplicacion

```powershell
.\mvnw.cmd spring-boot:run
```

La aplicacion queda disponible en:

```text
http://localhost:8080/tareas
```

## Checkpoint 1 - Selenium Page Object Model

Ejecutar solo las pruebas E2E:

```powershell
.\mvnw.cmd -Dtest=TareasE2ETest test
```

Evidencia: tomar captura de la terminal o del IDE mostrando `TareasE2ETest` con 2 tests en verde, 0 failures y 0 errors.

Clases implementadas:

- `e2e/TareasPage.java`: encapsula `btn-nueva` y `.tarea-item`.
- `e2e/NuevaTareaPage.java`: encapsula `titulo`, `descripcion` y `btn-guardar`.
- `e2e/TareasE2ETest.java`: ejecuta Chrome headless y valida carga de pagina y creacion desde formulario.

## Checkpoint 2 - Postman

Archivos incluidos:

- `postman/ColeccionToDo.json`
- `postman/env-local.json`
- `postman/env-ci.json`

Ejecutar en Postman Runner:

1. Importar `postman/ColeccionToDo.json`.
2. Importar el entorno `postman/env-local.json`.
3. Seleccionar el entorno `ToDoApp-Local`.
4. Verificar que la aplicacion este corriendo en `http://localhost:8080`.
5. Ejecutar la coleccion completa en orden.
6. Tomar captura del Runner mostrando 5 requests y 0 failures.

## Checkpoint 3 - Newman y GitHub Actions

Ejecutar Newman localmente:

```powershell
npm install -g newman
newman run postman/ColeccionToDo.json --environment postman/env-local.json
```

Workflow incluido:

```text
.github/workflows/api-tests.yml
```

Evidencia en GitHub:

1. Hacer push al repositorio.
2. Entrar a la pestana `Actions`.
3. Abrir el workflow `API Tests con Newman`.
4. Confirmar que aparece con check verde.
5. Tomar captura de la ejecucion mostrando los tests de Newman en verde.
