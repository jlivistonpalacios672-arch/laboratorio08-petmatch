# Laboratorio 8 — PetMatch Mini: formularios, validación y CRUD

Este zip es el proyecto COMPLETO (Laboratorio 7 + Laboratorio 8). Reemplaza al del lab 7.
Los datos siguen en memoria: al reiniciar se pierden los cambios.

## Cómo usarlo
1. En tu carpeta `petmatch-lab` (la que tiene `mvnw`, `mvnw.cmd` y `.mvn/`):
   borra `src/` y `target/`, y copia `src/`, `pom.xml` y `.gitignore` de este zip.
2. Terminal de VS Code, dentro de esa carpeta:
```
.\mvnw.cmd test
.\mvnw.cmd spring-boot:run
```
(Linux/Mac: `./mvnw ...`). No necesita base de datos.

## Qué cambia respecto al lab 7
- pom.xml: + `spring-boot-starter-validation`
- NUEVO: `dto/PetForm.java`, `templates/pets/form.html`, `messages.properties`
- REEMPLAZADOS: `InMemoryPetRepository` (Map modificable, vuelve a 3 mascotas: Luna, Milo, Nube),
  `PetService`, `PetController`, `pets/list.html`, `pets/detail.html`, `application.css` (+ estilos al final)
- Tests: `InMemoryPetRepositoryTests`, `PetServiceTests` (ampliado), `PetControllerIntegrationTests`
- Reto integrador incluido: búsqueda por especie en `/pets?species=Gato`

## Probar en el navegador
| Acción | Resultado |
|---|---|
| /pets | 3 mascotas + buscador |
| /pets/new, enviar vacío o edad -1 | errores junto a cada campo, no se guarda |
| /pets/new con datos válidos | redirige a /pets/4 con mensaje verde |
| Editar (/pets/2/edit) | formulario con datos actuales; el id se conserva |
| Eliminar | desaparece del catálogo; /pets/ID da 404 |
| /pets?species=gato | solo Milo; /pets?species=Dragon -> "Sin coincidencias" |
| Reiniciar la app | vuelven las 3 mascotas iniciales |

## Si algo falla
- 404 en /pets/new: revisa que `createForm` esté en PetController (ruta fija, antes de /{id}).
- Error "Neither BindingResult..." : el `th:object` debe ser `petForm` y el controlador debe poner ese atributo.
- Prueba falla por cantidad de mascotas: las pruebas MVC comparten el repositorio en memoria; no dependen de cantidades.
